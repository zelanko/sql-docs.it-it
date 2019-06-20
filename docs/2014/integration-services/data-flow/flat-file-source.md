---
title: Origine file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesource.f1
helpviewer_keywords:
- sources [Integration Services], Flat File
- text file reading [Integration Services]
- flat files
- Flat File source
ms.assetid: 4a64f7f3-f25d-4db0-93b3-a29496030e58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6338c7a306f163f786f2c1e7d44ae4dbc66504ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62902449"
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
  
 Le colonne di output nell'output dell'origine file flat includono la proprietà FastParse. FastParse indica se la colonna usa le routine di analisi più veloci ma indipendenti dalle impostazioni locali disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oppure le routine di analisi standard dipendenti dalle impostazioni locali. Per altre informazioni, vedere [Analisi veloce](../fast-parse.md) e [Analisi standard](../standard-parse.md).  
  
 Le colonne di output includono anche la proprietà UseBinaryFormat, utilizzata per implementare il supporto per i dati binari, ad esempio i dati con formato decimale packed, all'interno dei file. Per impostazione predefinita UseBinaryFormat è impostata su `false`. Se si desidera utilizzare un formato binario, impostare UseBinaryFormat su `true` e il tipo di dati della colonna di output su `DT_BYTES`. In questo modo, nell'origine file flat viene saltata la conversione dei dati e i dati vengono passati alla colonna di output così come sono. È quindi possibile utilizzare una trasformazione, ad esempio Colonna derivata o Conversione dati, per eseguire il cast dei dati `DT_BYTES` in un diverso tipo di dati oppure scrivere uno script personalizzato in una trasformazione Script per interpretare i dati. Per l'interpretazione dei dati è inoltre possibile scrivere un componente del flusso di dati personalizzato. Per altre informazioni su quali tipi di dati possono eseguire il cast `DT_BYTES` per visualizzare [Cast &#40;espressione SSIS&#41;](../expressions/cast-ssis-expression.md).  
  
 Per accedere al file di testo, questa origine utilizza una gestione connessione file flat. Impostando le proprietà di tale gestione connessione è possibile fornire informazioni sul file e le singole colonne contenute, nonché specificare la modalità con cui l'origine file flat deve gestire i dati del file di testo. È ad esempio possibile specificare i caratteri che delimitano le righe e le colonne del file, oltre al tipo di dati e alla lunghezza di ogni colonna. Per ulteriori informazioni, vedere [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Questa origine include un output e un output degli errori.  
  
## <a name="configuration-of-the-flat-file-source"></a>Configurazione dell'origine file flat  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor origine file flat**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor origine file flat &#40;pagina Gestione connessione&#41;](../flat-file-source-editor-connection-manager-page.md)  
  
-   [Editor origine file flat &#40;pagina Colonne&#41;](../flat-file-source-editor-columns-page.md)  
  
-   [Editor origine file flat &#40;pagina Output degli errori&#41;](../flat-file-source-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate del file flat](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà di un componente del flusso di dati, vedere [Impostare le proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione file flat](flat-file-destination.md)   
 [Flusso di dati](data-flow.md)  
  
  
