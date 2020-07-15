---
title: Modificare le opzioni di inizializzazione dello snapshot
description: Modificare varie opzioni di inizializzazione dello snapshot di replica, ad esempio il formato dello snapshot e il percorso della cartella snapshot in SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3117e274c146413dcf8b973f054c7d0b1865e7de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767607"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificare le opzioni di inizializzazione dello snapshot per la replica di SQL 
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Quando [si inizializza una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md) sono disponibili diverse opzioni.

## <a name="specify-snapshot-format-sql-server-management-studio"></a>Specifica del formato dello snapshot (SQL Server Management Studio)
  Specificare il formato dello snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Publication>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Per specificare il formato dello snapshot  
  
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Publication>** selezionare **Formato nativo di SQL Server: tutti i Sottoscrittori devono essere server che eseguono SQL Server** oppure **Carattere: obbligatorio se in un server di pubblicazione o in un Sottoscrittore non è in esecuzione SQL Server**.  
  
    > [!NOTE]  
    >  È consigliabile selezionare il formato nativo a meno che la pubblicazione non debba supportare sottoscrizioni a un database di SQL Server Compact o a un database non di SQL Server.  
  
2.  Selezionare **OK**.   

## <a name="snapshot-folder-locations"></a>Posizioni della cartella snapshot

### <a name="default-snapshot-location"></a>Posizione predefinita degli snapshot
Specificare la posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Configurazione guidata distribuzione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md). Se si crea una pubblicazione su un server non configurato come server di distribuzione, specificare una posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modificare la posizione predefinita degli snapshot nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<Distributor>** . Per altre informazioni, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Impostare la cartella snapshot per ogni pubblicazione nella finestra di dialogo **Proprietà pubblicazione - \<Publication>** . Per altre informazioni, vedere [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Per modificare la posizione predefinita degli snapshot  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<Distributor>** fare clic sul pulsante delle proprietà ( **...** ) per il server di pubblicazione di cui modificare la posizione predefinita degli snapshot.    
2.  Nella finestra di dialogo **Proprietà server di pubblicazione - \<Publisher>** immettere un valore per la proprietà **Cartella snapshot predefinita**.  
  
    > [!NOTE]  
    >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).    
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
 

### <a name="alternate-snapshot-locations"></a>Posizioni alternative della cartella snapshot
Le posizioni alternative della cartella snapshot consentono di archiviare i file di snapshot in una posizione aggiuntiva o diversa da quella predefinita, in genere inclusa nel database di distribuzione. Una posizione alternativa può essere un altro server, un'unità di rete oppure un supporto rimovibile, ad esempio un CD-ROM o un disco rimovibile.  
  
Le posizioni alternative della cartella snapshot vengono archiviate come proprietà della pubblicazione. Dato che la posizione alternativa della cartella snapshot è una proprietà della pubblicazione, l'agente di distribuzione e l'agente di merge sono in grado di individuare la cartella snapshot corretta durante il processo di sincronizzazione.  
  
Se si desidera specificare una posizione alternativa della cartella snapshot o comprimere i file di snapshot senza creare immediatamente lo snapshot iniziale, è possibile impostare le proprietà della pubblicazione relative alla posizione dello snapshot e quindi eseguire l'agente snapshot per tale pubblicazione. Se tuttavia si modifica la posizione alternativa dopo avere creato lo snapshot iniziale, è possibile che gli snapshot generati per la pubblicazione non vengano ricollocati nella nuova posizione alternativa. In questo caso, a seconda delle impostazioni di pubblicazione, l'agente di merge o l'agente di distribuzione potrebbero non essere in grado di trovare i file di snapshot nella nuova posizione alternativa.  
  
> [!NOTE]  
>  Evitare di specificare una posizione alternativa che corrisponde alla posizione predefinita della cartella snapshot utilizzando la finestra di dialogo **Proprietà pubblicazione** o [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md).  
  
> [!CAUTION]  
>  Non utilizzare contemporaneamente sia WebSync sia percorsi alternativi della cartella snapshot.  
  
#### <a name="use-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Publication>** :  
  
    1.  Selezionare **Inserisci i file nella cartella seguente**e quindi fare clic su **Sfoglia** per passare a una directory oppure immettere il percorso della directory in cui devono essere archiviati i file di snapshot.  
  
        > [!NOTE]  
        >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Deselezionare **Inserisci i file nella cartella predefinita** a meno che non sia necessario scrivere i file di snapshot in entrambe le posizioni.  
  
     Per comprimere i file di snapshot, selezionare **Comprimi i file di snapshot in questa cartella**. La compressione viene in genere utilizzata per le connessioni a larghezza di banda ridotta e per i percorsi alternativi per lo snapshot nei supporti rimovibili, ad esempio un CD-ROM.  
  
2.  Selezionare **OK**.  
  
#### <a name="use-transact-sql"></a>Usare Transact-SQL 

