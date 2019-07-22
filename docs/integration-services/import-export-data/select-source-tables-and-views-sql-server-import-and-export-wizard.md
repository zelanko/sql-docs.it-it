---
title: Selezione tabelle e viste di origine (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8c42b4c7438eade57b8615d5011945112d9451a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901727"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Selezione tabelle e viste di origine (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Dopo aver specificato che si vuole copiare un'intera tabella o dopo aver specificato una query, l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] visualizza **Seleziona tabelle e viste di origine**. In questa pagina è possibile selezionare le tabelle e le viste esistenti da copiare. Viene poi eseguito il mapping delle tabelle di origine in tabelle di destinazione nuove o esistenti. Facoltativamente, è anche possibile esaminare il mapping di singole colonne e visualizzare in anteprima i dati di esempio.

> [!TIP]
> Se è necessario copiare più database SQL Server o più oggetti di database SQL Server diversi da tabelle e viste, usare Copia guidata database anziché Importazione/Esportazione guidata. Per altre informazioni, vedere [Utilizzo di Copia guidata database](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Screenshot: se si copiano tabelle  
 Lo screenshot seguente illustra un esempio della pagina **Selezione tabelle e viste di origine** della procedura guidata dopo che è stata selezionata l'opzione **Copia i dati da una o più tabelle o viste** nella pagina **Impostazione copia tabella o query**. L'elenco visualizza tutte le tabelle e le viste disponibili dall'origine dati.
 
In questo esempio, l'elenco **Origine** contiene tutte le tabelle nel database di esempio AdventureWorks. La riga selezionata illustra che l'utente vuole copiare la tabella **Sales.Customer** dall'origine nella nuova tabella **Sales.CustomerNew** di destinazione. 
   
 ![Pagina Selezione tabelle dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/select-tables1.png "Pagina Selezione tabelle dell'Importazione/Esportazione guidata")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Screenshot: se si specifica una query  
 Lo screenshot seguente illustra un esempio della pagina **Selezione tabelle e viste di origine** della procedura guidata dopo che è stata selezionata l'opzione **Scrivi una query per specificare i dati da trasferire** nella pagina **Impostazione copia tabella o query**. L'elenco **Origine** contiene un'unica riga, in cui l'elemento denominato `[Query]` rappresenta la query specificata nella pagina **Impostazione query di origine**.
 
In questo esempio, l'utente vuole copiare i risultati della query dall'origine dati nella tabella **Sales.CustomerNew** di destinazione.  
    
 ![Pagina Selezione tabelle dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/select-tables2.png "Pagina Selezione tabelle dell'Importazione/Esportazione guidata")  

## <a name="select-source-and-destination-tables"></a>Selezionare le tabelle di origine e di destinazione 
**Origine**  
Mediante le caselle di controllo, selezionare dall'elenco di tabelle e viste disponibili quelle da copiare nella destinazione. Per impostazione predefinita, i dati dell'origine dati vengono copiati senza modifiche. Se si crea una nuova tabella di destinazione, viene copiato senza modifiche anche lo schema per la nuova tabella, in altre parole l'elenco delle colonne e le relative proprietà, dall'origine dati.

Se è stata specificata una query, l'elenco contiene un unico elemento denominato `[Query]`. 

**Destinazione**  
 Selezionare una tabella di destinazione dall'elenco per ogni tabella di origine o query oppure immettere il nome di una nuova tabella da creare con la procedura guidata. Se si seleziona una tabella di destinazione esistente, è necessario che la tabella abbia colonne con tipi di dati compatibili con i dati di origine.  

> [!NOTE]
> Se la procedura guidata viene sospesa a questo punto per creare manualmente una nuova tabella nel database di destinazione tramite uno strumento esterno, ad esempio  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], la nuova tabella non sarà subito visibile nell'elenco delle tabelle di destinazione disponibili. Per aggiornare l'elenco delle tabelle di destinazione, tornare indietro alla pagina **Scelta destinazione** , selezionare di nuovo il database di destinazione per aggiornare l'elenco delle tabelle e delle viste disponibili e quindi avanzare fino alla pagina **Selezione tabelle e viste di origine** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Facoltativamente, rivedere i mapping delle colonne e visualizzare in anteprima i dati
**Modifica mapping**   
Facoltativamente, fare clic su **Modifica mapping** per visualizzare la finestra di dialogo **Mapping colonne** per la tabella selezionata. Nella finestra di dialogo **Mapping colonne** eseguire le operazioni seguenti,
-   Esaminare il mapping di singole colonne tra l'origine e la destinazione.
-   Copiare solo un subset di colonne selezionando **ignora** per le colonne da non copiare.

Per altre informazioni, vedere [Mapping colonne](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Anteprima**  
Facoltativamente, fare clic su **Anteprima** per visualizzare in anteprima fino a 200 righe di dati di esempio nella finestra di dialogo **Anteprima dati**. Questo permette di verificare che la procedura guidata sta per copiare i dati desiderati. Per altre informazioni, vedere [Anteprima dati](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Dopo aver visualizzato i dati in anteprima, potrebbe essere necessario modificare le opzioni selezionate nelle pagine precedenti della procedura guidata. Per apportare queste modifiche, tornare alla pagina **Seleziona tabelle e viste di origine** e quindi fare clic su **Indietro** per tornare alle pagine precedenti nelle quali modificare le opzioni selezionate.  

## <a name="select-source-and-destination-tables-for-excel"></a>Selezionare le tabelle di origine e di destinazione per Excel

> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

### <a name="excel-source-tables"></a>Tabelle di origine Excel
L'elenco delle tabelle e delle viste di origine di un'origine dati Excel include due tipi di oggetti Excel.
-   **Fogli di lavoro**. I nomi dei fogli di lavoro sono seguiti dal segno di dollaro ($), ad esempio **'Foglio1$'** .
-   **Intervalli denominati.** Gli intervalli denominati, se presenti, sono elencati per nome.

Se si vuole caricare i dati da o in uno specifico intervallo di celle senza nome, ad esempio **[Foglio1$A1:B4]** , è necessario scrivere una query. Tornare alla pagina **Impostazione copia tabella o query** e selezionare **Scrivi una query per specificare i dati da trasferire**.

### <a name="excel-destination-tables"></a>Tabelle di destinazione Excel
Se si esportano dati in Excel, è possibile specificare la destinazione in uno dei tre modi seguenti.
-   **Foglio di lavoro.** Per specificare un foglio di lavoro, aggiungere il carattere $ alla fine del nome del foglio e aggiungere delimitatori all'inizio e alla fine della stringa, ad esempio **[Foglio1$]** .
-   **Intervallo denominato.** Per specificare un intervallo denominato, è sufficiente usare il nome dell'intervallo, ad esempio **MioIntervalloDati**.
-   **Intervallo senza nome.** Per specificare un intervallo di celle a cui non è stato assegnato un nome, aggiungere il carattere $ alla fine del nome del foglio, aggiungere la specifica dell'intervallo e aggiungere delimitatori all'inizio e alla fine della stringa, ad esempio **[Foglio1$A1:B4]** .

> [!TIP]
> Quando si usa Excel come origine o destinazione, è consigliabile fare clic su **Modifica mapping** e rivedere i mapping dei tipi di dati nella pagina **Mapping colonne** . 

## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver selezionato le tabelle e le viste esistenti da copiare e sottoporre a mapping nelle rispettive destinazioni, la pagina successiva è **Salvare ed eseguire il pacchetto**. In questa pagina specificare se eseguire immediatamente l'operazione di copia. A seconda della configurazione, è anche possibile salvare il pacchetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creato dalla procedura guidata per personalizzarlo e usarlo di nuovo in seguito. Per altre informazioni, vedere [Salvare ed eseguire il pacchetto](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Vedere anche
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)



