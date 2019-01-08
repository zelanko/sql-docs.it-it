---
title: Snapshot per pubblicazioni di tipo merge con filtri con parametri | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 25df8e37a8ed1a9f88438558edc2770081dbddcb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751014"
---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>Snapshot per pubblicazioni di tipo merge con filtri con parametri
  Quando si utilizzano filtri di riga con parametri nelle pubblicazioni di tipo merge, ogni sottoscrizione con uno snapshot in due parti viene inizializzata dalla replica. Viene innanzitutto creato uno snapshot dello schema contenente tutti gli oggetti necessari alla replica e lo schema degli oggetti pubblicati, ma non i dati. Ogni sottoscrizione viene quindi inizializzata con uno snapshot che include gli oggetti e lo schema dello snapshot dello schema e i dati appartenenti alla partizione della sottoscrizione. Se più di una sottoscrizione riceve una determinata partizione, ovvero riceve lo stesso schema e gli stessi dati, lo snapshot di tale partizione viene creato una sola volta. Dallo stesso snapshot vengono inizializzate più sottoscrizioni. Per ulteriori informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](merge/parameterized-filters-parameterized-row-filters.md).  
  
 È possibile creare snapshot per pubblicazioni con filtri con parametri in tre modi diversi:  
  
-   Pregenerare uno snapshot per ogni partizione. Questa opzione consente di controllare il momento in cui vengono generati gli snapshot.  
  
     È inoltre possibile aggiornare gli snapshot in base a una pianificazione. I nuovi Sottoscrittori che sottoscrivono una partizione per cui è stato creato uno snapshot riceveranno uno snapshot aggiornato.  
  
-   Consentire ai Sottoscrittori di richiedere la generazione e l'applicazione dello snapshot alla prima sincronizzazione. Questa opzione consente ai nuovi Sottoscrittori di eseguire la sincronizzazione senza l'intervento di un amministratore. Per consentire la generazione dello snapshot, è necessario che[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione nel server di pubblicazione.  
  
    > [!NOTE]  
    >  Se il filtro di uno o più articoli nella pubblicazione restituisce partizioni non sovrapposte univoche per ogni sottoscrizione, i metadati vengono eliminati a ogni esecuzione dell'agente di merge. Lo snapshot partizionato scade quindi più rapidamente. Quando si utilizza questa opzione, è consigliabile consentire ai Sottoscrittori di inizializzare la generazione e il recapito dello snapshot. Per ulteriori informazioni sulle opzioni di filtro, vedere [Filtri di riga con parametri](merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Generare manualmente uno snapshot per ogni Sottoscrittore con l'agente snapshot. Il Sottoscrittore deve quindi indicare il percorso dello snapshot all'agente di merge, in modo che sia possibile recuperare e applicare lo snapshot corretto.  
  
    > [!NOTE]  
    >  Questa opzione è supportata per garantire la compatibilità con le versioni precedenti e non consente le condivisioni snapshot FTP.  
  
 Il metodo più flessibile consiste nell'utilizzo di una combinazione di opzioni snapshot pregenerate e richieste dal Sottoscrittore: gli snapshot vengono pregenerati e aggiornati in base a una pianificazione, in genere durante i periodi di minore attività, ma un Sottoscrittore può generare il proprio snapshot nel caso in cui venga creata una sottoscrizione per cui è necessaria una nuova partizione.  
  
 Considerare [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], che dispone di forza lavoro mobile per la distribuzione delle scorte ai singoli negozi. Ogni venditore riceve una sottoscrizione basata sul proprio account di accesso, che consente di recuperare i dati relativi ai negozi serviti. L'amministratore decide di pregenerare gli snapshot e di aggiornarli ogni domenica. Occasionalmente viene aggiunto al sistema un nuovo utente per il quale sono necessari i dati per una partizione per cui non è disponibile alcuno snapshot. L'amministratore decide inoltre di consentire gli snapshot inizializzati dal Sottoscrittore, per evitare che si verifichi una situazione in cui un Sottoscrittore non può sottoscrivere la pubblicazione in quanto lo snapshot non è ancora disponibile. Quando il nuovo Sottoscrittore effettua la prima connessione, lo snapshot per la partizione specificata viene generato e viene applicato al Sottoscrittore. Per consentire la generazione dello snapshot, è necessario che[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione nel server di pubblicazione.  
  
 Per creare uno snapshot per una pubblicazione con filtri con parametri, vedere [Creazione di uno snapshot per una pubblicazione di tipo merge con filtri con parametri](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="security-settings-for-the-snapshot-agent"></a>Impostazioni di sicurezza per l'agente snapshot  
 L'agente snapshot crea gli snapshot per ogni partizione. Per gli snapshot pregenerati e per quelli richiesti da un Sottoscrittore, viene eseguito l'agente e vengono effettuate le connessioni con le credenziali specificate al momento della creazione del processo dell'agente snapshot. Tale processo viene creato tramite la Creazione guidata nuova pubblicazione o **sp_addpublication_snapshot**. Per modificare le credenziali, utilizzare **sp_changedynamicsnapshot_job**. Per altre informazioni, vedere [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Filtri di riga con parametri](merge/parameterized-filters-parameterized-row-filters.md)   
 [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md)  
  
  
