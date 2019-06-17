---
title: Origine XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28e7a7395c02e44e52469992f3738f0d873e227f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62899944"
---
# <a name="xml-source"></a>Origine XML
  L'origine XML legge un file di dati XML e popola con tali dati le colonne nell'output dell'origine.  
  
 Nei file XML i dati includono spesso relazioni gerarchiche. Un file di dati XML può ad esempio rappresentare cataloghi e articoli di catalogo. Prima di immettere i dati nel flusso di dati è necessario determinare le relazioni tra gli elementi del file di dati XML e generare un output per ogni elemento del file.  
  
## <a name="schemas"></a>Schemi  
 Per interpretare i dati XML, l'origine XML utilizza uno schema. L'origine XML supporta l'utilizzo di un file XSD (XML Schema Definition) o di schemi inline per la conversione dei dati in formato tabulare. Se si configura l'origine XML tramite la finestra di dialogo **Editor origine XML** , l'interfaccia utente può generare un file XSD dal file di dati XML specificato.  
  
> [!NOTE]  
>  I DTD non sono supportati.  
  
 Gli schemi possono supportare un solo spazio dei nomi. Le raccolte di schemi non sono supportate.  
  
> [!NOTE]  
>  L'origine XML non convalida i dati nel file XML rispetto al file XSD.  
  
## <a name="xml-source-editor"></a>Editor origine XML  
 Nei file XML i dati includono spesso relazioni gerarchiche. La finestra di dialogo **Editor origine XML** usa lo schema specificato per generare gli output dell'origine XML. È possibile specificare un file XSD, utilizzare uno schema inline oppure generare un file XSD dal file di dati XML specificato. Lo schema deve essere disponibile in fase di progettazione.  
  
 L'origine XML genera strutture tabulari dai dati XML creando un output per ogni elemento del file XML che contiene altri elementi. Se ad esempio i dati XML rappresentano cataloghi e articoli di catalogo, l'origine XML creerà un output per i cataloghi e uno per ogni tipo di articolo contenuto nei cataloghi. L'output di ogni articolo conterrà colonne di output per gli attributi dell'articolo.  
  
 Per fornire informazioni sulle relazioni gerarchiche dei dati negli output, l'origine XML aggiunge agli output una colonna che identifica l'elemento padre di ogni elemento figlio. Se nell'esempio dei cataloghi sono presenti diversi tipi di articoli, a ogni articolo corrisponderà un valore di colonna che identifica il catalogo a cui appartiene.  
  
 L'origine XML crea un output per ogni elemento, ma non è necessario utilizzare tutti gli output. È possibile eliminare qualsiasi output che non si desidera utilizzare o semplicemente evitare di connetterlo a un componente a valle.  
  
 L'origine XML genera inoltre i nomi degli output, per garantire l'utilizzo di nomi univoci. Tali nomi possono essere tuttavia troppo lunghi e non identificare gli output in modo utile all'utente. È possibile rinominare gli output, purché i nomi rimangano univoci. È inoltre possibile modificare il tipo di dati e la lunghezza delle colonne di output.  
  
 L'origine XML aggiunge un output degli errori per ogni output. Per impostazione predefinita le colonne negli output degli errori hanno tipo di dati stringa Unicode (DT_WSTR) e lunghezza 255, ma è possibile configurarle modificandone il tipo di dati e la lunghezza.  
  
 Se il file di dati XML contiene elementi non presenti nel file XSD, tali elementi verranno ignorati e non verrà generato alcun output corrispondente. Se viceversa nel file di dati XML mancano elementi che sono rappresentati nel file XSD, l'output conterrà colonne con valori Null.  
  
 I dati estratti dal file di dati XML vengono convertiti in un tipo di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tuttavia, l'origine XML non è in grado di convertire i dati XML nei tipi di dati DT_TIME2 o DT_DBTIMESTAMP2, in quanto l'origine non supporta tali tipi di dati. Per altre informazioni, vedere [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
 Lo schema inline o XSD può specificare il tipo di dati per gli elementi ma, in caso contrario, la finestra di dialogo **Editor origine XML** assegna il tipo di dati stringa Unicode (DT_WSTR) alla colonna dell'output che contiene l'elemento e imposta la lunghezza della colonna su 255 caratteri.  
  
 L'eventuale valore specificato nello schema relativo alla lunghezza massima di un elemento viene applicato alla lunghezza della colonna di output. Se la lunghezza massima è maggiore di quella supportata dal tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in cui l'elemento viene convertito, i dati vengono troncati al raggiungimento della lunghezza massima del tipo di dati. Se ad esempio la lunghezza di una stringa è 5000, la stringa verrà troncata a 4000 caratteri poiché tale è la lunghezza massima del tipo di dati DT_WSTR. Analogamente, i dati byte vengono troncati a 8000 caratteri, ovvero la lunghezza massima del tipo di dati DT_BYTES. Se nello schema non è specificata una lunghezza massima, la lunghezza predefinita delle colonne con qualsiasi tipo di dati è impostata su 255. Il troncamento dei dati nell'origine XML viene gestito con la stessa modalità di troncamento utilizzata in altri componenti del flusso di dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).  
  
 È possibile modificare sia il tipo di dati sia la lunghezza della colonna. Per altre informazioni, vedere [Tipi di dati di Integration Services](integration-services-data-types.md).  
  
## <a name="configuration-of-the-xml-source"></a>Configurazione dell'origine XML  
 L'origine XML supporta tre diverse modalità di accesso ai dati. è possibile specificare il percorso del file di dati XML, la variabile che contiene il percorso del file oppure la variabile che contiene i dati XML.  
  
 L'origine XML include le proprietà personalizzate `XMLData` e `XMLSchemaDefinition`, che possono essere aggiornate da espressioni di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate dell'origine XML](xml-source-custom-properties.md).  
  
 L'origine XML supporta più output regolari e più output degli errori.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include la finestra di dialogo **Editor origine XML**per la configurazione dell'origine XML. Questa finestra di dialogo è disponibile in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor origine XML** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor origine XML &#40;pagina Gestione connessione&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [Editor origine XML &#40;pagina Colonne&#41;](../xml-source-editor-columns-page.md)  
  
-   [Editor origine XML &#40;pagina Output degli errori&#41;](../xml-source-editor-error-output-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate dell'origine XML](xml-source-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostare le proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Estrarre i dati tramite l'origine XML](xml-source.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo [utilizzando un file XML per configurare un pacchetto SSIS](https://www.sqlshack.com/using-xml-file-configure-ssis-package/).  
  
  
