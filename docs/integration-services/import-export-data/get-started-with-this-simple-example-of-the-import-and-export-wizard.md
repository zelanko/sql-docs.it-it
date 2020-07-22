---
title: Introduzione a un esempio semplice di importazione/esportazione guidata | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 58225c6728915c5b9dcd73937b2bd645bd08950f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86910195"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Introduzione a un esempio semplice di importazione/esportazione guidata

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Informazioni sull'importazione/esportazione guidata SQL Server attraverso uno scenario comune da un foglio di calcolo di Excel a un database SQL Server. Anche se si prevede di usare un'origine diversa e una destinazione diversa, in questo argomento è illustrata la maggior parte delle operazioni da conoscere per l'esecuzione della procedura guidata.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Prerequisito: la procedura guidata è installata nel computer?
Se si vuole eseguire la procedura guidata, ma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è disponibile nel computer, è possibile installare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installando SQL Server Data Tools (SSDT). Per altre informazioni, vedere [Scaricare SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="heres-the-excel-source-data-for-this-example"></a>Di seguito è riportata l'origine dati di Excel per questo esempio
Ecco i dati di origine che si intende copiare - una piccola tabella a due colonne nel foglio di lavoro WizardWalkthrough della cartella di lavoro di WizardWalkthrough.xlsx Excel.

![Origine dati Excel](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Database di destinazione di SQL Server per questo esempio
Di seguito (in SQL Server Management Studio) è riportato il database di destinazione di SQL Server in copiare i dati di origine. La tabella di destinazione non è presente. Consentire alla procedura guidata di creare la tabella per l'utente.

![Database di destinazione SQL Server](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Passaggio 1: Avviare la procedura guidata
Avviare la procedura guidata dal gruppo Microsoft SQL Server 2016 nel menu Start di Windows.

![Avviare la procedura guidata](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> Per questo esempio, è possibile selezionare la procedura guidata a 32 bit dato che la versione di Microsoft Office è la versione a 32 bit. Di conseguenza, è necessario usare il provider di dati a 32 bit per connettersi a Excel. Per molte altre origini dati, in genere è possibile selezionare la procedura guidata a 64 bit.
>
> Per usare la versione a 64 bit dell'Importazione/Esportazione guidata SQL Server, è necessario installare SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) sono applicazioni a 32 bit e installano solo i file a 32 bit, inclusa la versione a 32 bit della procedura guidata.

Per altre informazioni, vedere [Avviare SQL Server importazione / esportazione guidata](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="step-2---view-the-welcome-page"></a>Passaggio 2 - Visualizzare la pagina iniziale
La prima pagina della procedura guidata è la **pagina iniziale**. 

Per visualizzare questa pagina, è possibile fare clic su **Non visualizzare più questa pagina iniziale**.

![Configurazione guidata](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Passaggio 3: Selezionare Excel come origine dati
Nella pagina successiva **Scegliere un'origine dati**, scegliere Microsoft Excel come origine dati. Quindi, esplorare per selezionare il file di Excel. Infine specificare la versione di Excel usata per creare il file.

> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

![Scegliere l'origine dati di Excel](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Scegliere un'origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Passaggio 4: Selezionare SQL Server come destinazione
Nella pagina successiva **Scegliere una destinazione** selezionare Microsoft SQL Server come destinazione scegliendo uno dei provider di dati nell'elenco che si connetterà a SQL Server. In questo esempio selezionare **Provider di dati .Net Framework per SQL Server**.

La pagina visualizza un elenco di proprietà del provider. Molti dei nomi visualizzati sono complessi e le impostazioni non sono riconoscibili. Fortunatamente, per connettersi a qualsiasi database aziendale è in genere necessario specificare solo tre informazioni. È possibile ignorare i valori predefiniti delle altre impostazioni.

|Informazioni obbligatorie|Proprietà Provider di dati .NET Framework per SQL Server|
|---|---|
|Nome server|**Origine dati**|
|Informazioni di autenticazione (accesso)|**Sicurezza integrata** oppure **ID utente** e **Password**<br/>Per visualizzare un elenco a discesa dei database nel server, è necessario prima specificare informazioni di accesso valide.|
|Nome database|**Catalogo iniziale**|

![Scegliere la destinazione SQL Server](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Per altre informazioni sulla connessione a SQL Server, vedere [Connettersi a un'origine dati di SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Per altre informazioni relative a questa pagina della procedura guidata, vedere [Scegliere una destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Passaggio 5: Copiare una tabella invece di scrivere una query
Nella pagina successiva **Specificare una copia della tabella o una query** specificare che si vuole copiare l'intera tabella di origine dati. Non si vuole scrivere una query nel linguaggio SQL per selezionare i dati da copiare.

![Specificare la copia di una tabella](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Specificare una copia della tabella o una query](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Passaggio 6: Selezionare la tabella da copiare
Nella pagina successiva **Selezionare tabelle e viste di origine** scegliere la tabella o le tabelle da copiare dall'origine dati. Viene poi eseguito il mapping delle tabelle di origine a tabelle di destinazione nuove o esistenti.

In questo esempio la procedura guidata ha eseguito, per impostazione predefinita, il mapping del foglio di lavoro **WizardWalkthrough$** nella colonna **Origine** a una nuova tabella con lo stesso nome della destinazione di SQL Server. (La cartella di lavoro di Excel contiene solo un singolo foglio di lavoro).
-   Il segno di dollaro ($) nel nome della tabella di origine indica un foglio di lavoro di Excel. Un intervallo denominato incluso in Excel è rappresentato solo dal nome.
-   Il simbolo sull'icona della tabella di destinazione indica che la procedura guidata sta per creare una nuova tabella di destinazione.

![Selezionare la tabella (prima di rinominarla)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

È possibile rimuovere il segno di dollaro ($) dal nome della nuova tabella di destinazione.

![Selezionare la tabella (dopo averla rinominata)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Selezionare tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Passaggio 7, facoltativo: Controllare i mapping delle colonne
Prima di lasciare la pagina **Selezione tabelle e viste di origine**, fare clic sul pulsante **Modifica mapping**per aprire la finestra di dialogo **Mapping colonne** (facoltativo). Nella tabella **Mapping** è possibile vedere in che modo la procedura guidata eseguirà il mapping delle colonne dal foglio di lavoro di origine alle colonne nella nuova tabella di destinazione.

![Visualizzare mapping delle colonne](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Per altre informazioni su questa pagina della procedura guidata, vedere [Mapping delle colonne](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Passaggio 8, facoltativo: Controllare l'istruzione CREATE TABLE
Mentre è aperta la finestra di dialogo **Mapping delle colonne**, fare clic sul pulsante **Edit SQL** (Modifica SQL) per aprire la finestra di dialogo **Istruzione SQL CREATE TABLE**. Qui viene visualizzata l'istruzione **CREATE TABLE** generata dalla procedura guidata per creare la nuova tabella di destinazione. In genere non è necessario modificare l'istruzione.

![Visualizzare l'istruzione CREATE TABLE](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Istruzione SQL CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Passaggio 9, facoltativo: Anteprima dei dati da copiare
Dopo aver fatto clic su**OK** per chiudere la finestra di dialogo **Istruzione SQL CREATE TABLE**, fare clic su **OK** per chiudere la finestra di dialogo **Mapping colonne**. Si tornerà nella pagina **Selezione tabelle e viste di origine**. È possibile fare clic sul pulsante **Anteprima** per visualizzare un esempio dei dati che verranno copiati dalla procedura guidata. In questo esempio, è corretto.

![Anteprima dei dati da copiare](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Per altre informazioni su questa pagina della procedura guidata, vedere [Anteprima dati](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Passaggio 10: Sì, eseguire le operazioni di importazione/esportazione
Nella pagina successiva **Salva ed Esegui pacchetto** abilitare **Esegui immediatamente** per avviare la copia dei dati immediata dopo aver fatto clic su **Fine** nella pagina successiva. Oppure ignorare la pagina seguente facendo clic su **Fine**nella pagina **Salvare ed eseguire il pacchetto**.

![Eseguire il pacchetto](../../integration-services/import-export-data/media/run-the-package.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Passaggio 11: Terminare la procedura guidata ed eseguire le operazione di importazione/esportazione
Se nella pagina per **salvare ed eseguire il pacchetto** si è fatto clic su **Avanti** anziché su **Fine**, allora nella pagina successiva, relativa al **completamento della procedura guidata**, verrà visualizzato un riepilogo sulle operazioni che saranno eseguite dalla procedura guidata. Fare clic su **Fine** per eseguire l'operazione di importazione/esportazione.

![Completamento procedura guidata](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Per altre informazioni relative a questa pagina della procedura guidata, vedere [Completare la procedura guidata](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Passaggio 12: Controllare l'esecuzione della procedura guidata
Nella pagina finale osservare come la procedura guidata porta a termine le attività e controllare i risultati. La linea evidenziata indica che i dati sono stati copiati. Esecuzione completata.

![Procedura guidata completata](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Per altre informazioni su questa pagina della procedura guidata, vedere [Esecuzione delle operazioni](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Nuova tabella di dati copiati in SQL Server
Qui (in SQL Server Management Studio) è visualizzata la nuova tabella di destinazione creata in SQL Server dalla procedura guidata.

![Dati copiati in SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

Di seguito (di nuovo in SSMS) sono visualizzati i dati che la procedura guidata ha copiato in SQL Server.

![Dati copiati in SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Altre informazioni  
Altre informazioni sul funzionamento della procedura guidata.
-   **Altre informazioni sulla procedura guidata.** Per una panoramica della procedura guidata, vedere [Importare ed esportare dati con l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Informazioni sui passaggi della procedura guidata.** Per informazioni sui passaggi della procedura guidata, selezionare la pagina desiderata dall'elenco seguente [Passaggi dell'importazione/esportazione guidata SQL Server](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Per ogni pagina della procedura guidata è anche disponibile una pagina di documentazione separata.

-   **Informazioni su come connettersi a origini dati e destinazioni.** Se si cercano informazioni su come connettersi ai dati, selezionare la pagina desiderata nell'elenco in [Connettersi a origini dati con l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). È disponibile una pagina di documentazione separata per ognuna delle diverse origini dati di uso comune.

-   **Altre informazioni sul caricamento di dati da e in Excel.** Se sono necessarie informazioni sulla connessione ai file di Excel, nonché sulle limitazioni e sui problemi noti del caricamento di dati da o a file di Excel, vedere [Caricare i dati da o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
