---
title: Funzione di classificazione di Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function
- user-defined functions [SQL Server], classifier function
- classifier function [SQL Server]
- classifier function [SQL Server], overview
ms.assetid: 64c25012-7068-476f-afa2-0b4f3adde9a4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 69b6fd10ac0adc6f76925e0d41f110b917111466
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063543"
---
# <a name="resource-governor-classifier-function"></a>Funzione di classificazione di Resource Governor
  Il processo di classificazione di Resource Governor in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di assegnare sessioni in ingresso a un gruppo di carico di lavoro in base alle caratteristiche della sessione. È possibile personalizzare la logica di classificazione scrivendo una funzione definita dall'utente, chiamata funzione di classificazione.  
  
## <a name="classification"></a>Classificazione  
 Resource Governor supporta la classificazione delle sessioni in ingresso. La classificazione è basata su un set di criteri definiti dall'utente contenuti in una funzione. I risultati della logica della funzione consentono a Resource Governor di classificare sessioni in gruppi del carico di lavoro esistenti.  
  
> [!NOTE]  
>  Il gruppo del carico di lavoro interno è popolato con richieste per solo uso interno. Non è possibile modificare i criteri utilizzati per indirizzare tali richieste né è possibile classificare richieste nel gruppo del carico di lavoro interno.  
  
 È possibile scrivere una funzione scalare che contiene la logica utilizzata per assegnare sessioni in ingresso a un gruppo del carico di lavoro. Prima che sia possibile utilizzare tale funzione, è necessario completare le operazioni seguenti:  
  
-   Creare e registrare la funzione utilizzando l'istruzione ALTER RESOURCE GOVERNOR. Per altre informazioni, vedere [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
-   Aggiornare la configurazione di Resource Governor utilizzando l'istruzione ALTER RESOURCE GOVERNOR con il parametro RECONFIGURE.  
  
 Dopo avere creato la funzione e applicato le modifiche di configurazione, la funzione di classificazione di Resource Governor utilizzerà il nome del gruppo del carico di lavoro restituito dalla funzione per inviare una nuova richiesta al gruppo del carico di lavoro appropriato.  
  
> [!IMPORTANT]  
>  Potrebbe verificarsi il timeout della sessione client se la funzione di classificazione non viene completata entro il timeout specificato per l'accesso. Il timeout di accesso è una proprietà client e, in quanto tale, il server non è a conoscenza di un timeout. Una funzione di classificazione con esecuzione prolungata può lasciare il server con connessioni orfane per periodi prolungati. È importante che vengano create funzioni di classificazione che terminano l'esecuzione prima del timeout della connessione.  
  
 La funzione definita dall'utente ha le seguenti caratteristiche e comportamenti:  
  
-   La funzione definita dall'utente viene valutata per ogni nuova sessione, anche quando il pool di connessioni è abilitato.  
  
-   La funzione definita dall'utente fornisce il contesto del gruppo del carico di lavoro per la sessione. Dopo che l'appartenenza a un gruppo è stata determinata, la sessione viene associata al gruppo del carico di lavoro per la durata della sessione.  
  
-   Se la funzione definita dall'utente restituisce NULL, il valore predefinito o il nome di un gruppo non esistente, alla sessione viene fornito il contesto predefinito del gruppo del carico di lavoro. Alla sessione viene inoltre fornito il contesto predefinito se per qualsiasi motivo la funzione non riesce.  
  
-   La funzione deve essere definita con l'ambito del server (database master).  
  
-   La designazione della funzione di classificazione definita dall'utente viene applicata solo dopo l'esecuzione di ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   È possibile definire come classificatore solo una funzione definita dall'utente alla volta.  
  
-   La funzione di classificazione definita dall'utente non può essere eliminata o modificata a meno che non venga rimosso lo stato di classificazione.  
  
-   In assenza di una funzione di classificazione definita dall'utente, tutte le sessioni vengono classificate nel gruppo predefinito.  
  
-   Il gruppo del carico di lavoro restituito dalla funzione di classificazione è esterno all'ambito della restrizione relativa all'associazione allo schema. Non è possibile ad esempio eliminare una tabella, ma è possibile eliminare un gruppo del carico di lavoro.  
  
> [!IMPORTANT]  
>  Si consiglia di abilitare la connessione amministrativa dedicata nel server. Tale connessione non è soggetta alla classificazione di Resource Governor e può essere utilizzata per monitorare e risolvere i problemi relativi a una funzione di classificazione. Per altre informazioni, vedere [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Se per la risoluzione dei problemi non è disponibile alcuna connessione DAC, è possibile riavviare il sistema in modalità utente singolo. Sebbene tale modalità non sia soggetta alla classificazione, non consente di eseguire la diagnosi della classificazione di Resource Governor mentre quest'ultimo è in esecuzione.  
  
### <a name="classification-process"></a>Processo di classificazione  
 Nel contesto di Resource Governor il processo di accesso per una sessione è costituito dai passaggi seguenti:  
  
1.  Autenticazione dell'account di accesso  
  
2.  Esecuzione del trigger LOGON  
  
3.  Classificazione  
  
 Quando la classificazione viene avviata, in Resource Governor viene eseguita la funzione di classificazione e il valore restituito dalla funzione viene utilizzato per inviare richieste al gruppo del carico di lavoro appropriato.  
  
> [!NOTE]  
>  Informazioni sull'esecuzione della funzione di classificazione e sui trigger LOGON sono disponibili in [sys.dm_exec_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) e [sys.dm_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql).  
  
## <a name="classification-function-tasks"></a>Attività della funzione di classificazione  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come creare e verificare una funzione di classificazione definita dall'utente.|[Creare e testare una funzione di classificazione definita dall'utente](create-and-test-a-classifier-user-defined-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Abilitare Resource Governor](enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Configurare Resource Governor utilizzando un modello](configure-resource-governor-using-a-template.md)   
 [Visualizzare proprietà di Resource Governor](view-resource-governor-properties.md)  
  
  
