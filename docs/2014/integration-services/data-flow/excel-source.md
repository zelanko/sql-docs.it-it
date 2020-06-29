---
title: Origine Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ac4995898482abdd1d431a6d038d1f574d13539
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437808"
---
# <a name="excel-source"></a>Origine Excel
  L'origine Excel consente di estrarre dati da fogli di lavoro o intervalli di una cartella di lavoro di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 Sono disponibili quattro diverse modalità di accesso ai dati per l'estrazione dei dati:  
  
-   Vista o tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Risultato di un'istruzione SQL. La query può essere con parametri.  
  
-   Risultato di un'istruzione SQL archiviata in una variabile.  
  
> [!IMPORTANT]  
>  In Excel un intervallo o un foglio di lavoro equivale a una vista o tabella. Nell'elenco delle tabelle disponibili degli editor di origine e di destinazione Excel vengono visualizzati i fogli di lavoro (riconoscibili dalla presenza del simbolo $ in fondo al nome del foglio di lavoro, ad esempio Sheet1$) e gli intervalli denominati (riconoscibili dall'assenza del simbolo $, ad esempio MyRange) esistenti. Per ulteriori informazioni, vedere la sezione Considerazioni sull'utilizzo.  
  
 Per connettersi a un'origine dei dati l'origine Excel utilizza una gestione connessione Excel che specifica il file di cartella di lavoro da utilizzare. Per altre informazioni, vedere [Excel Connection Manager](../connection-manager/excel-connection-manager.md).  
  
 L'origine Excel include un output regolare e un output degli errori.  
  
