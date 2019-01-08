---
title: Creare e applicare lo snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], applying
- snapshots [SQL Server replication], creating
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd78bf7da1a68e7e053af52c4fa8f9cf0cd71094
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52755643"
---
# <a name="create-and-apply-the-snapshot"></a>Creare e applicare lo snapshot
  Gli snapshot vengono generati dall'agente snapshot al termine della creazione di una pubblicazione. La generazione può essere eseguita:  
  
-   Immediatamente. Per impostazione predefinita, per una pubblicazione di tipo merge uno snapshot viene generato immediatamente dopo la creazione di una pubblicazione mediante la Creazione guidata nuova pubblicazione.  
  
-   A un'ora pianificata. Specificare una pianificazione nella pagina **Agente snapshot** della Creazione guidata nuova pubblicazione o quando si utilizzano stored procedure o Replication Management Objects (RMO).  
  
-   Manualmente. Eseguire l'agente snapshot dal prompt dei comandi o da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sull'esecuzione degli agenti, vedere [Concetti di base relativi ai file eseguibili dell'agente di replica](concepts/replication-agent-executables-concepts.md) e [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
 Per la replica di tipo merge, viene generato uno snapshot a ogni esecuzione dell'agente snapshot. Per la replica transazionale, la generazione dello snapshot dipende dall'impostazione della proprietà di pubblicazione **immediate_sync**. Se tale proprietà è impostata su TRUE, ovvero il valore predefinito quando si utilizza la Creazione guidata nuova pubblicazione, viene generato uno snapshot ogni volta che viene eseguito l'agente snapshot, che può essere applicato a un Sottoscrittore in qualsiasi momento. Se invece è impostata su FALSE, ovvero il valore predefinito quando si utilizza **sp_addpublication**, lo snapshot viene generato solo se è stata aggiunta una nuova sottoscrizione dopo l'ultima esecuzione dell'agente snapshot. Per poter eseguire la sincronizzazione, è necessario che i sottoscrittori attendano il completamento dell'agente snapshot.  
  
 Per impostazione predefinita, una volta generati gli snapshot vengono salvati nella cartella snapshot predefinita nel server di distribuzione. È anche possibile salvare i file di snapshot su supporti rimovibili come dischi rimovibili, CD-ROM o in posizioni diverse dalla cartella snapshot predefinita. È inoltre possibile comprimere i file in modo da semplificarne l'archiviazione e il trasferimento ed eseguire script prima o dopo aver applicato lo snapshot nel Sottoscrittore. Per altre informazioni su queste opzioni, vedere [Snapshot Options](snapshot-options.md).  
  
 Se lo snapshot è per una pubblicazione di tipo merge che utilizza filtri con parametri, verrà creato utilizzando un processo a due fasi. Viene innanzitutto creato uno snapshot dello schema contenente gli script di replica e lo schema degli oggetti pubblicati, ma non i dati. Ogni sottoscrizione viene quindi inizializzata con uno snapshot che include gli script e lo schema copiati dallo snapshot dello schema e i dati appartenenti alla partizione della sottoscrizione. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Dopo aver creato lo snapshot nel server di pubblicazione e averlo archiviato in una posizione snapshot predefinita o alternativa, sarà possibile trasferirlo nel Sottoscrittore e applicarlo. L'agente di distribuzione (per la replica snapshot o transazionale) o l'agente di merge (per la replica di tipo merge) trasferisce lo snapshot e applica lo schema e i file di dati al database di sottoscrizione sul Sottoscrittore durante la sincronizzazione iniziale. Per impostazione predefinita, se si utilizza la Creazione guidata nuova sottoscrizione la sincronizzazione iniziale viene eseguita subito dopo la creazione di una sottoscrizione. Questo comportamento è controllato dall'opzione **Inizializza quando** della pagina **Inizializza sottoscrizioni** della procedura guidata. Gli snapshot generati in seguito all'inizializzazione di una sottoscrizione non vengono applicati a un Sottoscrittore a meno che la sottoscrizione non sia contrassegnata per la reinizializzazione. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](reinitialize-subscriptions.md).  
  
 Dopo aver applicato lo snapshot iniziale, l'agente di distribuzione o l'agente di merge propaga gli aggiornamenti successivi e le altre modifiche dei dati. La distribuzione e l'applicazione degli snapshot nei Sottoscrittori hanno effetto solamente sui Sottoscrittori in attesa dello snapshot iniziale o di nuovi snapshot, mentre non hanno alcun effetto sui Sottoscrittori della pubblicazione in cui sono già state eseguite operazioni di inserimento, aggiornamento ed eliminazione o altre modifiche dei dati pubblicati.  
  
 Per creare e applicare lo snapshot iniziale, vedere [Create and Apply the Initial Snapshot](create-and-apply-the-initial-snapshot.md).  
  
 Per visualizzare o modificare la posizione della cartella snapshot predefinita, vedere  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Specificare la posizione predefinita degli Snapshot &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   Programmazione della replica e programmazione di RMO: [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)  
  
  
