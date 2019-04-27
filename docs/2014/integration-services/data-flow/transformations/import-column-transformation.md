---
title: Trasformazione Importa colonna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13deb9b423ce20fd77e0853cba9d0f205905ca44
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770407"
---
# <a name="import-column-transformation"></a>Trasformazione Importa colonna
  La trasformazione Importa colonna legge i dati dai file e li aggiunge alle colonne in un flusso di dati. Tramite questa trasformazione un pacchetto può aggiungere a un flusso di dati immagini e testo archiviati in file distinti. Un flusso di dati che carica dati in una tabella in cui sono archiviate informazioni sui prodotti può ad esempio includere la trasformazione Importa colonna per importare dai rispettivi file i commenti dei clienti su ogni prodotto e aggiungerli al flusso di dati.  
  
 Per configurare la trasformazione Importa colonna, procedere nel modo seguente:  
  
-   Specificare le colonne in cui devono essere aggiunti i dati.  
  
-   Specificare se la trasformazione prevede un indicatore dell'ordine dei byte.  
  
    > [!NOTE]  
    >  È previsto un indicatore dell'ordine dei byte solo se i dati sono di tipo DT_NTEXT.  
  
 I nomi dei file che contengono i dati si trovano in una colonna nell'input della trasformazione. Ogni riga nel set di dati può specificare un file diverso. Quando la trasformazione Importa colonna elabora una riga, legge il nome del file, apre il file corrispondente nel file system e ne carica il contenuto in una colonna di output. Il tipo di dati della colonna di output deve essere DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../integration-services-data-types.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
## <a name="configuration-of-the-import-column-transformation"></a>Configurazione della trasformazione Importa colonna  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Esporta colonna](export-column-transformation.md)   
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