## <a name="usage-considerations"></a>Considerazioni sull'utilizzo  
 La gestione connessione Excel usa il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Jet 4.0 e il relativo driver ISAM (Indexed Sequential Access Method, metodo di accesso sequenziale indicizzato) di Excel di supporto per stabilire la connessione con le origini dati Excel, quindi leggere e scrivere informazioni.  
  
 Il comportamento di questo provider e del relativo driver è documentato in molti articoli della [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base e, sebbene tali articoli non siano specifici di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o del suo predecessore, Data Transformation Services, consentono di ottenere informazioni circa i comportamenti che possono produrre risultati imprevisti. Per informazioni generali sull'utilizzo e sul comportamento del driver per Excel, vedere [HOWTO: Utilizzare ADO con dati di Excel da Visual Basic o VBA](https://support.microsoft.com/kb/257819).  
  
 I seguenti comportamenti del provider Jet utilizzato insieme al driver per Excel possono produrre risultati imprevisti durante la lettura da un'origine dei dati Excel.  
  
-   **Origini dati**. L'origine dei dati in una cartella di lavoro di Excel può essere un foglio di lavoro, a cui è necessario aggiungere il simbolo $, ad esempio Sheet1$ o un intervallo denominato, ad esempio MyRange. Nelle istruzioni SQL i nomi dei fogli di lavoro devono essere delimitati (ad esempio, [Sheet1$]) per evitare errori di sintassi dovuti alla presenza del simbolo $. In Generatore query tali delimitatori vengono aggiunti automaticamente. Quando si specifica un foglio di lavoro o un intervallo, il driver legge il blocco di celle contigue che inizia con la prima cella non vuota nell'angolo superiore sinistro del foglio di lavoro o dell'intervallo. Non è pertanto possibile utilizzare origini contenenti righe vuote tra i dati oppure tra il titolo o le righe di intestazione e le righe di dati.  
  
-   **Valori mancanti**. Per determinare il tipo di dati di ogni colonna, il driver per Excel legge un determinato numero di righe (8 per impostazione predefinita) nell'origine specificata. Se una colonna contiene tipi di dati diversi, soprattutto se sono presenti sia dati numerici che di testo, il driver adotta il tipo di dati a cui corrisponde il maggior numero di elementi e restituisce valori Null per le celle che contengono dati di tipo diverso. In caso di parità, viene adottato il tipo numerico. La maggior parte delle opzioni di formattazione utilizzate nei fogli di lavoro di Excel non influisce sulla determinazione del tipo di dati. È possibile modificare questo comportamento del driver per Excel specificando la Modalità di importazione. Per specificare la modalità di importazione, aggiungere `IMEX=1` al valore di proprietà estese nella stringa di connessione della gestione connessione Excel nella finestra **Proprietà** . Per altre informazioni, vedere l'articolo relativo a [PRB sui valori di Excel restituiti come NULL tramite OpenRecordset DAO](https://support.microsoft.com/kb/194124).  
  
-   **Testo troncato**. Se il driver determina che una colonna di Excel contiene dati di tipo text, seleziona il tipo di dati (string o memo), in base al più lungo valore campionato. Se il driver non individua valori contenenti più di 255 caratteri nelle righe campionate, gestirà la colonna come una colonna di stringhe di 255 caratteri, anziché come una colonna con tipo di dati memo. I valori contenenti più di 255 caratteri potrebbero essere pertanto troncati. Per evitare troncamenti durante l'importazione di dati da una colonna di tipo memo, è necessario verificare che almeno una delle righe campionate nella colonna di tipo memo contenga un valore con più di 255 caratteri oppure aumentare il numero delle righe campionate dal driver, in modo da includere una riga di questo tipo. È possibile aumentare il numero di righe campionate incrementando il valore di **TypeGuessRows** sotto la chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** . Per altre informazioni, vedere l'articolo relativo a [PRB sul trasferimento di dati dall'origine Jet 4.0 OLEDB che non si effettua con l'errore di buffer di overflow](https://support.microsoft.com/kb/281517).  
  
-   **Tipi di dati**. Il driver per Excel riconosce solo un set limitato di tipi di dati. Tutte le colonne numeriche vengono interpretate come valori double (DT_R8) e tutte le colonne di tipo stringa (con tipo di dati diverso da memo) vengono interpretate come stringhe Unicode di 255 caratteri (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esegue il mapping dei tipi di dati di Excel nel modo seguente:  
  
    -   Numero - Numero a virgola mobile e precisione doppia (DT_R8)  
  
    -   Valuta - Valuta (DT_CY)  
  
    -   Valore booleano - Valore booleano (DT_BOOL)  
  
    -   Data/ora- `datetime` (DT_DATE)  
  
    -   Stringa - Stringa Unicode di 255 caratteri (DT_WSTR)  
  
    -   Memo - Flusso di testo Unicode (DT_NTEXT)  
  
-   **Conversione di tipi di dati e lunghezze**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non viene eseguita la conversione implicita dei tipi di dati. Può essere pertanto necessario utilizzare trasformazioni Colonna derivata o Conversione dati per convertire i dati di Excel in modo esplicito prima di caricarli in una destinazione diversa da Excel oppure per convertire dati non di Excel prima di caricarli in una destinazione Excel. In questo caso può essere conveniente creare il pacchetto iniziale usando Importazione/Esportazione guidata SQL Server, che configura automaticamente le conversioni necessarie. Di seguito sono riportati alcuni esempi di tali conversioni:  
  
    -   Conversione tra colonne di Excel di tipo stringa Unicode e colonne di tipo stringa non Unicode con tabelle codici specifiche  
  
    -   Conversione tra colonne di Excel di tipo stringa di 255 caratteri e colonne di tipo stringa di lunghezze diverse  
  
    -   Conversione tra colonne di Excel di tipo numerico a precisione doppia e colonne numeriche di altro tipo  
  
## <a name="excel-source-configuration"></a>Configurazione dell'origine Excel  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor origine Excel** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor origine Excel &#40;pagina Gestione connessione&#41;](../excel-source-editor-connection-manager-page.md)  
  
-   [Editor origine Excel &#40;pagina Colonne&#41;](../excel-source-editor-columns-page.md)  
  
-   [Editor origine Excel &#40;pagina Output degli errori&#41;](../excel-source-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate di Excel](excel-custom-properties.md)  
  
 Per informazioni sul ciclo tramite un gruppo di file Excel, vedere [Esecuzione di un ciclo su file e tabelle di Excel utilizzando un contenitore Ciclo Foreach](../control-flow/foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Attività correlate  

-   [Caricare dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)

-   [Mapping dei parametri di query a variabili in un componente del flusso di dati](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinamento dei dati per le trasformazioni Unione e Merge Join](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Esecuzione di un ciclo su file e tabelle di Excel utilizzando un contenitore Ciclo Foreach](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Intervento nel blog sull' [importazione dei dati da Excel a 64 bit in SSIS](https://go.microsoft.com/fwlink/?LinkId=217673)sul sito Web hrvoje.piasevoli.com  
  
-   Intervento nel Blog relativo [alla connessione a Excel (xlsx) in SSIS](https://microsoft-ssis.blogspot.com/2014/02/connecting-to-excel-xlsx-in-ssis.html).  
  
  
