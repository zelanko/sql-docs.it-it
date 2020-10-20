---
description: Trasformazione Importa colonna
title: Trasformazione Importa colonna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.importcolumntrans.f1
helpviewer_keywords:
- Import Column transformation [Integration Services]
- columns [Integration Services], importing
- importing data, SSIS packages
- inserting data
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 538077633c5eb6716dc632d9635e13f92d2421b4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194133"
---
# <a name="import-column-transformation"></a>Trasformazione Importa colonna

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Importa colonna legge i dati dai file e li aggiunge alle colonne in un flusso di dati. Tramite questa trasformazione un pacchetto può aggiungere a un flusso di dati immagini e testo archiviati in file distinti. Un flusso di dati che carica dati in una tabella in cui sono archiviate informazioni sui prodotti può ad esempio includere la trasformazione Importa colonna per importare dai rispettivi file i commenti dei clienti su ogni prodotto e aggiungerli al flusso di dati.  
  
 Per configurare la trasformazione Importa colonna, procedere nel modo seguente:  
  
-   Specificare le colonne in cui devono essere aggiunti i dati.  
  
-   Specificare se la trasformazione prevede un indicatore dell'ordine dei byte.  
  
    > [!NOTE]  
    >  È previsto un indicatore dell'ordine dei byte solo se i dati sono di tipo DT_NTEXT.  
  
 I nomi dei file che contengono i dati si trovano in una colonna nell'input della trasformazione. Ogni riga nel set di dati può specificare un file diverso. Quando la trasformazione Importa colonna elabora una riga, legge il nome del file, apre il file corrispondente nel file system e ne carica il contenuto in una colonna di output. Il tipo di dati della colonna di output deve essere DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
## <a name="configuration-of-the-import-column-transformation"></a>Configurazione della trasformazione Importa colonna  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Esporta colonna](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
