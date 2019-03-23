---
title: Percorsi in Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 832ea48478eb28b94caf292067344a3754040b2b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374719"
---
# <a name="integration-services-paths"></a>Percorsi in Integration Services
  Un percorso collega due componenti in un flusso di dati connettendo l'output di un componente all'input dell'altro. Un percorso ha un'origine e una destinazione. Se un percorso connette, ad esempio, un'origine OLE DB e una trasformazione Ordinamento, l'origine OLE DB costituirà l'origine del percorso e la trasformazione Ordinamento ne costituirà la destinazione. L'origine è il componente da cui inizia il percorso, mentre la destinazione è il componente in cui termina.  
  
 Se si esegue un pacchetto in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , è possibile visualizzare i dati in un flusso di dati collegando visualizzatori dati a un percorso. Un visualizzatore dati può essere configurato in modo da visualizzare i dati in una griglia. Si tratta di un utile strumento di debug. Per altre informazioni, vedere [Debug di un flusso di dati](../troubleshooting/debugging-data-flow.md).  
  
## <a name="configuration-of-the-path"></a>Configurazione del percorso  
 In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] è disponibile la finestra di dialogo **Editor percorso flusso di dati** che consente di impostare le proprietà di un percorso, visualizzare i metadati delle colonne di dati che passano attraverso il percorso e configurare i visualizzatori dati.  
  
 Le proprietà configurabili di un percorso includono nome, descrizione e annotazione. È possibile configurare i percorsi anche a livello di codice. Per altre informazioni, vedere [Connessione dei componenti del flusso di dati a livello di programmazione](../building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 L'annotazione di un percorso visualizza il nome dell'origine del percorso o il nome del percorso sull'area di progettazione della scheda **Flusso di dati** in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Le annotazioni dei percorsi sono simili a quelle che è possibile aggiungere a flussi di dati, flussi di controllo e gestori di eventi. L'unica differenza è costituita dal fatto che sono collegate a un percorso, mentre le altre annotazioni vengono visualizzate nelle schede **Flusso di dati**, **Flusso di controllo**e **Gestore evento**di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 I metadati indicano il nome, il tipo di dati, la precisione, la scala, la lunghezza, la tabella codici e il componente di origine di ogni colonna nell'output del componente precedente. Il componente di origine è il componente del flusso di dati che ha creato la colonna e può anche non essere il primo componente nel flusso di dati. Le trasformazioni Unione input multipli e Ordinamento, ad esempio, creano proprie colonne e costituiscono pertanto l'origine delle relative colonne di output. La trasformazione Copia colonna, invece, può passare colonne senza modificarle oppure creare nuove colonne copiando le colonne di input. La trasformazione Copia colonna costituisce il componente di origine solo per le nuove colonne.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor percorso flusso di dati**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor percorso flusso di dati &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor percorso flusso di dati &#40;pagina dei metadati&#41;](../data-flow-path-editor-metadata-page.md)  
  
-   [Editor percorso flusso di dati &#40;pagina visualizzatori dati&#41;](../data-flow-path-editor-data-viewers-page.md)  
  
 Per altre informazioni sulle proprietà che è possibile impostare a livello di programmazione, vedere [Proprietà del percorso](../path-properties.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Visualizzazione dei metadati dei percorsi nell'Editor percorso flusso di dati](../view-path-metadata-in-the-data-flow-path-editor.md)  
  
-   [Connettere componenti in un flusso di dati](connect-components-in-a-data-flow.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](data-flow.md)  
  
  
