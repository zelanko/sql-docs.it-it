---
title: Attività di gestione del carico di lavoro
description: Attività di gestione del carico di lavoro nel sistema della piattaforma Analytics.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399410"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Attività di gestione del carico di lavoro nel sistema della piattaforma Analytics
Attività di gestione del carico di lavoro nel sistema della piattaforma Analytics.

## <a name="view-login-members-of-each-resource-class"></a>Visualizzare i membri di accesso di ogni classe di risorse
Viene descritto come visualizzare i membri di accesso di ogni ruolo del server della classe di risorse in SQL Server PDW. Usare questa query per determinare la classe di risorse consentite per le richieste inviate da ogni account di accesso.  
  
Per le descrizioni delle classi di risorse, vedere [gestione del carico di lavoro](workload-management.md).  
  
Questa query consente di visualizzare l'elenco delle appartenenze per ogni classe di risorse. Sono disponibili tre classi di risorse, mediumrc, largerc e xlargerc.  
  
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
  
Se un account di accesso non è presente nell'elenco, le relative richieste riceveranno le risorse predefinite. Se un account di accesso è membro di più di una classe di risorse, la classe più grande ha la precedenza.  
  
Le allocazioni di risorse sono elencate in [gestione del carico di lavoro](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Modificare le risorse di sistema allocate a una richiesta
Viene descritto come individuare la classe di risorse in cui viene eseguita una richiesta di SQL Server PDW e come modificare le risorse di sistema per la richiesta. Per modificare le risorse per una richiesta, è necessario modificare l'appartenenza alla classe di risorse dell'account di accesso che invia la richiesta, usando l'istruzione [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md) .  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Passaggio 1: determinare la classe di risorse per l'account di accesso che esegue la richiesta.  
Questa query consente di visualizzare gli account di accesso che sono membri delle appartenenze ai ruoli del server della classe di risorse. Sono disponibili tre classi di risorse, **mediumrc**, **largerc**e **xlargerc**.  
  
> [!IMPORTANT]  
> Questa query deve essere eseguita da un account di accesso con autorizzazione **Control Server** . Se eseguita da un account di accesso senza autorizzazione **Control Server** , questa query restituisce solo le appartenenze ai ruoli per l'account di accesso corrente.  
  
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
  
Se non sono presenti account di accesso che sono membri di un ruolo del server della classe di risorse, la tabella risultante sarà vuota. In questo caso, se la query restituisce un account di accesso denominato Ching, quando Ching invia una richiesta, la richiesta riceverà le risorse di sistema predefinite, che sono inferiori alle risorse di sistema della classe di risorse. Se un account di accesso è membro di più di una classe di risorse, la classe più grande ha la precedenza.  
  
Per un elenco delle allocazioni di risorse per ogni classe di risorse, vedere [gestione del carico di lavoro](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Passaggio 2: eseguire la richiesta con un account di accesso con appartenenza a una classe di risorse diversa  
Esistono due modi per eseguire una richiesta con risorse di sistema più grandi o più piccole:  
  
-   Eseguire la richiesta con un account di accesso diverso che sia membro di una classe di risorse più grande o più piccola.  
  
-   Aggiungere l'account di accesso necessario a uno dei ruoli della classe di risorse. Scegliere questa opzione con cautela. la modifica della classe di risorse per l'account di accesso modificherà il livello di risorse di sistema per tutte le richieste inviate dall'account di accesso.  
  
Si supponga che Ching sia un membro del ruolo del server largerc. Nell'esempio seguente viene illustrato come aggiungere login Ching al ruolo server xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching è ora un membro dei ruoli del server largerc e xlargerc. Quando Ching invia richieste, le richieste riceveranno le risorse di sistema xlargerc.  
  
Nell'esempio seguente viene spostato di nuovo il ruolo server mediumrc.  Per passare al nuovo ruolo, è necessario rimuovere l'account di accesso dai ruoli del server xlargerc e largerc e aggiungerlo al ruolo del server mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching è ora un membro del ruolo server mediumrc.  Nell'esempio seguente viene modificato Ching in modo da disporre delle risorse di sistema predefinite per le richieste.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Per ulteriori informazioni sulla modifica dell'appartenenza al ruolo della classe di risorse, vedere [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Modificare un account di accesso alle risorse di sistema predefinite per le relative richieste
Viene descritto come modificare le allocazioni delle risorse di sistema assegnate a un SQL Server PDW account di accesso agli importi predefiniti. 
  
Per le descrizioni delle classi di risorse, vedere [gestione del carico di lavoro](workload-management.md)  
  
Quando un account di accesso non è un membro di un ruolo del server della classe di risorse, le richieste inviate dall'account di accesso riceveranno la quantità predefinita di risorse di sistema.  
  
Si supponga che l'account di accesso opaco sia attualmente un membro di tutti i ruoli del server della classe di risorse e che voglia ripristinare le richieste che ricevono solo le risorse predefinite.  Nell'esempio seguente vengono assegnate le risorse predefinite alle richieste di Matt rilasciando l'appartenenza da tutti e tre i ruoli del server della classe di risorse.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Visualizzare il numero di slot di concorrenza necessari per una richiesta in attesa
Viene descritto come determinare il numero di slot di concorrenza necessari per una richiesta in attesa di essere eseguita in SQL Server PDW.  
  
Per ulteriori informazioni, vedere [gestione del carico di lavoro](workload-management.md).  
  
Una richiesta potrebbe rimanere in attesa troppo A lungo senza essere eseguita. Uno dei modi per risolvere i problemi relativi alla richiesta è esaminare il numero di slot di concorrenza necessari per la richiesta.  Nell'esempio seguente viene illustrato il numero di slot di concorrenza necessari per ogni richiesta in attesa.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Vedere anche  
[Gestione del carico di lavoro](workload-management.md)  
  
