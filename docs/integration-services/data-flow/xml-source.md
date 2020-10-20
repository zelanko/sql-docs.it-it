---
description: Origine XML
title: Origine XML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.xmlsource.f1
- sql13.dts.designer.xmlsourceadapter.connectionmanager.f1
- sql13.dts.designer.xmlsourceadapter.columns.f1
- sql13.dts.designer.xmlsourceadapter.erroroutput.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c066add73dbc8049f389c828363f1157bb39edae
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194555"
---
# <a name="xml-source"></a>Origine XML

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
 I dati estratti dal file di dati XML vengono convertiti in un tipo di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tuttavia, l'origine XML non è in grado di convertire i dati XML nei tipi di dati DT_TIME2 o DT_DBTIMESTAMP2, in quanto l'origine non supporta tali tipi di dati. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Lo schema inline o XSD può specificare il tipo di dati per gli elementi ma, in caso contrario, la finestra di dialogo **Editor origine XML** assegna il tipo di dati stringa Unicode (DT_WSTR) alla colonna dell'output che contiene l'elemento e imposta la lunghezza della colonna su 255 caratteri.  
  
 L'eventuale valore specificato nello schema relativo alla lunghezza massima di un elemento viene applicato alla lunghezza della colonna di output. Se la lunghezza massima è maggiore di quella supportata dal tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in cui l'elemento viene convertito, i dati vengono troncati al raggiungimento della lunghezza massima del tipo di dati. Se ad esempio la lunghezza di una stringa è 5000, la stringa verrà troncata a 4000 caratteri poiché tale è la lunghezza massima del tipo di dati DT_WSTR. Analogamente, i dati byte vengono troncati a 8000 caratteri, ovvero la lunghezza massima del tipo di dati DT_BYTES. Se nello schema non è specificata una lunghezza massima, la lunghezza predefinita delle colonne con qualsiasi tipo di dati è impostata su 255. Il troncamento dei dati nell'origine XML viene gestito con la stessa modalità di troncamento utilizzata in altri componenti del flusso di dati. Per altre informazioni, vedere [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md).  
  
 È possibile modificare sia il tipo di dati sia la lunghezza della colonna. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="configuration-of-the-xml-source"></a>Configurazione dell'origine XML  
 L'origine XML supporta tre diverse modalità di accesso ai dati. è possibile specificare il percorso del file di dati XML, la variabile che contiene il percorso del file oppure la variabile che contiene i dati XML.  
  
 L'origine XML include le proprietà personalizzate **XMLData** e **XMLSchemaDefinition** , che possono essere aggiornate da espressioni di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate dell'origine XML](../../integration-services/data-flow/xml-source-custom-properties.md).  
  
 L'origine XML supporta più output regolari e più output degli errori.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include la finestra di dialogo **Editor origine XML**per la configurazione dell'origine XML. Questa finestra di dialogo è disponibile in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](./set-the-properties-of-a-data-flow-component.md)  
  
-   [Proprietà personalizzate dell'origine XML](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="xml-source-editor-connection-manager-page"></a>Editor origine XML (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** di **Editor origine XML** per specificare un file XML e il file XSD che trasforma i dati XML.  
  
### <a name="static-options"></a>Opzioni statiche  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|Percorso file XML|Consente di recuperare i dati da un file XML.|  
|File XML da variabile|Consente di specificare il nome del file XML in una variabile.<br /><br /> **Informazioni correlate**: [Uso di variabili nei pacchetti](../integration-services-ssis-variables.md)|  
|Dati XML da variabile|Consente di recuperare i dati XML da una variabile.|  
  
 **Usa schema inline**  
 Consente di specificare se i dati di origine XML contengono lo schema XSD che ne definisce e ne convalida la struttura e i dati.  
  
 **Percorso XSD**  
 Consente di digitare il percorso e il nome del file dello schema XSD o di individuare il file selezionando **Sfoglia**.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file di schema XSD.  
  
 **Genera XSD**  
 Usare la finestra di dialogo **Salva con nome** per selezionare un percorso per il file di schema XSD creato automaticamente. L'editor deduce lo schema dalla struttura dei dati XML.  
  
### <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
#### <a name="data-access-mode--xml-file-location"></a>Modalità di accesso ai dati = Percorso file XML  
 **Percorso XML**  
 Consente di digitare il percorso e il nome del file di dati XML o di individuare il file scegliendo **Sfoglia**.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file di dati XML.  
  
#### <a name="data-access-mode--xml-file-from-variable"></a>Modalità di accesso ai dati = File XML da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il percorso e il nome del file XML.  
  
#### <a name="data-access-mode--xml-data-from-variable"></a>Modalità di accesso ai dati = Dati XML da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente i dati XML.  
  
## <a name="xml-source-editor-columns-page"></a>Editor origine XML (pagina Colonne)
  Usare il nodo **Colonne** della finestra di dialogo **Editor origine XML** per eseguire il mapping tra una colonna di output e una colonna (di origine) esterna.  
  
### <a name="options"></a>Opzioni  
 **Colonne esterne disponibili**  
 Consente di visualizzare l'elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne.  
  
 **Colonna esterna**  
 Consente di visualizzare le colonne esterne (origine) nell'ordine in cui verranno lette dall'attività. È possibile modificare l'ordine deselezionando innanzitutto le colonne selezionate nella tabella visualizzata nell'editor e quindi selezionando le colonne esterne nell'elenco secondo un ordine diverso.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="xml-source-editor-error-output-page"></a>Editor origine XML (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor origine XML** per selezionare le opzioni di gestione degli errori e impostare le proprietà delle colonne di output degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (di origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine XML**.  
  
 **Error (Errore) (Error (Errore)e)**  
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
  
## <a name="related-tasks"></a>Attività correlate  
 [Estrazione dei dati tramite l'origine XML](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)