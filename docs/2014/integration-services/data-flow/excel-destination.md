---
title: Destinazione Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldest.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84647752eb549bd5d3607637d679e58356597a6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827224"
---
# <a name="excel-destination"></a>Destinazione Excel
  La destinazione Excel consente di caricare dati in fogli di lavoro o intervalli di una cartella di lavoro di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
## <a name="access-modes"></a>Modalità di accesso  
 Sono disponibili tre diverse modalità di accesso ai dati per il caricamento dei dati:  
  
-   Vista o tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Risultato di un'istruzione SQL. La query può essere con parametri.  
  
> [!IMPORTANT]  
>  In Excel un intervallo o un foglio di lavoro equivale a una vista o tabella. Nell'elenco delle tabelle disponibili degli editor dell'origine e della destinazione Excel vengono visualizzati solo i fogli di lavoro (riconoscibili dalla presenza del simbolo $ in fondo al nome del foglio di lavoro, ad esempio Sheet1$) e gli intervalli denominati (riconoscibili dall'assenza del simbolo $, ad esempio MyRange) esistenti.  
  
## <a name="usage-considerations"></a>Considerazioni sull'utilizzo  
 La gestione connessione Excel usa il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Jet 4.0 e il relativo driver ISAM (Indexed Sequential Access Method, metodo di accesso sequenziale indicizzato) di Excel di supporto per stabilire la connessione con le origini dati Excel, quindi leggere e scrivere informazioni.  
  
 Il comportamento di questo provider e del relativo driver è documentato in molti articoli della [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base e, sebbene tali articoli non siano specifici di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o del suo predecessore, Data Transformation Services, consentono di ottenere informazioni circa i comportamenti che possono produrre risultati imprevisti. Per informazioni generali sull'uso e sul comportamento del driver per Excel, vedere [HOWTO: Utilizzo di ADO con dati di Excel da Visual Basic o VBA](https://support.microsoft.com/kb/257819).  
  
 I seguenti comportamenti del provider Jet incluso nel driver per Excel possono produrre risultati imprevisti durante il salvataggio di dati in una destinazione Excel.  
  
-   **Salvataggio di dati di testo**. Quando salva dati di testo in una destinazione Excel, il driver per Excel antepone una virgoletta singola (') al testo in ogni cella, per garantire che i valori salvati verranno interpretati come testo. Se si usano o si sviluppano altre applicazioni che leggono o elaborano i dati salvati, può essere necessario includere istruzioni specifiche per la gestione della virgoletta singola (') che precede ogni valore di testo.  
  
     Per informazioni su come evitare di includere la virgoletta singola, vedere il post di blog seguente relativo all' [aggiunta della virgoletta singola a tutte le stringhe quando i dati sono trasformati in Excel tramite il componente per flusso di dati di destinazione di Excel in un pacchetto SSIS](https://go.microsoft.com/fwlink/?LinkId=400876), su msdn.com.  
  
-   **Salvataggio di dati memo (ntext)** . Per poter salvare correttamente stringhe di oltre 255 caratteri in una colonna Excel, il driver deve riconoscere il tipo di dati della colonna di destinazione come **memo** invece di **string**. Se la tabella di destinazione contiene già righe di dati, le prime righe campionate dal driver devono contenere almeno un'istanza di un valore composto da più di 255 caratteri nella colonna con tipo di dati memo. Se la tabella di destinazione viene creata durante la progettazione del pacchetto o in fase di esecuzione, quindi l'istruzione CREATE TABLE deve usare LONGTEXT (o uno dei sinonimi) come tipo di dati della colonna di tipo memo.  
  
-   **Tipi di dati**. Il driver per Excel riconosce solo un set limitato di tipi di dati. Tutte le colonne numeriche vengono interpretate come valori double (DT_R8) e tutte le colonne di tipo stringa (con tipo di dati diverso da memo) vengono interpretate come stringhe Unicode di 255 caratteri (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esegue il mapping dei tipi di dati di Excel nel modo seguente:  
  
    -   Numero    Numero a virgola mobile e precisione doppia (DT_R8)  
  
    -   Valuta     Valuta (DT_CY)  
  
    -   Valore booleano     Valore booleano (DT_BOOL)  
  
    -   Data/ora `datetime` (DT_DATE)  
  
    -   Stringa     Stringa Unicode di 255 caratteri (DT_WSTR)  
  
    -   Memo     Flusso di testo Unicode (DT_NTEXT)  
  
-   **Conversione di tipi di dati e lunghezze**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non viene eseguita la conversione implicita dei tipi di dati. Può essere pertanto necessario usare le trasformazioni Colonna derivata o Conversione dati per convertire i dati di Excel in modo esplicito prima di caricarli in una destinazione diversa da Excel oppure per convertire dati non di Excel prima di caricarli in una destinazione Excel. In questo caso può essere conveniente creare il pacchetto iniziale usando Importazione/Esportazione guidata SQL Server, che configura automaticamente le conversioni necessarie. Di seguito sono riportati alcuni esempi di tali conversioni:  
  
    -   Conversione tra colonne di Excel di tipo stringa Unicode e colonne di tipo stringa non Unicode con tabelle codici specifiche  
  
    -   Conversione tra colonne di Excel di tipo stringa di 255 caratteri e colonne di tipo stringa di lunghezze diverse  
  
    -   Conversione tra colonne di Excel di tipo numerico a precisione doppia e colonne numeriche di altro tipo  
  
## <a name="configuration-of-the-excel-destination"></a>Configurazione della destinazione Excel  
 Per connettersi a un'origine dei dati, la destinazione Excel usa una gestione connessione Excel che specifica il file di cartella di lavoro da usare. Per altre informazioni, vedere [Excel Connection Manager](../connection-manager/excel-connection-manager.md).  
  
 La destinazione Excel include un input regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor destinazione Excel** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione Excel &#40;pagina Gestione connessione&#41;](../excel-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione Excel &#40;pagina Mapping&#41;](../excel-destination-editor-mappings-page.md)  
  
-   [Editor destinazione Excel &#40;pagina Output degli errori&#41;](../excel-destination-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate di Excel](excel-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Caricare dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
  
-   [Esecuzione di un ciclo su file e tabelle di Excel usando un contenitore Ciclo Foreach](../control-flow/foreach-loop-container.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Intervento nel blog concernente [Excel in Integration Services, parte 1 di 3: Connessioni e componenti](https://go.microsoft.com/fwlink/?LinkId=217674), su dougbert.com  
  
-   Intervento nel blog concernente [Excel in Integration Services, parte 2 di 3: Le tabelle e tipi di dati](https://go.microsoft.com/fwlink/?LinkId=217675), su dougbert.com.  
  
-   Intervento nel blog concernente [Excel in Integration Services, parte 3 di 3: Problemi e alternative](https://go.microsoft.com/fwlink/?LinkId=217676), su dougbert.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Origine Excel](excel-source.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md)   
 [Flusso di dati](data-flow.md)   
 [Utilizzo di file di Excel con l'attività Script](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
