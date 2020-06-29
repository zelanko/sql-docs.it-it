---
title: Trasformazione Esporta colonna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2914c6a23a326f4d312c2784eaad2b84fdad0b0e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430648"
---
# <a name="export-column-transformation"></a>Trasformazione Esporta colonna
  La trasformazione Esporta colonna legge dati in un flusso di dati e li inserisce in un file. Se ad esempio il flusso di dati contiene informazioni sui prodotti, ad esempio l'immagine di ogni prodotto, è possibile utilizzare la trasformazione Esporta colonna per salvare tali immagini in uno o più file.  
  
## <a name="append-and-truncate-options"></a>Opzioni Accoda e tronca  
 Nella tabella seguente vengono descritti gli effetti delle impostazioni delle opzioni relative all'accodamento e al troncamento sui risultati.  
  
|Accoda|Truncate|File esistente|Risultati|  
|------------|--------------|-----------------|-------------|  
|False|False|No|La trasformazione crea un nuovo file e vi scrive i dati.|  
|True|False|No|La trasformazione crea un nuovo file e vi scrive i dati.|  
|False|True|No|La trasformazione crea un nuovo file e vi scrive i dati.|  
|True|True|No|La trasformazione non supera la convalida in fase di progettazione. Non è consentito impostare su `true` entrambe le proprietà.|  
|False|False|Sì|Viene generato un errore di run-time. Il file esiste ma la trasformazione non è in grado di scrivervi.|  
|False|True|Sì|La trasformazione elimina e ricrea il file e vi scrive i dati.|  
|True|False|Sì|La trasformazione apre il file e scrive i dati alla fine.|  
|True|True|Sì|La trasformazione non supera la convalida in fase di progettazione. Non è consentito impostare su `true` entrambe le proprietà.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configurazione della trasformazione Esporta colonna  
 Per configurare la trasformazione Esporta colonna, procedere nel modo seguente:  
  
-   Specificare le colonne di dati e le colonne contenenti i percorsi dei file in cui scrivere i dati.  
  
-   Specificare se durante l'operazione di inserimento dei dati in file esistenti i dati vengono troncati o accodati.  
  
-   Specificare se scrivere un indicatore dell'ordine dei byte nel file.  
  
    > [!NOTE]  
    >  L'indicatore dell'ordine dei byte viene scritto solo se i dati non vengono accodati a un file esistente e hanno tipo di dati DT_NTEXT.  
  
 La trasformazione utilizza coppie di colonne di input: una contenente un nome di file e una contenente i dati. Ogni riga nel set di dati può specificare un file diverso. A mano a mano che la trasformazione elabora una riga, i dati vengono inseriti nel file specificato. In fase di esecuzione la trasformazione crea i file, se non esistono ancora, e quindi vi scrive i dati. I dati da scrivere devono avere tipo di dati DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../integration-services-data-types.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Esportazione colonna**, vedere [Editor trasformazione Esportazione colonna &#40;pagina Colonne&#41;](../../export-column-transformation-editor-columns-page.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [proprietà personalizzate della trasformazione](transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
  
