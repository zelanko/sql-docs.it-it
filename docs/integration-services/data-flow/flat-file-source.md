---
title: Origine file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfilesource.f1
- sql13.dts.designer.flatfilesourceadapter.connection.f1
- sql13.dts.designer.flatfilesourceadapter.columns.f1
- sql13.dts.designer.flatfilesourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b1a7e2f0320790959df4f29bfd586f70acec9de7
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271052"
---
# <a name="flat-file-source"></a>origine file flat
  L'origine file flat legge dati da un file di testo. Tale file può essere in formato delimitato, a larghezza fissa o misto.  
  
-   Nel formato delimitato per definire le righe e le colonne vengono utilizzati delimitatori di riga e colonna.  
  
-   Nel formato a larghezza fissa per definire le righe e le colonne viene utilizzata la larghezza. In questo formato è inoltre previsto un carattere di riempimento da utilizzare per portare i campi alla lunghezza massima.  
  
-   Nel formato non allineato a destra tutte le colonne sono definite in base alla larghezza, ad eccezione dell'ultima che è delimitata dal delimitatore di riga.  
  
 Per configurare l'origine file flat, procedere nel modo seguente:  
  
-   Aggiungere all'output della trasformazione una colonna contenente il nome del file di testo da cui l'origine file flat estrae i dati.  
  
-   Specificare se le stringhe di lunghezza zero nelle colonne devono essere interpretate come valori Null.  
  
    > [!NOTE]  
    >  Affinché sia possibile interpretare come Null le stringhe di lunghezza zero, la gestione connessione file flat utilizzata dall'origine file flat deve essere configurata per l'utilizzo di un formato delimitato. Se la gestione connessione utilizza un formato a larghezza fissa o non allineato a destra, i dati costituiti da spazi non potranno essere interpretati come valori Null.  
  
 Le colonne di output nell'output dell'origine file flat includono la proprietà FastParse. FastParse indica se la colonna usa le routine di analisi più veloci ma indipendenti dalle impostazioni locali disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oppure le routine di analisi standard dipendenti dalle impostazioni locali. Per altre informazioni, vedere [Analisi veloce](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) e [Analisi standard](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013).  
  
 Le colonne di output includono anche la proprietà UseBinaryFormat, utilizzata per implementare il supporto per i dati binari, ad esempio i dati con formato decimale packed, all'interno dei file. Per impostazione predefinita, la proprietà UseBinaryFormat è impostata su **false**. Se si preferisce usare un formato binario, impostare UseBinaryFormat su **true** e il tipo di dati nella colonna di output su **DT_BYTES**. In questo modo, nell'origine file flat viene saltata la conversione dei dati e i dati vengono passati alla colonna di output così come sono. È quindi possibile usare una trasformazione, ad esempio Colonna derivata o Conversione dati, per eseguire il cast dei dati **DT_BYTES** in un diverso tipo di dati oppure scrivere uno script personalizzato in una trasformazione Script per interpretare i dati. Per l'interpretazione dei dati è inoltre possibile scrivere un componente del flusso di dati personalizzato. Per altre informazioni sui tipi di dati in cui può essere eseguito il cast di **DT_BYTES**, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Per accedere al file di testo, questa origine utilizza una gestione connessione file flat. Impostando le proprietà di tale gestione connessione è possibile fornire informazioni sul file e le singole colonne contenute, nonché specificare la modalità con cui l'origine file flat deve gestire i dati del file di testo. È ad esempio possibile specificare i caratteri che delimitano le righe e le colonne del file, oltre al tipo di dati e alla lunghezza di ogni colonna. Per ulteriori informazioni, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Questa origine include un output e un output degli errori.  
  
## <a name="configuration-of-the-flat-file-source"></a>Configurazione dell'origine file flat  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate del file flat](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà di un componente del flusso di dati, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-source-editor-connection-manager-page"></a>Editor origine file flat (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor origine file flat** per selezionare la gestione connessione file flat per l'origine da utilizzare. L'origine file flat legge i dati da un file di testo. I dati possono essere in formato delimitato, a larghezza fissa o misto.  
  
 Un'origine file flat può utilizzare uno dei tipi seguenti di gestione connessione:  
  
-   Gestione connessione file flat se l'origine è un singolo file flat. Per ulteriori informazioni, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
-   Gestione connessione per più file flat se l'origine è data da più file flat e l'attività Flusso di dati si trova in un contenitore Ciclo, ad esempio il contenitore Ciclo For. In ogni ciclo del contenitore, l'origine file flat carica dati dal nome file successivo fornito dalla gestione connessione per più file. Per ulteriori informazioni, vedere [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Flat file connection manager**  
 Consente di selezionare una gestione connessione esistente nell'elenco o di creare una nuova gestione connessione facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Editor gestione connessione file flat** .  
  
 **Mantieni i valori Null dell'origine come valori Null nel flusso di dati**  
 Consente di specificare se mantenere i valori Null durante l'estrazione dei dati. Il valore predefinito della proprietà è **false**. Quando questo valore è f**alse**, l'origine del file flat sostituisce i valori Null dai dati di origine con i valori predefiniti corretti per ogni colonna, ad esempio stringhe vuote per colonne con stringhe e zero per colonne numeriche.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
## <a name="flat-file-source-editor-columns-page"></a>Editor origine file flat (pagina Colonne)
  Usare il nodo **Colonne** della finestra di dialogo **Editor origine file flat** per eseguire il mapping tra una colonna di output e ogni colonna esterna (di origine).  
  
> [!NOTE]  
>  La proprietà **FileNameColumnName** dell'origine file flat e la proprietà **FastParse** delle relative colonne di output non sono disponibili nell' **Editor origine file flat**, tuttavia possono essere impostate utilizzando l' **Editor avanzato**. Per ulteriori informazioni su queste proprietà, vedere la sezione relativa all'origine file flat in [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
### <a name="options"></a>Opzioni  
 **Colonne esterne disponibili**  
 Consente di visualizzare l'elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne.  
  
 **Colonna esterna**  
 Consente di visualizzare le colonne esterne (origine) nell'ordine in cui verranno lette dall'attività. È possibile modificare l'ordine deselezionando innanzitutto le colonne della tabella selezionate e quindi selezionando dall'elenco le colonne esterne in un ordine diverso.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="flat-file-source-editor-error-output-page"></a>Editor origine file flat (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor origine file flat** per selezionare le opzioni di gestione degli errori e impostare le proprietà nelle colonne di output degli errori.\  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (di origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine file flat**.  
  
 **Errore**  
 Consente di specificare l'azione da eseguire in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Argomenti correlati:** [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Troncamento**  
 Consente di specificare l'azione da eseguire in caso di troncamenti, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'errore.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione file flat](../../integration-services/data-flow/flat-file-destination.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
