---
title: Destinazione file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledest.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30f8f566dc04726076dd9eb7c4d91b56f687218d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62902446"
---
# <a name="flat-file-destination"></a>file flat - destinazione
  La destinazione file flat scrive dati in un file di testo che può essere in formato delimitato, a larghezza fissa, a larghezza fissa con delimitatore di riga o non allineato a destra.  
  
 Per configurare la destinazione file flat, procedere nel modo seguente:  
  
-   Specificare un blocco di testo inserito nel file prima di iniziare a scrivere i dati. Il testo può ad esempio contenere le intestazioni delle colonne.  
  
-   Specificare se sovrascrivere i dati eventualmente presenti in un file di destinazione con lo stesso nome.  
  
 Per accedere al file di testo, questa destinazione utilizza una gestione connessione file flat. Impostando le proprietà della gestione connessione file flat utilizzata dalla destinazione file flat è possibile specificare la modalità con cui la destinazione file flat deve formattare e scrivere il file di testo. Durante la configurazione della gestione connessione file flat si specificano informazioni sul file e sulle singole colonne nel file. È ad esempio possibile specificare i caratteri che delimitano le righe e le colonne del file, oltre al tipo di dati e alla lunghezza di ogni colonna. Per ulteriori informazioni, vedere [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 La destinazione file flat include la proprietà personalizzata Header, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate del file flat](flat-file-custom-properties.md).  
  
 Questa destinazione include un solo output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configurazione della destinazione file flat  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor origine file flat**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione file flat &#40;pagina Gestione connessione&#41;](../flat-file-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione file flat &#40;pagina Mapping&#41;](../flat-file-destination-editor-mappings-page.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../common-properties.md)  
  
-   [Proprietà personalizzate del file flat](flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà di un componente del flusso di dati, vedere [Impostazione delle proprietà di un componente del flusso di dati](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Origine file flat](flat-file-source.md)   
 [Flusso di dati](data-flow.md)  
  
  
