---
title: Origine file non elaborato | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfilesource.f1
- sql13.dts.designer.rawfilesourceconnectionmanager.f1
- sql13.dts.designer.rawfilesourcecolumns.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd61425f63f4124951c8c0c90c6c599292602c23
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916041"
---
# <a name="raw-file-source"></a>origine file non elaborato

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'origine file non elaborato legge i dati non elaborati da un file. Poiché la rappresentazione dei dati è nativa per l'origine, non è necessaria alcuna conversione e quasi nessuna analisi dei dati. Ciò significa che l'origine file non elaborato è in grado di leggere i dati più rapidamente rispetto ad altre origini, ad esempio l'origine file flat e l'origine OLE DB.  
  
 L'origine file non elaborato consente di recuperare dati non elaborati scritti in precedenza dalla destinazione file non elaborato. È anche possibile puntare l'origine file non elaborato a un file non elaborato vuoto in cui sono contenute solo le colonne (file di soli metadati). Si utilizza la destinazione file non elaborato per generare il file di soli metadati senza dover eseguire il pacchetto. Per altre informazioni, vedere [Destinazione file non elaborato](../../integration-services/data-flow/raw-file-destination.md).  
  
 Nel formato di file non elaborato sono contenute informazioni di ordinamento. Con la destinazione file non elaborato è possibile salvare tutte le informazioni di ordinamento in cui sono inclusi i flag di confronto per le colonne stringa. Con l'origine file non elaborato è possibile leggere e riconoscere le informazioni di ordinamento. È possibile configurare l'origine file non elaborato in modo da ignorare i flag di ordinamento nel file utilizzando l'editor avanzato. Per altre informazioni sui flag di confronto, vedere [Confronto di dati stringa](../../integration-services/data-flow/comparing-string-data.md).  
  
 Per configurare il file non elaborato è necessario specificare il nome del file che deve essere letto dall'origine file non elaborato.  
  
> [!NOTE]  
>  Questa origine non utilizza alcuna gestione connessione.  
  
 Questa origine include un solo output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-raw-file-source"></a>Configurazione dell'origine file non elaborato  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate del file non elaborato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà del componente, vedere [Impostare le proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Post di blog sugli [aspetti positivi dei file non elaborati](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)nel sito Web sqlservercentral.com.  
  
## <a name="raw-file-source-editor-connection-manager-page"></a>Editor origine file non elaborato (pagina Gestione connessione)
  L'origine file non elaborato legge i dati non elaborati da un file. Poiché la rappresentazione dei dati è nativa per l'origine, non è necessaria alcuna conversione e quasi nessuna analisi dei dati.   
## <a name="raw-file-source-editor-columns-page"></a>Editor origine file non elaborato (pagina Colonne)
  L'origine file non elaborato legge i dati non elaborati da un file. Poiché la rappresentazione dei dati è nativa per l'origine, non è necessaria alcuna conversione e quasi nessuna analisi dei dati.   
## <a name="see-also"></a>Vedere anche  
 [Destinazione file non elaborato](../../integration-services/data-flow/raw-file-destination.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
