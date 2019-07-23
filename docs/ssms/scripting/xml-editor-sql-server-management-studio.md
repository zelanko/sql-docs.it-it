---
title: Editor XML (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.editor.xml.f1
- sql13.swb.editorxml.f1
- vs.xmleditor
- sql13.swb.xmleditor.f1
helpviewer_keywords:
- XML Designer [SQL Server Management Studio]
ms.assetid: 0824a5ce-e67b-4b53-98d9-d371faf2d23c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9b82bec0f3def57ac575b4e338e437c05f0bbd1
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252824"
---
# <a name="xml-editor-sql-server-management-studio"></a>Editor XML (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Offre una serie di strumenti visivi per utilizzare gli XML Schema, i set di dati ADO.NET e i documenti XML. Progettazione XML supporta il linguaggio XML Schema Definition (XSD) definito dal World Wide Web Consortium (WC3). Lo strumento di progettazione non supporta le definizioni DTD (Document Type Definitions) o altri linguaggi XML Schema, ad esempio XDR (XML-Data Reduced).  
  
 Per visualizzare Progettazione XML, aggiungere un set di dati, un XML Schema o un file XML a un progetto o aprire uno dei tipi di file descritti nella tabella seguente.  
  
> [!CAUTION]  
>  Il comando **Annulla** non è disponibile nella visualizzazione schema. Pianificare quindi accuratamente il lavoro e salvare spesso i file.  
  
 Per consentire di lavorare sui file XML, sugli XML Schema e sui set di dati, Progettazione XML dispone delle tre visualizzazioni (o modalità) seguenti:  
  
|Vista|Descrizione|Tipi di file supportati|  
|----------|-----------------|--------------------------|  
|**Schema**|Per la creazione e la modifica in modo visivo degli XML Schema e dei set di dati ADO.NET.|xsd|  
|**Dati**|Per la modifica in modo visivo dei file di dati XML in una griglia dati strutturata.|xml|  
|**XML**|Per le modifiche XML, l'editor di origine dispone di codifica a colori e di IntelliSense, che include le funzionalità Completa parola ed Elenca membri.|xml, xsd, xslt, wsdl, web, resx, tdl, wsf, hta, disco, vsdisco e config|  
|**Showplan**|Consente di visualizzare i piani di query xml creati utilizzando l'opzione SET SHOWPLAN_XML ON.|showplan|  
  
## <a name="schema-view"></a>Visualizzazione schema  
 La visualizzazione schema offre una rappresentazione visiva degli elementi, degli attributi, dei tipi e così via che compongono gli XML Schema e i set di dati ADO.NET.  
  
 Nella visualizzazione schema è possibile creare schemi e set di dati trascinando gli elementi dalla scheda XML Schema della casella degli strumenti o da Esplora server e rilasciandoli sulla superficie di progettazione. È inoltre possibile aggiungere elementi allo strumento di progettazione facendo clic con il pulsante destro del mouse sulla superficie di progettazione e scegliendo Aggiungi dal menu di scelta rapida.  
  
 Nella visualizzazione schema è possibile:  
  
-   Creare e modificare XML Schema e set di dati ADO.NET esistenti  
  
-   Creare e modificare relazioni tra le tabelle  
  
-   Creare e modificare le chiavi  
  
-   Generare set di dati ADO.NET da XML Schema  
  
> [!NOTE]  
>  Il layout degli elementi nella visualizzazione schema viene memorizzato nel file xsx che può essere visualizzato facendo clic su **Mostra tutti i file** sulla barra degli strumenti Esplora soluzioni e quindi espandendo il file xsd. Se non viene visualizzato alcun file xsx, significa che il file xsd non è mai stato aperto in Progettazione XML.  
  
### <a name="customizing-schema-view"></a>Personalizzazione della visualizzazione schema  
 Le caratteristiche seguenti consentono di modificare il layout visivo degli elementi nella visualizzazione schema.  
  
-   Zoom  
  
-   Espansione o compressione degli elementi nidificati  
  
-   Disposizione automatica del layout degli elementi  
  
-   Reimpostazione dello stato predefinito degli elementi compressi  
  
##### <a name="to-expand-hidden-nested-elements"></a>Per visualizzare gli elementi nidificati nascosti  
  
-   Fare clic sull'icona con il segno più alla base dell'elemento.  
  
##### <a name="to-collapse-nested-elements"></a>Per comprimere gli elementi nidificati  
  
-   Fare clic sull'icona con il segno meno sull'elemento di livello più basso che si desidera visualizzare in Progettazione XML.  
  
## <a name="data-view"></a>Vista dati  
 La visualizzazione dati dispone di una griglia dati che può essere utilizzata per modificare i file xml. Nella visualizzazione dati è possibile modificare solo il contenuto di un file XML, ma non i tag e la struttura.  
  
 La visualizzazione dati contiene due aree separate: **Tabelle dati** e **Dati**. L'area **Tabelle dati** è un elenco di relazioni definite nel file XML nello stesso ordine di annidamento (dalla più esterna alla più interna). L'area **Dati** è una griglia dati che visualizza i dati sulla base della selezione eseguita nell'area Tabelle dati.  
  
> [!NOTE]  
>  I file XML appena creati non contengono alcun dato e quindi non possono essere visualizzati nella visualizzazione dati. Esistono inoltre alcuni casi di documenti XML la cui visualizzazione dati non può essere attivata. Benché il codice XML possa essere considerato valido, se non è costituito da dati strutturati, quando si tenta di passare alla visualizzazione dati verrà restituito il messaggio seguente: "Anche se il documento XML ha un formato corretto, contiene una struttura non visualizzabile in Visualizzazione dati".  
  
 Nella visualizzazione dati è possibile:  
  
-   Popolare manualmente le tabelle di dati  
  
-   Modificare le tabelle di dati esistenti  
  
-   Generare un XML Schema da un documento XML  
  
## <a name="xml-view"></a>Visualizzazione XML  
 La visualizzazione XML dispone di un editor per modificare il codice XML non formattato e dispone inoltre di IntelliSense e della codifica a colori. Quando si lavora su file xsd e xml associati a uno schema è disponibile il completamento delle istruzioni. Digitare < per iniziare un tag. Verrà presentato un elenco di elementi validi presso quella posizione. Dopo avere digitato il nome dell'elemento e premuto la barra spaziatrice verrà visualizzato un elenco di attributi supportati dall'elemento.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense non sono disponibili sulla barra degli strumenti. Per accedere alle opzioni, nell'editor XML scegliere **IntelliSense** dal menu **Modifica**.  
  
## <a name="showplan-view"></a>Visualizzazione SHOWPLAN  
 I piani di query possono essere salvati in formato XML quando vengono creati con l'opzione SET SHOWPLAN_XML ON. Per aprire il piano di query, fare doppio clic su un file con estensione showplan.  
  
## <a name="see-also"></a>Vedere anche  
 [Salvare un piano di esecuzione in formato XML](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
