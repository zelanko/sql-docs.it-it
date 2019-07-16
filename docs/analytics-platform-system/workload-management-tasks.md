---
title: Attività di gestione del carico di lavoro - sistema di piattaforma Analitica | Microsoft Docs
description: Attività di gestione del carico di lavoro nel sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea6b3785914781e73a8570c1282741f7c4b56298
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959751"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Attività di gestione del carico di lavoro nel sistema di piattaforma Analitica
Attività di gestione del carico di lavoro nel sistema di piattaforma Analitica.

## <a name="view-login-members-of-each-resource-class"></a>Visualizzare i membri di account di accesso di ogni classe di risorse
Viene descritto come visualizzare i membri di account di accesso di ogni ruolo del server di classe di risorse in SQL Server PDW. Usare questa query per individuare la classe di risorse consentiti per le richieste inviate da ogni account di accesso.  
  
Per descrizioni classe di risorse, vedere [Workload Management](workload-management.md).  
  
Questa query consente di visualizzare l'elenco di appartenenze per ogni classe di risorse. Esistono tre classi di risorse, mediumrc, largerc e xlargerc.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
Se un account di accesso non è inclusa nell'elenco, le relative richieste riceverà le risorse predefinite. Se un account di accesso è un membro di più di una classe di risorse, la classe più grande ha la precedenza.  
  
Le allocazioni di risorse sono racchiusi [Workload Management](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Modificare le risorse di sistema allocate a una richiesta
Viene descritto come individuare la risorsa di classe in cui è in esecuzione una richiesta di SQL Server PDW, quindi come modificare le risorse di sistema per la richiesta. Modifica le risorse per una richiesta richiede la modifica dell'appartenenza di classe di risorse dell'account di accesso di invio della richiesta, tramite il [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) istruzione.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Passaggio 1: Determinare la classe di risorse per l'account di accesso che esegue la richiesta.  
Questa query consente di visualizzare gli account di accesso che sono membri delle appartenenze al ruolo di server di classe di risorse. Esistono tre classi di risorse, **mediumrc**, **largerc**, e **xlargerc**.  
  
> [!IMPORTANT]  
> Questa query deve essere eseguita da un account di accesso che dispone **CONTROL SERVER** l'autorizzazione. Se eseguito da un account di accesso senza **CONTROL SERVER** autorizzazione, questa query restituisce solo le appartenenze al ruolo per l'account di accesso corrente.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
Se non sono presenti Nessun account di accesso che sono membri di un ruolo del server di classe di risorse, la tabella risultante sarà vuota. In questo caso, se la query restituisce un account di accesso denominato Ching, quindi quando Ching invia una richiesta, la richiesta riceverà le risorse di sistema predefinite, che sono inferiori alle risorse di sistema di classe di risorse. Se un account di accesso è un membro di più di una classe di risorse, la classe più grande ha la precedenza.  
  
Per un elenco delle allocazioni di risorse per ogni classe di risorse, vedere [Workload Management](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Passaggio 2: Eseguire la richiesta con un account di accesso con l'appartenenza alla classe di risorse diverso  
Esistono due modi per eseguire una richiesta con entrambi risorse di sistema o aumentandone le dimensioni:  
  
-   Eseguire la richiesta con un account di accesso diversi che è un membro di una classe di risorse superiori o inferiori.  
  
-   Aggiungere l'account di accesso necessario per uno dei ruoli di classe di risorse. Scegliere questa opzione con cautela. modifica la classe di risorse per l'account di accesso cambierà il livello di risorse di sistema per tutte le richieste inviate dall'account di accesso.  
  
Si supponga che Ching è un membro del ruolo del server largerc. Nell'esempio seguente viene illustrato come aggiungere account di accesso Ching al ruolo del server xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching fa parte di largerc e xlargerc i ruoli del server. Quando Ching invia le richieste, le richieste ricevono le risorse di sistema xlargerc.  
  
Nell'esempio seguente sposta Ching nuovamente al ruolo del server mediumrc.  Per modificare al nuovo ruolo, l'account di accesso deve essere rimosso dal ruolo xlargerc e ruoli del server largerc e aggiunto al ruolo del server mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching è ora un membro del ruolo del server mediumrc.  L'esempio seguente modifica Ching affinché le risorse di sistema predefinite per le richieste.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Per altre informazioni su come modificare l'appartenenza al ruolo di classe di risorse, vedere [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Modificare un account di accesso alle risorse di sistema predefinito per le richieste
Viene descritto come modificare le allocazioni di risorse di sistema assegnate a un account di accesso di SQL Server PDW per la quantità predefinita. 
  
Per descrizioni classe di risorse, vedere [Workload Management](workload-management.md)  
  
Quando un account di accesso non è un membro di qualsiasi ruolo di server di classe di risorse, le richieste inviate dall'account di accesso riceveranno la quantità di risorse di sistema predefinita.  
  
Si supponga che l'account di accesso Matt è attualmente un membro di tutti i ruoli di server di classe di risorse e vuole ripristinare con le richieste ricevano solo le risorse predefinite.  L'esempio seguente assegna le risorse predefinite per le richieste di Matt eliminando l'appartenenza a da tutti i ruoli del server classe tre risorse.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Visualizza che il numero di slot di concorrenza necessari per un'attesa richieste
Viene descritto come determinare il numero di concorrenza sono necessari spazi da una richiesta che è in attesa di esecuzione in SQL Server PDW.  
  
Per altre informazioni, vedere [Workload Management](workload-management.md).  
  
Una richiesta potrebbe essere in attesa troppo a lungo senza essere eseguito. Uno dei modi per risolvere i problemi della richiesta è esaminare il numero di slot di concorrenza, che la richiesta è necessario.  Nell'esempio seguente mostra il numero di slot di concorrenza necessari per ogni richiesta in attesa.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Vedere anche  
[Gestione del carico di lavoro](workload-management.md)  
  
