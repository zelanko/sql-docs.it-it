---
title: Modificare le opzioni di inizializzazione dello snapshot per la replica di SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a611de458537156740521dae8b732eed3e2653c
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289479"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificare le opzioni di inizializzazione dello snapshot per la replica di SQL

Questo articolo illustra come modificare diverse opzioni durante l' [inizializzazione di una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md).

## <a name="snapshot-format"></a>Formato snapshot
  Specificare il formato dello snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  

1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** selezionare **Formato nativo di SQL Server: tutti i Sottoscrittori devono essere server che eseguono SQL Server** oppure **Carattere: obbligatorio se in un server di pubblicazione o in un Sottoscrittore non è in esecuzione SQL Server**. 

    > [!NOTE]  
    >  È consigliabile selezionare il formato nativo a meno che la pubblicazione non debba supportare sottoscrizioni a un database di [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o a un database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>Percorsi cartella snapshot

### <a name="default-snapshot-location"></a>Posizione predefinita degli snapshot
Specificare la posizione predefinita degli snapshot (SQL Server Management Studio) specificare la posizione predefinita degli snapshot nella pagina **cartella snapshot** della configurazione guidata distribuzione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md). Se si crea una pubblicazione su un server non configurato come server di distribuzione, specificare una posizione predefinita degli snapshot nella pagina **Cartella snapshot** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso di questa procedura guidata, vedere [Creare una pubblicazione](publish/create-a-publication.md).  
  
 Modificare la posizione predefinita degli snapshot nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** . Per altre informazioni, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md). Impostare la cartella snapshot per ogni pubblicazione nella finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione**. Per altre informazioni, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
#### <a name="modify-the-default-snapshot-location"></a>Modificare la posizione predefinita degli snapshot  
  
1.  Nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà database di distribuzione - \<DatabaseDistribuzione>** fare clic sul pulsante delle proprietà ( **...** ) per il server di pubblicazione di cui si vuole modificare la posizione predefinita degli snapshot.    
2.  Nella finestra di dialogo **Proprietà server di pubblicazione - \<Server di pubblicazione>** immettere un valore per la proprietà **Cartella snapshot predefinita**.

    > [!NOTE]  
    >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>Posizione alternativa snapshot
  Specificare un percorso alternativo per lo snapshot nella pagina **snapshot** della finestra di dialogo **proprietà pubblicazione \<->pubblicazione** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md). 

  
#### <a name="specify-an-alternate-snapshot-location"></a>Specificare un percorso alternativo per lo snapshot  
  
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** :    
    1.  Selezionare **Inserisci i file nella cartella seguente**e quindi fare clic su **Sfoglia** per passare a una directory oppure immettere il percorso della directory in cui devono essere archiviati i file di snapshot.    

        > [!NOTE]  
        >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).    
    a.  Deselezionare **Inserisci i file nella cartella predefinita** a meno che non sia necessario scrivere i file di snapshot in entrambe le posizioni.    
     Per comprimere i file di snapshot, selezionare **Comprimi i file di snapshot in questa cartella**. La compressione viene in genere utilizzata per le connessioni a larghezza di banda ridotta e per i percorsi alternativi per lo snapshot nei supporti rimovibili, ad esempio un CD-ROM.    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>Comprimi file di snapshot
Specificare che i file devono essere compressi nella pagina **snapshot** della finestra di dialogo **proprietà \<pubblicazione->pubblicazione** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** :  
  
    1.  Selezionare **Inserisci i file nella cartella seguente**e quindi fare clic su **Sfoglia** per passare a una directory oppure immettere il percorso della directory in cui devono essere archiviati i file di snapshot.    
        > [!NOTE]  
        >  L'agente snapshot deve disporre delle autorizzazioni di scrittura per la directory specificata, mentre l'agente di distribuzione o l'agente di merge deve disporre delle autorizzazioni di lettura. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\snapshot. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).  
  
    2.  Deselezionare **Inserisci i file nella cartella predefinita** a meno che non sia necessario scrivere i file di snapshot in entrambe le posizioni.    
        > [!NOTE]  
        >  Se questa casella di controllo è selezionata, i file archiviati nella cartella predefinita non vengono compressi. I file compressi possono essere archiviati solo nel percorso alternativo specificato nel passaggio precedente.    
2.  Selezionare **Comprimi i file di snapshot in questa cartella**.    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Eseguire gli script prima e dopo l'applicazione dello snapshot

 È possibile specificare gli script da eseguire nel Sottoscrittore prima o dopo l'applicazione dello snapshot. È possibile utilizzare script per diversi scopi, ad esempio per creare account di accesso e schemi (proprietari di oggetti) in ogni Sottoscrittore.  
  
 Dopo avere specificato un percorso per ogni script, l'agente snapshot copia i file script nella cartella snapshot corrente ogni volta che viene eseguita l'elaborazione dello snapshot. Quando si applica uno snapshot, l'agente di distribuzione o l'agente di merge esegue lo script pre-snapshot prima di qualsiasi script degli oggetti replicati. L'agente di distribuzione o l'agente di merge esegue lo script post-snapshot dopo l'applicazione di tutti gli altri script degli oggetti replicati e dei dati. Al termine dell'applicazione dello snapshot e dell'esecuzione corretta dei file script, gli script vengono rimossi dalla directory di lavoro del Sottoscrittore.  
  
 Lo script viene eseguito avviando l'utilità **sqlcmd** . Prima di distribuire uno script, eseguirlo con **sqlcmd** per verificarne la corretta esecuzione in base a quanto previsto. È necessario che il contenuto degli script eseguiti prima e dopo l'applicazione dello snapshot sia ripetibile. Se, ad esempio, si crea una tabella nello script, è innanzitutto necessario verificarne l'esistenza e, in tal caso, eseguire le azioni appropriate. Lo script deve essere ripetibile perché, se è necessario reinizializzare una sottoscrizione per cui lo script è già stato applicato, lo script viene applicato nuovamente in corrispondenza dell'applicazione del nuovo snapshot in fase di reinizializzazione.  
  
 Se il file di snapshot viene compresso in formato [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB, vengono compressi e inclusi nel file CAB anche gli script. Dopo il trasferimento e la decompressione del file di snapshot compresso in una directory di lavoro nel Sottoscrittore, vengono eseguiti tutti gli script indicati come pre-snapshot. In modo analogo, tutti gli script post-snapshot vengono decompressi ed eseguiti nel Sottoscrittore come ultimo passaggio dell'applicazione dello snapshot.  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>Eseguire uno script prima o dopo l'applicazione di uno snapshot  
 Specificare uno script facoltativo da eseguire prima o dopo l'applicazione dello snapshot nella pagina **snapshot** della finestra di dialogo **proprietà pubblicazione \<->pubblicazione** . Per ulteriori informazioni sull'accesso a questa finestra di dialogo, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  


1.  Nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** :    
    -   Per specificare uno script da eseguire prima dell'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso per lo script nella casella di testo **Prima di applicare lo snapshot, esegui lo script seguente** . 
   
        > [!NOTE]  
        >  È necessario che l'agente di distribuzione o l'agente di merge disponga delle autorizzazioni di lettura per la directory specificata. Se si usano sottoscrizioni pull, è necessario specificare una directory condivisa come percorso UNC (Universal Naming Convention), ad esempio \\\nomecomputer\script\scriptpersonali.sql.    
    -   Per specificare uno script da eseguire dopo l'applicazione dello snapshot, fare clic su **Sfoglia** per passare allo script oppure immettere un percorso UNC per lo script nella casella di testo **Dopo l'applicazione dello snapshot, esegui lo script seguente** .    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
