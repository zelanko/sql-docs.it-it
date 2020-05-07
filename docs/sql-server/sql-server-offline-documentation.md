---
title: Installare versioni precedenti della documentazione offline di SQL Server
description: Informazioni su come installare la documentazione offline per SQL Server 2019, 2017, 2016, 2014 e 2012. Usare SQL Server Management Studio (SSMS) per visualizzare il contenuto offline.
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.date: 04/20/2020
ms.openlocfilehash: 1420e18fbf335e22d44bf78d526ab35c8b1434e5
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087871"
---
# <a name="install-previous-versions-of-sql-server-documentation-to-view-offline-in-ssms"></a>Installare versioni precedenti della documentazione di SQL Server da visualizzare offline in SSMS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come scaricare e visualizzare offline il contenuto di SQL Server in [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md). Il contenuto offline consente di accedere alla documentazione senza una connessione a Internet, nonostante questa sia inizialmente necessaria per scaricare il contenuto.

La documentazione offline è disponibile per diverse versioni precedenti di SQL Server. Sebbene sia anche possibile [visualizzare il contenuto per le versioni precedenti online](https://docs.microsoft.com/previous-versions/sql/), l'opzione offline costituisce un modo più pratico per accedere al contenuto meno recente.

## <a name="how-to-download-and-configure-offline-content"></a>Come scaricare e configurare il contenuto offline

È possibile scaricare e installare i pacchetti della Guida di SQL Server da origini online o da un disco locale. Le sezioni seguenti illustrano come caricare contenuto offline per varie versioni di SQL Server:

- [SQL Server 2019](#sql2019)
- [SQL Server 2017](#sql2017)
- [SQL Server 2016](#sql2016)
- [SQL Server 2014](#sql2014)
- [SQL Server 2012](#sql2012)

## <a name="sql-server-2019"></a><a id="sql2019"></a> SQL Server 2019

Usare la procedura seguente per caricare la documentazione offline per SQL Server 2019.

1. In SSMS selezionare **Aggiungi e rimuovi contenuto della Guida** nel menu di Help Viewer.

   ![Aggiungi e rimuovi contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.

2. Per trovare il contenuto della Guida più recente per SQL Server 2019, nella scheda **Gestisci contenuto** scegliere **Online** in Origine dell'installazione e digitare *SQL Server 2019* nella barra di ricerca.

   ![Ricerca della documentazione di SQL Server 2019 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-search.png)

   > [!Note]
   > Percorso archivio locale nella scheda Gestisci contenuto indica dove viene installato il contenuto nel computer locale. Per modificare il percorso, selezionare **Sposta**, immettere il percorso di un'altra cartella nel campo **in** e quindi fare clic su **OK**. Se l'installazione della Guida non riesce dopo aver modificato Percorso archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

3. Per installare il contenuto della Guida più recente per SQL Server 2019, selezionare **Aggiungi** accanto a ogni pacchetto di contenuto (documentazione) che si vuole installare e selezionare **Aggiorna** in basso a destra.

   ![Aggiunta e aggiornamento della documentazione di SQL Server 2019 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-add-update.png)

   > [!NOTE]
   > Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

4. È possibile verificare che il contenuto di SQL Server 2019 sia stato caricato cercando *sql server 2019* nel riquadro del contenuto a sinistra.

   ![Documentazione di SQL Server 2019 aggiornata automaticamente](../sql-server/media/sql-server-help-installation/sql-2019-content.png)

## <a name="sql-server-2017"></a><a id="sql2017"></a>SQL Server 2017

Usare la procedura seguente per caricare la documentazione offline per SQL Server 2017.

1. In SSMS selezionare **Aggiungi e rimuovi contenuto della Guida** nel menu di Help Viewer.

   ![Aggiungi e rimuovi contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.

2. Per trovare il contenuto della Guida più recente per SQL Server 2017, nella scheda **Gestisci contenuto** scegliere **Online** in Origine dell'installazione, quindi digitare *SQL Server 2017* nella barra di ricerca.

   ![Ricerca della documentazione di SQL Server 2017 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-search.png)

   > [!Note]
   > Percorso archivio locale nella scheda Gestisci contenuto indica dove viene installato il contenuto nel computer locale. Per modificare il percorso, selezionare **Sposta**, immettere il percorso di un'altra cartella nel campo **in** e quindi fare clic su **OK**. Se l'installazione della Guida non riesce dopo aver modificato Percorso archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

3. Per installare il contenuto della Guida più recente per SQL Server 2017, selezionare **Aggiungi** accanto a ogni pacchetto di contenuto (documentazione) che si vuole installare e selezionare **Aggiorna** in basso a destra.

   ![Aggiunta e aggiornamento della documentazione di SQL Server 2017 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-add-update.png)

   > [!NOTE]
   > Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

4. È possibile verificare che il contenuto di SQL Server 2017 sia stato caricato cercando *sql server 2017* nel riquadro del contenuto a sinistra.

   ![Documentazione di SQL Server 2017 aggiornata automaticamente](../sql-server/media/sql-server-help-installation/sql-2017-content.png)

## <a name="sql-server-2016"></a><a id="sql2016"></a>SQL Server 2016

Usare la procedura seguente per caricare la documentazione offline per SQL Server 2016.

1. In SSMS selezionare **Aggiungi e rimuovi contenuto della Guida** nel menu di Help Viewer.

   ![Aggiungi e rimuovi contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.

2. Per trovare il contenuto della Guida più recente per SQL Server 2016, nella scheda **Gestisci contenuto** scegliere **Online** in Origine dell'installazione, quindi digitare *sql server 2016* nella barra di ricerca.

   ![Ricerca della documentazione di SQL Server 2016 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-search.png)

   > [!Note]
   > Percorso archivio locale nella scheda Gestisci contenuto indica dove viene installato il contenuto nel computer locale. Per modificare il percorso, selezionare **Sposta**, immettere il percorso di un'altra cartella nel campo **in** e quindi fare clic su **OK**. Se l'installazione della Guida non riesce dopo aver modificato Percorso archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

3. Per installare il contenuto della Guida più recente per SQL Server 2016, selezionare **Aggiungi** accanto a ogni pacchetto di contenuto (documentazione) che si vuole installare e selezionare **Aggiorna** in basso a destra.

   ![Aggiunta e aggiornamento della documentazione di SQL Server 2016 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-add-update.png)

   > [!NOTE]
   > Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

4. È possibile verificare che il contenuto di SQL Server 2016 sia stato caricato cercando *sql server 2016* nel riquadro del contenuto a sinistra.

   ![Documentazione di SQL Server 2016 aggiornata automaticamente](../sql-server/media/sql-server-help-installation/sql-2016-content.png)

## <a name="sql-server-2014"></a><a id="sql2014"></a>SQL Server 2014

Usare la procedura seguente per caricare la documentazione offline per SQL Server 2014.

1. Scaricare il contenuto della [documentazione del prodotto per Microsoft SQL Server 2014 per ambienti firewall e proxy con restrizioni](https://www.microsoft.com/download/details.aspx?id=42557) dall'area download e salvarlo in una cartella.

2. Decomprimere il file per visualizzare il file con estensione msha.

   ![File di installazione della documentazione della Guida di SQL Server 2014](../sql-server/media/sql-server-help-installation/sql-2014-help-content-setup-msha.png)

3. In SSMS selezionare **Aggiungi e rimuovi contenuto della Guida** nel menu di Help Viewer.

   ![Aggiungi e rimuovi contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.

4. Per installare il pacchetto di contenuto della Guida più recente, scegliere **Disco** in Origine dell'installazione e selezionare i puntini di sospensione (...).

   ![Origine Disco in Gestisci contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > Percorso archivio locale nella scheda Gestisci contenuto indica dove viene salvato il contenuto nel computer locale. Per modificare il percorso, selezionare **Sposta**, immettere il percorso di un'altra cartella nel campo **in** e quindi fare clic su **OK**.
   Se l'installazione della Guida non riesce dopo aver modificato il percorso dell'archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

5. Individuare la cartella in cui è stato decompresso il contenuto. Selezionare il file **HelpContentSetup.msha** nella cartella e quindi selezionare **Apri**.

   ![Aprire il file del contenuto della Guida per SQL Server 2014 Setup.msha](../sql-server/media/sql-server-help-installation/sql-2014-open-msha.png)

6. Digitare *sql server 2014* nella barra di ricerca. Una volta visualizzato il contenuto della versione 2014 disponibile, selezionare **Aggiungi** accanto a ogni pacchetto di contenuto (documentazione) che si vuole installare in Help Viewer e quindi selezionare **Aggiorna**.

   ![Ricerca della documentazione di SQL Server 2014 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-search.png)

   ![Aggiunta e aggiornamento della documentazione di SQL Server 2014 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-add-update.png)

    > [!NOTE]
    > Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

7. È possibile verificare che il contenuto di SQL Server 2014 sia stato installato cercando *sql server 2014* nel riquadro del contenuto a sinistra.

   ![Documentazione di SQL Server 2014 aggiornata automaticamente](../sql-server/media/sql-server-help-installation/sql-2014-content.png)

## <a name="sql-server-2012"></a><a id="sql2012"></a> SQL Server 2012

Usare la procedura seguente per caricare la documentazione offline per SQL Server 2012.

1. Scaricare il contenuto della [documentazione del prodotto per Microsoft SQL Server 2012 per ambienti firewall e proxy con restrizioni](https://www.microsoft.com/download/details.aspx?id=35750) dall'area download e salvarlo in una cartella.

2. Decomprimere il file per visualizzare il file con estensione msha.

   ![File di installazione del contenuto della Guida di SQL Server 2012](../sql-server/media/sql-server-help-installation/sql-2012-help-content-setup-msha.png)

3. In SSMS selezionare **Aggiungi e rimuovi contenuto della Guida** nel menu di Help Viewer.

   ![Aggiungi e rimuovi contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   Help Viewer si apre con la scheda Gestisci contenuto visualizzata.

4. Per installare il pacchetto di contenuto della Guida più recente, scegliere **Disco** in Origine dell'installazione e selezionare i puntini di sospensione (...).

   ![Origine Disco in Gestisci contenuto in Help Viewer](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > Percorso archivio locale nella scheda Gestisci contenuto indica dove viene salvato il contenuto nel computer locale. Per modificare il percorso, selezionare **Sposta**, immettere il percorso di un'altra cartella nel campo **in** e quindi fare clic su **OK**.
   Se l'installazione della Guida non riesce dopo aver modificato il percorso dell'archivio locale, chiudere e riaprire Help Viewer. Verificare che la nuova posizione venga visualizzata nel percorso dell'archivio locale e tentare nuovamente l'installazione.

5. Individuare la cartella in cui è stato decompresso il contenuto. Selezionare il file **HelpContentSetup.msha** nella cartella e quindi selezionare **Apri**.

   ![Aprire il file del contenuto della Guida per SQL Server 2012 Setup.msha](../sql-server/media/sql-server-help-installation/sql-2012-open-msha.png)

6. Digitare *sql server 2012* nella barra di ricerca. Una volta visualizzato il contenuto della versione 2012 disponibile, selezionare **Aggiungi** accanto a ogni pacchetto di contenuto (documentazione) che si vuole installare in Help Viewer e quindi selezionare **Aggiorna**.

   ![Ricerca della documentazione di SQL Server 2012 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-search.png)

   ![Aggiunta e aggiornamento della documentazione di SQL Server 2012 in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-add-update.png)

    > [!NOTE]
    > Se Help Viewer si blocca mentre aggiunge il contenuto, modificare la riga Cache LastRefreshed="\<mm/gg/aaaa> 00:00:00" nel file %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings usando una data futura. Per altre informazioni su questo problema, vedere [Il visualizzatore della Guida di Visual Studio si blocca](/visualstudio/welcome-to-visual-studio).

7. È possibile verificare che il contenuto di SQL Server 2012 sia stato caricato cercando *sql server 2012* nel riquadro del contenuto a sinistra.

   ![Documentazione di SQL Server 2012 aggiornata automaticamente](../sql-server/media/sql-server-help-installation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>Visualizzare la documentazione offline

È possibile visualizzare il contenuto della Guida di SQL Server usando il menu **Guida** nella versione più recente di [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md).

### <a name="view-offline-help-content-in-ssms"></a>Visualizzare il contenuto della Guida offline in SSMS

Per visualizzare la Guida installata in SSMS, selezionare **Avvia in Help Viewer** dal menu Guida per avviare Help Viewer.

   ![Avvia in Help Viewer](../sql-server/media/sql-server-help-installation/helpviewer-view-offline.png)  

Help Viewer si apre con la scheda Gestisci contenuto visualizzata, con il sommario della Guida installata riportato nel riquadro a sinistra. Selezionare gli articoli nel sommario per visualizzarli nel riquadro a destra.

> [!TIP]
> Se il riquadro del contenuto non è visibile, selezionare Contenuto sul margine sinistro. Selezionare l'icona a forma di puntina da disegno per mantenere aperto il riquadro del contenuto.  

   ![Help Viewer con contenuto](../sql-server/media/sql-server-help-installation/view-offline-all.png)

## <a name="life-cycle-policy"></a>Criteri del ciclo di vita

Esaminare il ciclo di vita del prodotto Microsoft per informazioni sul supporto di un prodotto, un servizio o una tecnologia specifici:

- [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sul contenuto archiviato e su Help Viewer, fare riferimento ai collegamenti seguenti.

- [Collegamento diretto alle versioni precedenti della documentazione di SQL Server](https://docs.microsoft.com/previous-versions/sql/)
- [Microsoft Help Viewer: Visual Studio](https://docs.microsoft.com/visualstudio/help-viewer/overview)
- [Documentazione di SQL Server, avvio](../sql-server/index.yml?view=sql-server-2016)
- [Sistema di versioni per la documentazione SQL](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)