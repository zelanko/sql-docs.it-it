---
title: Contenuto della Guida e Help Viewer per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2017
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00db3d0ca027a0f188831281bb2c844b5bc8462d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202450"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Guida offline di SQL Server e Help Viewer

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È possibile usare Help Viewer in SQL Server Management Studio (SSMS) o in Visual Studio (VS) per scaricare e installare i pacchetti della Guida di SQL Server da origini online o da un disco e visualizzarli offline. Questo articolo descrive gli strumenti che consentono di installare Help Viewer e spiega come installare il contenuto della Guida offline e come visualizzare la Guida per [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 e SQL Server 2017.

Dopo aver scaricato il contenuto in un sistema che ha accesso a Internet, è possibile migrare il contenuto in un sistema che non ha accesso a Internet. 

> [!NOTE]
> La Guida di SQL Server 2016 e quella di SQL Server 2017 sono combinate, anche se alcuni argomenti riguardano le singole versioni, dove indicato. La maggior parte degli argomenti sono validi per entrambe.

## <a name="install-the-help-viewer"></a>Installare Help Viewer

Help Viewer è disponibile in due versioni: v2.x, che supporta la Guida di SQL Server 2016/SQL Server 2017 e v1.x, che supporta la Guida di [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]. Il visualizzatore della Guida non supporta impostazioni del proxy né il formato ISO. 

I seguenti strumenti consentono di installare Help Viewer: 

|**Strumento che installa Help Viewer**|**Versione di Help Viewer installata**|
|---------|---------|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)| v2.2|
|[SQL Server Data Tools per Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)| v2.2|
|Visual Studio 2017* | v2.3|
|Visual Studio 2015 | v2.2|
|SQL Server 2014 Management Studio | v1.x|
|Versioni precedenti di Visual Studio 2008 | v1.x|
|SQL Server 2016 | v1.x|

\* Per installare Help Viewer con Visual Studio 2017 nella scheda Singoli componenti del programma di installazione di Visual Studio selezionare **Help Viewer** in Strumenti per il codice e quindi fare clic su **Installa**. 

>[!NOTE]
> - SQL Server 2016 installa Help Viewer 1.1, che non supporta la Guida di SQL Server 2016. 
> - L'installazione di SQL Server 2017 non installa alcuna versione di Help Viewer.
> - Help Viewer v2.x può inoltre supportare la Guida di [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] se si installa il contenuto dal disco.

## <a name="use-help-viewer-v2x"></a>Usare Help Viewer v2.x

SSMS 17.x e VS 2015 e 2017 usano Help Viewer 2.x, che supporta ala Guida di SQL Server 2016/2017. 

**Per scaricare e installare il contenuto della Guida offline con Help Viewer v2.x**

