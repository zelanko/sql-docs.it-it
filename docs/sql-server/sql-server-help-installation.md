---
title: Contenuto della Guida e Help Viewer per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1352a7f469e72100f7a2e0573c87cbb8422fe413
ms.sourcegitcommit: 92b2e3cf058e6b1e9484e155d2cc28ed2a0b7a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2020
ms.locfileid: "77608483"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Guida offline di SQL Server e Help Viewer

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È possibile usare Microsoft Help Viewer per scaricare e installare i pacchetti della Guida di SQL Server da origini online o da un disco locale. È quindi possibile visualizzare il contenuto non in linea. Help Viewer viene installato con diversi strumenti. Questo articolo descrive gli strumenti che consentono di installare Help Viewer e spiega come installare il contenuto della Guida offline e come visualizzare la Guida.

Per scaricare il contenuto di Help Viewer è necessario l'accesso a Internet. Successivamente si potrà trasferire il contenuto in un computer senza accesso a Internet.

>[!NOTE]
> Per ottenere il contenuto locale per le versioni correnti di SQL Server, installare la versione corrente di SQL Server Management Studio [SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="what-tools-install-the-help-viewer-versions"></a>Strumenti per l'installazione di Help Viewer

Esistono due versioni principali di Microsoft Help Viewer,  le versioni 1.x e 2.x. Ogni versione supporta versioni diverse del contenuto di SQL Server.  Il formato della documentazione offline è cambiato nel tempo e le versioni più vecchie di Help Viewer non supportano le versioni più recenti della documentazione.

|**Set di contenuti**|**Strumenti che installano Help Viewer**|**Versione di Help Viewer**|
|-|-|-|
|SQL Server 2019 <br><br><br>SQL Server 2017 <br>SQL Server 2016 | [Visual Studio 2019 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019) <br>[SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) <br><br>[Visual Studio 2017 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017) <br>[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/release-notes-ssms?view=sql-server-2017#1791) <br>[SQL Server Data Tools per Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) <br>Visual Studio 2015 | v2.3 <br><br><br>v2.2 |
|SQL Server 2014<br>SQL Server 2012|Installazione di SQL Server 2016 (\*2)<br>SQL Server 2014 Management Studio<br>Installazione di SQL Server 2014 (\*2)<br>SQL Server Management Studio 2012<br>Installazione di SQL Server 2012 (\*2)| v1.x|
| | | |

(\*1) Per installare Help Viewer con Visual Studio 2019 o 2017, nella scheda **Singoli componenti** nel Programma di installazione di Visual Studio selezionare **Strumenti per il codice** \> **Help Viewer** \> **Installa**.

(\*2) Indica l'opzione **Componenti della documentazione** nel programma di installazione di SQL Server.

>[!NOTE]
> - SQL Server 2016 installa Help Viewer 1.1, che non supporta la Guida di SQL Server 2016. Per visualizzare il contenuto di SQL Server 2016 è necessaria la versione v2.x di Help Viewer. Per altre informazioni, vedere le [Note sulla versione di SQL Server 2016](sql-server-2016-release-notes.md).
> - Help Viewer 2.x consente di visualizzare la documentazione di SQL Server versioni 2014-2019.
> - Per ottenere Help Viewer 2.3 o versioni successive in modo semplice, è possibile scaricare prima di tutto la versione gratuita più recente di `SSMS.exe`. Quindi usare il menu della **Guida** di SSMS.
> - A partire da SQL Server 2017, Help Viewer non può essere installato dal programma di installazione di SQL Server.

## <a name="use-help-viewer-v2x"></a>Usare Help Viewer v2.x

Per questo approccio, è consigliabile usare Help Viewer 2.3 o versione successiva. Il menu della **Guida** nella [versione più recente di SSMS.exe](../ssms/download-sql-server-management-studio-ssms.md) offre la versione 2.3 o versione successiva.

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v2x"></a>Per scaricare e installare il contenuto della Guida offline con Help Viewer v2.x

1. In SQL Server Management Studio o Visual Studio fare clic su **Aggiungi e rimuovi contenuto della Guida** nel menu ?. 

   ![Aggiungere rimuovere contenuto con HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.  
   
2. Per installare il pacchetto di contenuto della Guida più recente, scegliere **Online** come origine dell'installazione.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Per eseguire l'installazione dal disco (Guida di SQL Server 2014), scegliere **Disco** come origine dell'installazione e specificare il percorso del disco.
   
   Il percorso dell'archivio locale nella scheda Gestisci contenuto indica dove verrà installato il contenuto nel computer locale. Per modificare il percorso, fare clic su **Sposta**, immettere il percorso di un'altra cartella nel campo **A** e quindi fare clic su **OK**.
   Se l'installazione della Guida non riesce dopo aver modificato il percorso dell'archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

3. Fare clic su **Aggiungi** accanto a ogni pacchetto di contenuto (libro) da installare. 
   Per installare tutto il contenuto della Guida di SQL Server, aggiungere tutti i 13 libri in SQL Server. 
   
4. Fare clic su **Aggiorna** in basso a destra. 
   Il sommario della Guida a sinistra si aggiorna automaticamente con i libri aggiunti. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> Non tutti i titoli del nodo superiore nel sommario di SQL Server corrispondono esattamente ai nomi dei libri della Guida scaricabili corrispondenti. I titoli del sommario sono associati ai nomi dei libri come indicato di seguito:

(*) Contenuto della prima versione disponibile a livello generale del contenuto di SQL Server 2017 insieme a contenuto meno recente della versione 2016. Questi libri verranno rimossi poiché i libri distinti e completi per SQL Server 2016 e 2017 contengono modifiche del contenuto a partire da gennaio 2019.  

| | Riquadro del contenuto | Libro di SQL Server |
|-----|-----|-----|
|*|Guida di riferimento al linguaggio di Analysis Services | Guida di riferimento al linguaggio di Analysis Services (MDX)|
|*|Guida di riferimento a Data Analysis Expressions (DAX) | Guida di riferimento a Data Analysis Expressions (DAX)|
|*|Guida di riferimento a DMX (Data Mining Extensions) | Guida di riferimento a DMX (Data Mining Extensions)|
|*|Introduzione al Machine Learning in SQL Server | Microsoft Machine Learning Services|
|*|Riferimento M di Power Query | Riferimento M di Power Query|
||Documentazione di SQL Server 2016 | Documentazione di SQL Server 2016|
||Documentazione di SQL Server 2017| Documentazione di SQL Server 2017|
|*|Guide per sviluppatori per SQL Server | Guida di riferimento per sviluppatori per SQL Server|
|*|Scaricare SQL Server Management Studio | SQL Server Management Studio|
|*|Home page per la programmazione client per Microsoft SQL Server | Driver di connessione SQL Server|
|*|SQL Server in Linux | SQL Server in Linux|
|*|Documentazione tecnica di SQL Server | Documentazione tecnica di SQL Server (SSIS, SSRS, motore di database, installazione)|
|*|Strumenti e utilità per database SQL di Azure | Strumenti di SQL Server|
|*|Guida di riferimento a Transact-SQL (Motore di database) | Riferimento all'istruzione Transact-SQL|
|*|Riferimento al linguaggio XQuery (SQL Server) | Riferimento al linguaggio XQuery (SQL Server)|
| &nbsp; | &nbsp; | &nbsp; |

> [!NOTE]
> Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

### <a name="to-view-offline-help-content-in-ssms-with-help-viewer-v2x"></a>Per visualizzare il contenuto della Guida offline in SSMS con Help Viewer v2.x

Per visualizzare la Guida installata in SQL Server Management Studio, premere CTRL + ALT + F1 oppure scegliere **Aggiungi o rimuovi contenuto** dal menu ? per avviare Help Viewer. 

   ![Aggiungere rimuovere contenuto con HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

Help Viewer si apre con la scheda Gestisci contenuto visualizzata, con il sommario della Guida installata riportato nel riquadro a sinistra. Fare clic sugli articoli nel sommario per visualizzarli nel riquadro a destra.
> [!TIP]
> Se il riquadro del contenuto non è visibile, fare clic su Contenuto sul margine sinistro. Fare clic sulla puntina da disegno per mantenere aperto il riquadro del contenuto.  

   ![Help Viewer v2.x con contenuto](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

### <a name="to-view-offline-help-content-in-vs-with-help-viewer-v2x"></a>Per visualizzare il contenuto della Guida offline in VS con Help Viewer v2.x

Per visualizzare la Guida installata in Visual Studio:
1. Selezionare **Imposta preferenza Guida** dal menu ? e scegliere **Avvia in Help Viewer**. 

   ![Avvio Help Viewer da Imposta preferenza Guida per la Guida di VS](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Fare clic su **Visualizza Guida** nel menu ? per visualizzare il contenuto in Help Viewer. 

   ![Visualizza Guida](../sql-server/media/sql-server-help-installation/viewhelp.png)

   Il sommario della Guida viene visualizzato sulla sinistra e l'articolo della Guida selezionato a destra.
  
## <a name="use-help-viewer-v1x"></a>Usare Help Viewer v1.x

In questa sezione vengono eseguiti i passaggi generali seguenti:

- Scaricare manualmente la documentazione offline di SQL Server 2014, suddivisa in quattro parti.
- Usare il menu della **Guida** di SSMS o VS per avviare Help Viewer.
- Infine, specificare in Help Viewer la posizione del file `*.msha` di SQL Server 2014 nel disco rigido locale.

Le versioni precedenti di SSMS e VS offrivano le versioni 1.x di Help Viewer. La versione 1.x consente di visualizzare la documentazione offline di SQL Server versioni 2012 e 2014. La versione 1.x, tuttavia, non consente di visualizzare la documentazione offline di SQL Server 2016 o versioni successive.

Help Viewer 2.3 consente anche di visualizzare la documentazione offline di SQL Server 2014, dopo averla scaricata nel disco rigido locale.

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v1x"></a>Per scaricare e installare il contenuto della Guida offline con Help Viewer v1.x

Questa procedura usa Help Viewer 1.x per scaricare la Guida di SQL Server 2014 da Microsoft Download Center e installarla nel computer in uso.

1. Passare al sito di download della [documentazione del prodotto per Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42557) e fare clic su **Scarica**.

2. Fare clic su **Salva** nella finestra del messaggio per salvare il file *SQLServer2014Documentation\_\*.exe* nel computer.

   > [!NOTE]
   > Per ambienti protetti da firewall e proxy, salvare il download in un'unità USB o in un altro supporto portatile che possa essere usato nell'ambiente.

3. Fare doppio clic sul file EXE per decomprimere il file del contenuto della Guida e salvarlo in una cartella locale o condivisa.

4. Aprire **Gestione librerie della Guida** avviando SSMS o VS e scegliendo **Gestione impostazioni della Guida** dal menu ?.

5. Fare clic su **Installa contenuto da disco** e passare alla cartella in cui è stato decompresso il file del contenuto della Guida.

   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)

   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)

   > [!IMPORTANT]
   > Per evitare di installare contenuto della Guida locale, che include solo un sommario parziale, è necessario usare l'opzione **Installa contenuto da disco** in **Gestione librerie della Guida**.  Se si usa l'opzione **Installa contenuto da online** e Help Viewer visualizza un sommario parziale, vedere questo [post di blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/) per i passaggi di risoluzione del problema.

6. Fare clic sul file `HelpContentSetup.msha`, fare clic su **Apri** e quindi su **Avanti**.

7. Fare clic su **Aggiungi** accanto alla documentazione che si vuole installare e quindi su **Aggiorna**.

   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)

8. Fare clic su **Fine**, quindi fare clic su **Esci**.

### <a name="to-view-offline-help-content-with-help-viewer-v1x"></a>Per visualizzare il contenuto della Guida offline con Help Viewer v1.x

1. Per visualizzare la Guida installata, aprire **Gestione librerie della Guida**, fare clic su **Scegliere di utilizzare la Guida online o locale** e quindi scegliere la **Guida locale**.

2. Aprire Help Viewer per visualizzare il contenuto facendo clic su **Visualizza Guida** nel menu **?** . Il contenuto installato è indicato nel riquadro a sinistra.

   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  

## <a name="view-online-help"></a>Visualizzare la Guida online

Nella Guida appare sempre il contenuto più aggiornato. 

### <a name="to-view-sql-server-online-help-in-ssms-17x"></a>Per visualizzare la Guida online di SQL Server in SSMS 17.x

- Fare clic su **Visualizza Guida** nel menu **?** . La documentazione di SQL Server 2016/2017 più recente da [https://docs.microsoft.com/sql/sql-server/](https://docs.microsoft.com/sql/sql-server/) viene visualizzata nel browser.

   ![Visualizza Guida](../sql-server/media/sql-server-help-installation/viewhelp.png)

### <a name="to-view-visual-studio-online-help-in-visual-studio"></a>Per visualizzare la Guida online di Visual Studio in Visual Studio

1. Selezionare **Imposta preferenza Guida** dal menu ? e scegliere **Avvia nel browser** o **Avvia in Help Viewer**. 
2. Fare clic su **Visualizza Guida** nel menu ?. La Guida più recente di Visual Studio viene visualizzata nell'ambiente selezionato. 

**Per visualizzare la Guida online con Help Viewer v1.x**

1. Aprire **Gestione librerie della Guida** scegliendo **Gestione impostazioni della Guida** dal menu ?.  
2. Nella finestra di dialogo Gestione librerie della Guida fare clic su **Scegliere di utilizzare la Guida online o locale**.  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. Fare clic sull'opzione per l'uso della **Guida online**, scegliere **OK** e fare clic su **Esci**.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

4. Aprire Help Viewer per visualizzare il contenuto facendo clic su **Visualizza Guida** nel menu **?** .

## <a name="view-f1-help"></a>Visualizzare la Guida sensibile al contesto

Quando si preme F1 o si fa clic su **Guida** o **?** in una finestra di dialogo in SSMS o VS, nel browser o in Help Viewer viene visualizzato un articolo della Guida online sensibile al contesto.

### <a name="to-view-f1-help"></a>Per visualizzare la Guida in linea (F1)

1. Nel menu della Guida fare clic su **Imposta preferenza Guida** e scegliere **Avvia nel browser** o **Avvia in Help Viewer**.
2. Premere F1 o fare clic su **Guida** oppure fare clic su **?** nelle finestre di dialogo in cui sono disponibili per visualizzare gli articoli online sensibili al contesto nell'ambiente selezionato.

> [!NOTE]
> La Guida sensibile al contesto funziona solo quando si è online. Non esistono origini offline per la Guida sensibile al contesto.

## <a name="systems-without-internet-access"></a>Sistemi senza accesso a Internet
Dopo aver scaricato i libri offline in un sistema con accesso a Internet, è possibile usare la procedura seguente per trasferire il contenuto in un sistema senza accesso a Internet.

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
