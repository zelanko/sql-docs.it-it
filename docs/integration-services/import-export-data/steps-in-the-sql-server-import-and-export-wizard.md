---
title: Passaggi dell'Importazione/Esportazione guidata SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ea71b8970119a5c88f38bb31e4a728addc0954fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023617"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Passaggi dell'Importazione/Esportazione guidata SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


In questo argomento viene descritta la sequenza dei passaggi per l'importazione e l'esportazione dei dati nell'Importazione/Esportazione guidata SQL Server. Sono anche disponibili collegamenti alle singole pagine della documentazione che descrivono ogni pagina o la finestra di dialogo usata nella procedura guidata.

Questo articolo descrive solo i **passaggi** della procedura guidata. Per altre informazioni, vedere [Attività e contenuti correlati](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Passaggi per l'importazione e l'esportazione dei dati  
 La tabella seguente elenca i passaggi necessari per l'importazione e l'esportazione di dati e le pagine corrispondenti della procedura guidata. In genere, non vengono visualizzate tutte le pagine, ma solo quelle corrispondenti alle opzioni selezionate nella procedura guidata.  

Per esaminare rapidamente le diverse schermate visualizzate durante una normale sessione, vedere questo semplice esempio illustrato in una singola pagina: [Introduzione a un esempio semplice di importazione/esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Passaggio|Pagine della procedura guidata|  
|----------|------------------|  
|**Pagina iniziale**<br />Non è necessario eseguire alcuna operazione in questa pagina.|[Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Selezionare l'origine** dei dati.|[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Selezionare la destinazione** dei dati.|[Scegliere una destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Configurare la destinazione** (passaggi facoltativi)<br /><br /> -   Creare un nuovo database di destinazione.<br />-   Se si stanno copiando dati in un file di testo, configurare impostazioni aggiuntive.|[Crea database](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Configurare la destinazione del file flat](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Specificare gli elementi da copiare.**|[Impostazione copia tabella o query](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Seleziona tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Impostazione query di origine](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Configurare l'operazione di copia** (passaggi facoltativi)<br /><br /> -   Creare una nuova tabella di destinazione.<br />-   Decidere come procedere se la procedura guidata non esegue il mapping dei tipi di dati tra l'origine e la destinazione selezionate.<br />-   Rivedere i mapping a livello di colonne tra l'origine e la destinazione.<br />-   Gestire i problemi mediante la conversione dei tipi di dati tra l'origine e la destinazione.<br />-   Visualizzare in anteprima i dati da copiare.|[Istruzione SQL CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Converti tipi senza eseguire i controlli di conversione](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Mapping colonne](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Verifica mapping tra i tipi di dati](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Finestra di dialogo Dettagli conversione colonna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Finestra di dialogo Anteprima dati](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Copiare i dati.**<br /><br /> Facoltativamente, salvare le impostazioni come pacchetto di SQL Server Integration Services (SSIS).|[Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[Salva pacchetto SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Completamento procedura guidata](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Esecuzione dell'operazione](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Premere il tasto F1 da qualsiasi pagina o finestra di dialogo della procedura guidata per visualizzare la documentazione relativa alla pagina corrente.

## <a name="related"></a> Attività e argomenti correlati  
Ecco alcune altre attività di base.
-   **Vedere un rapido esempio sul funzionamento della procedura guidata.**

    -   **Se si preferisce visualizzare screenshot.** Esaminare questo semplice esempio end-to-end in una singola pagina: [Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Se si preferisce guardare un video.** Questo video di YouTube della durata di quattro minuti illustra la procedura guidata e descrive come importare ed esportare dati in Excel con istruzioni chiare e semplici: [Uso dell'Importazione/Esportazione guidata SQL Server per l'esportazione in Excel](https://go.microsoft.com/fwlink/?linkid=829049) .

-   **Altre informazioni sul funzionamento della procedura guidata.**

    -   **Altre informazioni sulla procedura guidata.** Per una panoramica della procedura guidata, vedere [Importare ed esportare dati con l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Informazioni su come connettersi a origini dati e destinazioni.** Se si cercano informazioni su come connettersi ai dati, selezionare la pagina desiderata nell'elenco in [Connettersi a origini dati con l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). È disponibile una pagina di documentazione separata per ognuna delle diverse origini dati di uso comune. 

-   **Avviare la procedura guidata** Se si è pronti per eseguire la procedura guidata e servono solo le istruzioni per iniziare, vedere [Avviare l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **Ottenere la procedura guidata.** Se si vuole eseguire la procedura guidata, ma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è disponibile nel computer, è possibile installare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installando SQL Server Data Tools (SSDT). Per altre informazioni, vedere [Scaricare SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


