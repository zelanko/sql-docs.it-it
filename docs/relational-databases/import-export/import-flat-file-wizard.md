---
title: Importare file flat in SQL | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 962ed44bad714125f78cac5adff5af42b0c76685
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138443"
---
# <a name="import-flat-file-to-sql-wizard"></a>Procedura guidata per l'importazione di file flat in SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
> Per i contenuti correlati all'importazione ed esportazione guidata, vedere la pagina relativa all'[Importazione/Esportazione guidata SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).

La procedura guidata per l'importazione di file flat consente di copiare facilmente i dati da un file flat (con estensione csv, txt) a una nuova tabella nel database. In questa panoramica vengono descritti i motivi per l'uso di questa procedura guidata, come trovarla e un semplice esempio da seguire.

## <a name="why-would-i-use-this-wizard"></a>Perché usare questa procedura guidata?
Questa procedura guidata è stata creata per migliorare l'esperienza di importazione corrente sfruttando un framework intelligente noto come Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)). Per un utente senza una conoscenza specializzata dei domini, l'importazione dei dati può risultare un'attività complessa, soggetta a errori e impegnativa. Questa procedura guidata semplifica il processo di importazione: è sufficiente selezionare un file di input e un nome di tabella univoco e il framework PROSE gestisce il resto.

PROSE analizza i modelli di dati nel file di input per dedurre nomi di colonne, tipi, delimitatori e altro ancora. Questo framework apprende la struttura del file ed esegue l'intero lavoro al posto degli utenti.

Per comprendere meglio il miglioramento dell'esperienza utente della procedura guidata Importa file flat, vedere questo video:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player]

## <a name="prerequisites"></a>Prerequisites
Questa funzionalità è disponibile solo in SQL Server Management Studio (SSMS) v17.3 o versioni successive. Verificare che sia in uso la versione più recente. La versione più recente è disponibile [qui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
 
## <a id="started"></a>Introduzione
Per accedere alla procedura guidata per l'importazione di file flat, procedere come segue:

1. Aprire **SQL Server Management Studio**.
2. Connettersi a un'istanza del motore di database di Microsoft SQL Server o localhost.
3. Espandere **Database**, fare clic con il pulsante destro del mouse su un database (vedere l'esempio seguente), scegliere **Attività** e fare clic su **Importa file flat** sopra a Importa dati.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

![Menu della procedura guidata](media/import-flat-file-wizard/importffmenu.png)

Per altre informazioni sulle diverse funzioni della procedura guidata, vedere l'esercitazione seguente:

## <a name="tutorial"></a>Esercitazione
Ai fini di questa esercitazione, è possibile usare il proprio file flat. In caso contrario, servirsi del file CSV seguente da Excel, che può essere copiato liberamente. Se si usa questo CSV, denominarlo **esempio.csv** e salvarlo con l'estensione csv in un percorso semplice come ad esempio il desktop.

![Procedura guidata Excel](media/import-flat-file-wizard/importffexample.png)

### <a name="step-1-access-wizard-and-intro-page"></a>Passaggio 1: Accedere alla procedura guidata e alla pagina introduttiva
Accedere alla procedura guidata come descritto [qui](#started).

La prima pagina della procedura guidata è la pagina di benvenuto. Se non si vuole più visualizzare questa pagina, è possibile fare clic su **Non visualizzare più questa pagina iniziale**.

![Pagina introduttiva della procedura guidata](media/import-flat-file-wizard/importffintro.png)

### <a name="step-2-specify-input-file"></a>Passaggio 2: Specificare il file di input
Fare clic su Sfoglia per selezionare il file di input. Per impostazione predefinita, la procedura guidata cerca i file con estensione csv e txt. 

Il nuovo nome di tabella deve essere univoco. In caso contrario, la procedura guidata non consente di proseguire.

![Finestra di specifica della procedura guidata](media/import-flat-file-wizard/importffspecify.png)

### <a name="step-3-preview-data"></a>Passaggio 3: Anteprima dei dati
La procedura guidata genera un'anteprima che consente di visualizzare le prime 50 righe. Se sono presenti problemi fare clic su Annulla, in caso contrario passare alla pagina successiva.

![Anteprima della procedura guidata](media/import-flat-file-wizard/importffpreview.png)

### <a name="step-4-modify-columns"></a>Passaggio 4: Modificare le colonne
La procedura guidata identifica quelli che presume essere i nomi di colonna, i tipi di dati, e così via, corretti. A questo punto è possibile modificare i campi se non sono corretti (ad esempio, il tipo di dati deve essere un valore float anziché un valore int).

Quando si è pronti, proseguire.

![Finestra di modifica della procedura guidata](media/import-flat-file-wizard/importffmodify.png)

### <a name="step-5-summary"></a>Passaggio 5: Riepilogo
Si tratta semplicemente di una pagina di riepilogo che visualizza la configurazione corrente. Se sono presenti problemi, è possibile tornare alle sezioni precedenti. In caso contrario, fare clic su Fine per tentare il processo di importazione.

![Riepilogo della procedura guidata](media/import-flat-file-wizard/importffsummary.png)

### <a name="step-6-results"></a>Passaggio 6: Risultati
Questa pagina indica se l'importazione è riuscita. Se viene visualizzato un segno di spunta verde, l'importazione ha avuto esito positivo, in caso contrario potrebbe essere necessario rivedere la configurazione o il file di input per individuare eventuali errori.

![Risultati della procedura guidata](media/import-flat-file-wizard/importffresults.png)

## <a name="learn-more"></a>Ulteriori informazioni

Altre informazioni sulla procedura guidata.
 
- **Altre informazioni sull'importazione di altre origini**. Se si sta cercando di importare più file flat, vedere la pagina relativa all'[Importazione/Esportazione guidata SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).
- **Altre informazioni su come connettersi alle origini dei file flat**. Se sono necessarie altre informazioni sulla connessione alle origini dei file flat, vedere [Connettersi a un'origine dati file flat](https://docs.microsoft.com/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard).
- **Altre informazioni su PROSE**. Se si sta cercando una panoramica del framework intelligente usato da questa procedura guidata, vedere la pagina relativa all'[SDK PROSE](https://microsoft.github.io/prose/).