1. In SQL Server Management Studio o Visual Studio fare clic su **Aggiungi e rimuovi contenuto della Guida** nel menu ?. 

   ![Aggiungere rimuovere contenuto con HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.  
   
2. Per installare il pacchetto di contenuto della Guida più recente, scegliere **Online** come origine dell'installazione.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Per eseguire l'installazione dal disco (Guida di SQL Server 2014), scegliere **Disco** come origine dell'installazione e specificare il percorso del disco.
   
   Il percorso dell'archivio locale nella scheda Gestisci contenuto indica dove verrà installato il contenuto nel computer locale. Per modificare il percorso, fare clic su **Sposta**, immettere un altro percorso di cartella nel campo **A** e quindi fare clic su **OK**.
   Se l'installazione della Guida non riesce dopo aver modificato il percorso dell'archivio locale, chiudere e riaprire Help Viewer, verificare che la nuova posizione appaia nel percorso dell'archivio locale e quindi tentare nuovamente l'installazione.

3. Fare clic su **Aggiungi** accanto a ogni pacchetto di contenuto (libro) da installare. 
   Per installare tutto il contenuto della Guida di SQL Server, aggiungere tutti i 13 libri in SQL Server. 
   
4. Fare clic su **Aggiorna** in basso a destra. 
   Il sommario della Guida a sinistra si aggiorna automaticamente con i libri aggiunti. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> Non tutti i titoli del nodo superiore nel sommario di SQL Server corrispondono esattamente ai nomi dei libri della Guida scaricabili corrispondenti. I titoli del sommario sono associati ai nomi dei libri come indicato di seguito:

| Riquadro del contenuto | Libro di SQL Server |
|-----|-----|
|Guida di riferimento al linguaggio di Analysis Services | Guida di riferimento al linguaggio di Analysis Services (MDX)|
|Guida di riferimento a Data Analysis Expressions (DAX) | Guida di riferimento a Data Analysis Expressions (DAX)|
|Guida di riferimento a DMX (Data Mining Extensions) | Guida di riferimento a DMX (Data Mining Extensions)|
|Guide per sviluppatori per SQL Server | Guida di riferimento per sviluppatori per SQL Server|
|Scaricare SQL Server Management Studio | SQL Server Management Studio|
|Guida introduttiva con machine learning in SQL Server | Microsoft Machine Learning Services|
|Guida di riferimento di Power Query M | Guida di riferimento di Power Query M|
|Driver SQL Server | Driver di connessione SQL Server|
|SQL Server in Linux | SQL Server in Linux|
|Documentazione tecnica di SQL Server | Documentazione tecnica di SQL Server (SSIS, SSRS, motore di database, installazione)|
|Strumenti e utilità per database SQL di Azure | Strumenti di SQL Server|
|Guida di riferimento a Transact-SQL (Motore di database) | Riferimento all'istruzione Transact-SQL|
|Riferimento al linguaggio XQuery (SQL Server) | Riferimento al linguaggio XQuery (SQL Server)|

> [!NOTE]
> Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

**Per visualizzare il contenuto della Guida offline in SSMS con Help Viewer v2.x**

Per visualizzare la Guida installata in SQL Server Management Studio, premere CTRL + ALT + F1 oppure scegliere **Aggiungi o rimuovi contenuto** dal menu ? per avviare Help Viewer. 

   ![Aggiungere rimuovere contenuto con HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

Help Viewer si apre con la scheda Gestisci contenuto visualizzata, con il sommario della Guida installata riportato nel riquadro a sinistra. Fare clic sugli argomenti nel sommario per visualizzarli nel riquadro a destra. 
> [!TIP]
> Se il riquadro del contenuto non è visibile, fare clic su Contenuto sul margine sinistro. Fare clic sulla puntina da disegno per mantenere aperto il riquadro del contenuto.  

   ![Help Viewer v2.x con contenuto](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**Per visualizzare il contenuto della Guida offline in VS con Help Viewer v2.x**

Per visualizzare la Guida installata in Visual Studio:
1. Selezionare **Imposta preferenza Guida** dal menu ? e scegliere **Avvia in Help Viewer**. 

   ![Avvio Help Viewer da Imposta preferenza Guida per la Guida di VS](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Fare clic su **Visualizza Guida** nel menu ? per visualizzare il contenuto in Help Viewer. 

   ![Visualizza Guida](../sql-server/media/sql-server-help-installation/viewhelp.png)

   Il sommario della Guida viene visualizzato sulla sinistra e l'argomento della Guida selezionato a destra. 

  
## <a name="use-help-viewer-v1x"></a>Usare Help Viewer v1.x

Le versioni precedenti di SQL Server Management Studio e Visual Studio usano Help Viewer 1.x, che supporta la Guida di SQL Server 2014. 

**Per scaricare e installare il contenuto della Guida offline con Help Viewer v1.x**

Questa procedura usa Help Viewer 1.x per scaricare la Guida di SQL Server 2014 da Microsoft Download Center e installarla nel computer in uso.

1. Passare al sito di download della [documentazione del prodotto per Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42557) e fare clic su **Scarica**.  
2. Fare clic su **Salva** nella finestra del messaggio per salvare il file *SQLServer2014Documentation\_\*.exe* nel computer.  
   
   >[!NOTE]
   >Per ambienti protetti da firewall e proxy, salvare il download in un'unità USB o in un altro supporto portatile che possa essere usato nell'ambiente.   
   
3. Fare doppio clic sul file EXE per decomprimere il file del contenuto della Guida e salvarlo in una cartella locale o condivisa.  
4. Aprire **Gestione librerie della Guida** avviando SSMS o VS e scegliendo **Gestione impostazioni della Guida** dal menu ?.  
5. Fare clic su **Installa contenuto da disco** e passare alla cartella in cui è stato decompresso il file del contenuto della Guida.  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > Per evitare di installare contenuto della Guida locale, che include solo un sommario parziale, è necessario usare l'opzione **Installa contenuto da disco** in **Gestione librerie della Guida**.  Se si usa l'opzione **Installa contenuto da online** e Help Viewer visualizza un sommario parziale, vedere questo [post di blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) per i passaggi di risoluzione del problema. 
   
8. Selezionare il file HelpContentSetup.msha, fare clic su **Apri** e quindi su **Avanti**.  
9. Fare clic su **Aggiungi** accanto alla documentazione che si vuole installare e quindi su **Aggiorna**.  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. Fare clic su **Fine**, quindi fare clic su **Esci**.

**Per visualizzare il contenuto della Guida offline con Help Viewer v1.x**

11. Per visualizzare la Guida installata, aprire **Gestione librerie della Guida**, fare clic su **Scegliere di utilizzare la Guida online o locale** e quindi scegliere la **Guida locale**.
12. Aprire Help Viewer per visualizzare il contenuto facendo clic su **Visualizza Guida** nel menu **?**. Il contenuto installato è indicato nel riquadro a sinistra.  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   


## <a name="view-online-help"></a>Visualizzare la Guida online

Nella Guida appare sempre il contenuto più aggiornato. 

**Per visualizzare la Guida online di SQL Server in SSMS 17.x**

- Fare clic su **Visualizza Guida** nel menu **?**. La documentazione di SQL Server 2016/2017 più recente da [ https://docs.microsoft.com/sql/ https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation ](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation) viene visualizzata nel browser. 

   ![Visualizza Guida](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Per visualizzare la Guida online di Visual Studio in Visual Studio**

1. Selezionare **Imposta preferenza Guida** dal menu ? e scegliere **Avvia nel browser** o **Avvia in Help Viewer**. 
2. Fare clic su **Visualizza Guida** nel menu ?. La Guida più recente di Visual Studio viene visualizzata nell'ambiente selezionato. 

**Per visualizzare la Guida online con Help Viewer v1.x**

1. Aprire **Gestione librerie della Guida** scegliendo **Gestione impostazioni della Guida** dal menu ?.  
2. Nella finestra di dialogo Gestione librerie della Guida fare clic su **Scegliere di utilizzare la Guida online o locale**.  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. Fare clic sull'opzione per l'uso della **Guida online**, scegliere **OK** e fare clic su **Esci**.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)
   
4. Aprire Help Viewer per visualizzare il contenuto facendo clic su **Visualizza Guida** nel menu **?**. 

## <a name="view-f1-help"></a>Visualizzare la Guida sensibile al contesto

Quando si preme F1 o si fa clic su **Guida** o **?** in una finestra di dialogo in SSMS o VS, nel browser o in Help Viewer viene visualizzato un argomento della Guida online sensibile al contesto. 

**Per visualizzare la Guida sensibile al contesto**

1. Selezionare **Imposta preferenza Guida** dal menu ? e scegliere **Avvia nel browser** o **Avvia in Help Viewer**. 
2. Premere F1 o fare clic su **?** o **Guida** nelle finestre di dialogo in cui sono disponibili per visualizzare gli argomenti online sensibili al contesto nell'ambiente selezionato.

> [!NOTE]
>  La Guida sensibile al contesto funziona solo quando si è online. Non esistono origini offline per la Guida sensibile al contesto. 

## <a name="systems-without-internet-access"></a>Sistemi senza accesso a Internet
Dopo aver eseguito i [passaggi indicati in precedenza](#use-help-viewer-v2x) per scaricare il contenuto offline tramite SQL Server Help Viewer in un sistema che ha accesso a Internet, è possibile migrare il contenuto in un sistema senza accesso a Internet. L'operazione può essere eseguita con la procedura seguente. 

  >[!NOTE]
  >È necessario installare nel sistema offline un software che supporta Help Viewer, ad esempio SQL Server Management Studio. 

1. Aprire Help Viewer (CTRL+ALT+F1).
1. Selezionare la documentazione desiderata. Ad esempio, filtrare per SQL e selezionare la documentazione tecnica di SQL Server. 
1. Identificare il percorso fisico dei file sul disco disponibile in **Percorso archivio locale**.
1. Passare al percorso indicato usando lo strumento di esplorazione del file system. 
    1.  Il percorso predefinito è: `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Extensions\Application`
1. Selezionare le tre cartelle **ContentStore**, **Incoming**, **IndexStore** e copiarle nello stesso percorso nel sistema offline. Potrebbe essere necessario usare un supporto di memorizzazione provvisorio, ad esempio un CD o un'unità USB. 
1. Dopo aver spostato i file, avviare Help Viewer nel sistema offline per rendere disponibile la documentazione tecnica di SQL Server.

![physical-location-of-offline-content.png](media/sql-server-help-installation/physical-location-of-offline-content.png)
   

## <a name="next-steps"></a>Passaggi successivi
[Microsoft Help Viewer: Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
