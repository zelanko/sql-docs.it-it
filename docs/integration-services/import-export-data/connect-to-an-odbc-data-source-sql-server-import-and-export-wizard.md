---
title: Connettersi a un'origine dati ODBC (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd4dbec9e08b19a0c06c991a7007b449dff02485
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285496"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Connettersi a un'origine dati ODBC (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **ODBC** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server.

Può essere necessario scaricare il driver ODBC da Microsoft o da terze parti.

Può essere necessario anche cercare le informazioni di connessione che devono essere specificate. Il sito di terze parti [The Connection Strings Reference](https://www.connectionstrings.com/) (Riferimenti alle stringhe di connessione) contiene stringhe di connessione di esempio e altre informazioni sui provider di dati e sulle informazioni di connessione richieste dai provider.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Verificare che il driver desiderato sia installato
1.  Cercare o passare all'applet **Origini dati ODBC (64 bit)** nel Pannello di controllo. Se si ha solo un driver a 32 bit o è necessario usare un driver a 32 bit, cercare o passare a **Origini dati ODBC (32 bit)** .
2.  Avviare l'applet. Viene visualizzata la finestra **Amministrazione origine dati ODBC**.
3.  Nella scheda **Driver** è disponibile un elenco di tutti i driver ODBC installati nel computer. È possibile che i nomi di alcuni driver siano visualizzati in più lingue.

    Di seguito è riportato un esempio dell'elenco di driver a 64 bit installati.

    ![Driver ODBC a 64 bit installati](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Se il driver è installato ma non viene visualizzato nell'applet a 64-bit, cercarlo nell'applet a 32 bit. Queste informazioni indicano anche se eseguire l'Importazione/Esportazione guidata SQL Server a 64 bit o a 32 bit.
>
> Per usare la versione a 64 bit dell'Importazione/Esportazione guidata SQL Server, è necessario installare SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) sono applicazioni a 32 bit e installano solo i file a 32 bit, inclusa la versione a 32 bit della procedura guidata.
    
## <a name="step-1---select-the-data-source"></a>Passaggio 1 - Selezionare l'origine dati
I driver ODBC installati nel computer non sono presenti nell'elenco a discesa delle origini dati. Per connettersi con un driver ODBC, selezionare innanzitutto **Provider di dati .NET Framework per ODBC** come origine dati nella pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata. Questo provider funge da wrapper per il driver ODBC.

Di seguito è riportata la schermata generica che viene visualizzata dopo aver selezionato il Provider di dati .NET Framework per ODBC.

![Connettersi a SQL con ODBC (prima)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Passaggio 2 - Specificare le informazioni di connessione
Nel passaggio successivo vengono specificate le informazioni di connessione per il driver ODBC e l'origine dati. Sono disponibili due opzioni.
1.  Specificare un **DSN** (nome dell'origine dati) già esistente o creato con l'applet **Amministrazione origine dati ODBC** nel Pannello di controllo. Il DSN è l'insieme di impostazioni salvate necessarie per connettersi a un'origine dati ODBC.

    Se si conosce il nome DSN o si sa come creare un nuovo DSN, è possibile ignorare la parte rimanente di questa pagina. Immettere il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**, quindi procedere con il passaggio successivo della procedura guidata.

    [Specificare un DSN](#odbc_dsn)
    
2.  Specificare una **stringa di connessione** che è possibile cercare online o creare e testare nel computer con l'applet **Amministrazione origine dati ODBC**.

    Se la stringa di connessione è già stata specificata o si conosce già la procedura per creare la stringa, è possibile ignorare la parte rimanente della pagina. Immettere la stringa di connessione nel campo **ConnectionString** nella pagina **Scelta origine dati** o **Scelta destinazione**, quindi procedere con il passaggio successivo della procedura guidata.

    [Specificare una stringa di connessione](#odbc_connstring)

Se si specifica una stringa di connessione, la pagina **Scelta origine dati** o **Scelta destinazione** visualizza tutte le informazioni di connessione che verranno usate dalla procedura guidata per la connessione all'origine dati, ad esempio il nome del server e del database e il metodo di autenticazione. Se si specifica un DSN, queste informazioni non sono visibili.

## <a name="odbc_dsn"></a> Opzione 1 - Specificare un DSN
Se si vuole specificare le informazioni di connessione con un DSN (nome dell'origine dati), usare l'applet **Amministrazione origine dati ODBC** per trovare il nome del DSN esistente o creare un nuovo DSN.
1.  Cercare o passare all'applet **Origini dati ODBC (64 bit)** nel Pannello di controllo. Se si ha solo un driver a 32 bit o è necessario usare un driver a 32 bit, cercare o passare a **Origini dati ODBC (32 bit)** .
2.  Avviare l'applet. Viene visualizzata la finestra **Amministrazione origine dati ODBC**. L'applet ha l'aspetto seguente.

    ![Applet del Pannello di controllo Amministrazione origine dati ODBC](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Se si vuole **usare un DSN esistente** per l'origine dati, è possibile usare qualsiasi DSN visualizzato nella scheda **DSN utente**, **DSN di sistema** o **DSN su file**. Selezionare il nome, quindi tornare alla procedura guidata e immetterlo nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Ignorare la parte rimanente della pagina e procedere con il passaggio successivo della procedura guidata.
4.  Se si vuole **creare un nuovo DSN**, decidere se il DSN deve essere visibile solo all'utente (DSN utente), visibile a tutti gli utenti del computer inclusi i servizi Windows (DSN di sistema) o salvato in un file (DSN su file). L'esempio seguente crea un nuovo DSN di sistema.
5. Nella scheda **DSN di sistema** fare clic su **Aggiungi**.

    ![Aggiungere un nuovo DSN di sistema ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  Nella finestra di dialogo **Crea nuova origine dati** selezionare il driver per l'origine dati, quindi fare clic su **Fine**.

    ![Selezionare il driver per nuovo DSN di sistema](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. Il driver visualizzerà una o più schermate specifiche del driver in cui immettere le informazioni necessarie per la connessione all'origine dati. Per il driver SQL Server, ad esempio, vengono visualizzate quattro pagine di impostazioni personalizzate. Al termine, il nuovo DSN di sistema apparirà incluso nell'elenco.

    ![Nuovo DSN di sistema nell'elenco](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Tornare alla procedura guidata e immettere il nome DSN nel campo **Dsn** nella pagina **Scelta origine dati** o **Scelta destinazione**. Continuare con il passaggio successivo della procedura guidata.

## <a name="odbc_connstring"></a> Opzione 2 - Specificare una stringa di connessione
Se si vuole specificare le informazioni di connessione con una stringa di connessione, la parte rimanente di questo argomento descrive come ottenere la stringa di connessione necessaria.

L'esempio seguente usa la stringa di connessione seguente che stabilisce la connessione a Microsoft SQL Server.

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

Immettere la stringa di connessione nel campo **ConnectionString** nella pagina **Scelta origine dati** o **Scelta destinazione**. Dopo avere immesso la stringa di connessione, la procedura guidata analizza la stringa e visualizza le singole proprietà e i relativi valori nell'elenco.

Di seguito è riportata la schermata che viene visualizzata dopo aver immesso la stringa di connessione.

![Connettersi a SQL con ODBC (dopo)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> Le opzioni di connessione per il driver ODBC sono le stesse sia nel caso in cui venga configurata l'origine sia nel caso in cui venga configurata la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

## <a name="get-the-connection-string-online"></a>Ottenere la stringa di connessione online
Per trovare stringhe di connessione per il driver ODBC online, vedere [The Connection Strings Reference](https://www.connectionstrings.com/) (Riferimenti alle stringhe di connessione). Questo sito di terze parti contiene stringhe di connessione di esempio e altre informazioni sui provider di dati e sulle informazioni di connessione richieste dai provider.

## <a name="get-the-connection-string-with-an-app"></a>Ottenere la stringa di connessione con un'app
Per compilare e testare la stringa di connessione per il driver ODBC nel computer, è possibile usare l'applet **Amministrazione origine dati ODBC** del Pannello di controllo. Creare un DSN su file per la connessione, quindi copiare le impostazioni del DSN su file per assemblare la stringa di connessione. Questa operazione richiede diversi passaggi, ma offre una stringa di connessione valida.

1.  Cercare o passare all'applet **Origini dati ODBC (64 bit)** nel Pannello di controllo. Se si ha solo un driver a 32 bit o è necessario usare un driver a 32 bit, cercare o passare a **Origini dati ODBC (32 bit)** .
2.  Avviare l'applet. Viene visualizzata la finestra **Amministrazione origine dati ODBC**.
3.  Passare alla scheda **DSN su file** dell'applet. Scegliere **Aggiungi**.

    Per questo esempio, creare un DSN su file anziché un DSN utente o DSN di sistema poiché il DSN su file salva le coppie nome-valore nel formato specifico richiesto per la stringa di connessione.

    ![Aggiungere un nuovo DSN su file ODBC](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  Nella finestra di dialogo **Crea nuova origine dati** selezionare il driver nell'elenco e quindi fare clic su **Avanti**. Questo esempio crea un DSN che contiene gli argomenti della stringa di connessione necessari per la connessione a Microsoft SQL Server.

    ![Creare una nuova origine dati ODBC](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Selezionare un percorso e immettere un nome per il nuovo DSN su file e quindi fare clic su **Avanti**. Prendere nota del percorso in cui viene salvato il file per poterlo individuare e aprire nei passaggi successivi.

    ![Salvare un nuovo DSN su file](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Esaminare il riepilogo delle selezioni e quindi fare clic su **Fine**.

7.  Dopo aver fatto clic su **Fine**, il driver selezionato visualizza una o più schermate proprietarie per raccogliere le informazioni necessarie per la connessione. In genere queste informazioni includono server, informazioni di accesso e database per le origini dati basate su server e file, formato e versione per le origini dati basate su file.

8. Dopo aver configurato l'origine dati e fatto clic su **Fine**, viene visualizzato un riepilogo delle selezioni che è possibile testare.

    ![Testare un nuovo DSN su file](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Dopo aver testato l'origine dati e aver chiuso le finestre di dialogo, trovare il DSN su file nel percorso in cui è stato salvato nel file system. Se l'estensione del file non è stata modificata, l'estensione predefinita è DSN.

10. Aprire il file salvato con Blocco note o un altro editor di testo. Di seguito è riportato il contenuto dell'esempio SQL Server.

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. Copiare e incollare i valori necessari in una stringa di connessione in cui le coppie nome-valore sono separate da punti e virgola.

    Dopo aver assemblato i valori necessari del DSN su file di esempio, la stringa di connessione è la seguente.
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    Per creare una stringa di connessione valida non sono in genere necessarie tutte le impostazioni di un DSN creato da Amministrazione origine dati ODBC.  
    -   È sempre necessario specificare il driver ODBC.
    -   Per un'origine dati basata su server come SQL Server, è necessario specificare il server, il database e le informazioni di accesso. Di conseguenza, nel DSN di esempio non è necessario TrustServerCertificate, WSID o APP.
    -   Per un'origine dati basata su file, è necessario specificare almeno il nome del file e il percorso.
    
12. Incollare la stringa di connessione nel campo **ConnectionString** nella pagina **Scelta origine dati** o **Scelta destinazione** della procedura guidata. La procedura guidata analizza la stringa ed è possibile continuare.

    ![Connettersi a SQL con ODBC (dopo)](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scelta destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