Quando [si configurano le proprietà dello snapshot &#40;Programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), specificare il valore per **snapshot_in_defaultfolder** come False. 

## <a name="compressed-snapshots"></a>Snapshot compressi
  È consigliabile comprimere i file di snapshot quando vengono trasferiti in una rete lenta o salvati su supporti rimovibili in cui lo spazio disponibile non è sufficiente per contenere uno snapshot non compresso. La compressione, pur essendo utile in queste situazioni, richiede più tempo per generare e applicare lo snapshot.  
  
 I file di snapshot compressi vengono scritti nel formato di file [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB, che consente di comprimere file di 2 GB o di dimensione inferiore. La compressione non è invece possibile per file di dimensione superiore a 2 GB. Per comprimere i file, è necessario scriverli in una cartella snapshot alternativa, in quanto non è possibile comprimere i file scritti nella cartella predefinita. 
  
 I file vengono decompressi nella posizione di esecuzione dell'agente di distribuzione o dell'agente di merge. Con gli snapshot compressi vengono in genere utilizzate sottoscrizioni pull, in modo che i file vengano decompressi nel Sottoscrittore. Quando il Sottoscrittore riceve un file compresso, quest'ultimo viene scritto inizialmente in un percorso temporaneo. Dopo che il file compresso è stato copiato nel Sottoscrittore, i file di snapshot nel file compresso vengono decompressi, in ordine e uno alla volta, tramite l'utilità CAB. Lo spazio necessario nel Sottoscrittore equivale alla somma della dimensione del file compresso e della dimensione del file non compresso più grande.  
  
> [!NOTE]  
>  Gli snapshot compressi, in alcuni casi, consentono di migliorare le prestazioni relative al trasferimento di file di snapshot in rete. La compressione dello snapshot richiede, tuttavia, un'ulteriore elaborazione da parte dell'agente snapshot per la generazione dei file di snapshot e da parte dell'agente di distribuzione o dell'agente di merge per l'applicazione di tali file. Questo può rallentare il processo di generazione degli snapshot e, in alcuni casi, aumentare il tempo necessario per applicarli. Inoltre, poiché non è possibile riprendere gli snapshot compressi in caso di errore della rete, tali snapshot non sono adatti per le reti non affidabili. Quando si utilizzano snapshot compressi in rete, è necessario considerare tutti i pro e contro.  
  
### <a name="use-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Publication>** :  
  
    1.  Selezionare **Inserisci i file nella cartella seguente**e quindi fare clic su **Sfoglia** per passare a una directory oppure immettere il percorso della directory in cui devono essere archiviati i file di snapshot.  
  
        > [!NOTE]  
        >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).  
  
    2.  Deselezionare **Inserisci i file nella cartella predefinita** a meno che non sia necessario scrivere i file di snapshot in entrambe le posizioni.  
  
        > [!NOTE]  
        >  Se questa casella di controllo è selezionata, i file archiviati nella cartella predefinita non vengono compressi. I file compressi possono essere archiviati solo nel percorso alternativo specificato nel passaggio precedente.  
  
2.  Selezionare **Comprimi i file di snapshot in questa cartella**.    
3.  Selezionare **OK**.   

### <a name="use-transact-sql"></a>Usare Transact-SQL

Quando [si configurano le proprietà dello snapshot](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), specificare il valore **compress_snapshot** come **True**. 

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Eseguire gli script prima e dopo l'applicazione dello snapshot
È possibile specificare gli script da eseguire nel Sottoscrittore prima o dopo l'applicazione dello snapshot. È possibile utilizzare script per diversi scopi, ad esempio per creare account di accesso e schemi (proprietari di oggetti) in ogni Sottoscrittore.  
  
 Dopo avere specificato un percorso per ogni script, l'agente snapshot copia i file script nella cartella snapshot corrente ogni volta che viene eseguita l'elaborazione dello snapshot. Quando si applica uno snapshot, l'agente di distribuzione o l'agente di merge esegue lo script pre-snapshot prima di qualsiasi script degli oggetti replicati. L'agente di distribuzione o l'agente di merge esegue lo script post-snapshot dopo l'applicazione di tutti gli altri script degli oggetti replicati e dei dati. Al termine dell'applicazione dello snapshot e dell'esecuzione corretta dei file script, gli script vengono rimossi dalla directory di lavoro del Sottoscrittore.  
  
 Lo script viene eseguito avviando l'utilità **sqlcmd** . Prima di distribuire uno script, eseguirlo con **sqlcmd** per verificarne la corretta esecuzione in base a quanto previsto. È necessario che il contenuto degli script eseguiti prima e dopo l'applicazione dello snapshot sia ripetibile. Se, ad esempio, si crea una tabella nello script, è innanzitutto necessario verificarne l'esistenza e, in tal caso, eseguire le azioni appropriate. Lo script deve essere ripetibile perché, se è necessario reinizializzare una sottoscrizione per cui lo script è già stato applicato, lo script viene applicato nuovamente in corrispondenza dell'applicazione del nuovo snapshot in fase di reinizializzazione.  
  
 Se il file di snapshot viene compresso in formato [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB, vengono compressi e inclusi nel file CAB anche gli script. Dopo il trasferimento e la decompressione del file di snapshot compresso in una directory di lavoro nel Sottoscrittore, vengono eseguiti tutti gli script indicati come pre-snapshot. In modo analogo, tutti gli script post-snapshot vengono decompressi ed eseguiti nel Sottoscrittore come ultimo passaggio dell'applicazione dello snapshot.  

### <a name="execute-a-script"></a>Eseguire uno script 

1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Publication>** :    
    -   Per specificare uno script da eseguire prima dell'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso per lo script nella casella di testo **Prima di applicare lo snapshot, esegui lo script seguente** .  
  
        > [!NOTE]  
        >  È necessario che l'agente di distribuzione o l'agente di merge disponga delle autorizzazioni di lettura per la directory specificata. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\script\scriptpersonali.sql.  
  
    -   Per specificare uno script da eseguire dopo l'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso UNC per lo script nella casella di testo **Dopo l'applicazione dello snapshot, esegui lo script seguente** .   
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  


## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Trasferimento uno snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)   
 [Configurare le proprietà dello snapshot &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)     
  
  
