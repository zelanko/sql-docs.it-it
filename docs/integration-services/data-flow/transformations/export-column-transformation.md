---
title: Trasformazione Esporta colonna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exportcolumntrans.f1
- sql13.dts.designer.fileextractortransformation.columns.f1
- sql13.dts.designer.fileextractortransformation.errorhandling.f1
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
ms.openlocfilehash: 52acb1db548f6425dcfaf6339d38a4b55e57b76e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297950"
---
# <a name="export-column-transformation"></a>Trasformazione Esporta colonna

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Esporta colonna legge dati in un flusso di dati e li inserisce in un file. Se ad esempio il flusso di dati contiene informazioni sui prodotti, ad esempio l'immagine di ogni prodotto, è possibile utilizzare la trasformazione Esporta colonna per salvare tali immagini in uno o più file.  
  
## <a name="append-and-truncate-options"></a>Opzioni Accoda e tronca  
 Nella tabella seguente vengono descritti gli effetti delle impostazioni delle opzioni relative all'accodamento e al troncamento sui risultati.  
  
|Accoda|Troncamento|File esistente|Risultati|  
|------------|--------------|-----------------|-------------|  
|False|False|no|La trasformazione crea un nuovo file e vi scrive i dati.|  
|True|False|no|La trasformazione crea un nuovo file e vi scrive i dati.|  
|False|True|no|La trasformazione crea un nuovo file e vi scrive i dati.|  
|True|True|no|La trasformazione non supera la convalida in fase di progettazione. Non è consentito impostare su **true**entrambe le proprietà.|  
|False|False|Sì|Viene generato un errore di run-time. Il file esiste ma la trasformazione non è in grado di scrivervi.|  
|False|True|Sì|La trasformazione elimina e ricrea il file e vi scrive i dati.|  
|True|False|Sì|La trasformazione apre il file e scrive i dati alla fine.|  
|True|True|Sì|La trasformazione non supera la convalida in fase di progettazione. Non è consentito impostare su **true**entrambe le proprietà.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Configurazione della trasformazione Esporta colonna  
 Per configurare la trasformazione Esporta colonna, procedere nel modo seguente:  
  
-   Specificare le colonne di dati e le colonne contenenti i percorsi dei file in cui scrivere i dati.  
  
-   Specificare se durante l'operazione di inserimento dei dati in file esistenti i dati vengono troncati o accodati.  
  
-   Specificare se scrivere un indicatore dell'ordine dei byte nel file.  
  
    > [!NOTE]  
    >  L'indicatore dell'ordine dei byte viene scritto solo se i dati non vengono accodati a un file esistente e hanno tipo di dati DT_NTEXT.  
  
 La trasformazione usa coppie di colonne di input: una colonna contiene un nome di file e l'altra colonna contiene i dati. Ogni riga nel set di dati può specificare un file diverso. A mano a mano che la trasformazione elabora una riga, i dati vengono inseriti nel file specificato. In fase di esecuzione la trasformazione crea i file, se non esistono ancora, e quindi vi scrive i dati. I dati da scrivere devono avere tipo di dati DT_TEXT, DT_NTEXT o DT_IMAGE. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="export-column-transformation-editor-columns-page"></a>Editor trasformazione Esportazione colonna (pagina Colonne)
  Utilizzare la pagina **Colonne** della finestra di dialogo **Editor trasformazione Esportazione colonna** per specificare le colonne nel flusso di dati da estrarre in file. È possibile indicare se la trasformazione Esporta colonna deve accodare i dati a un file oppure sovrascrivere un file esistente.  
  
### <a name="options"></a>Opzioni  
 **Colonna estrazione**  
 Consente di eseguire una selezione dall'elenco di colonne di input contenenti dati di tipo text o image. In tutte le righe devono essere presenti definizioni per **Colonna estrazione** e **Colonna percorso file**.  
  
 **Colonna percorso file**  
 Consente di eseguire una selezione dall'elenco di colonne di input contenenti nomi e percorsi di file. In tutte le righe devono essere presenti definizioni per **Colonna estrazione** e **Colonna percorso file**.  
  
 **Consenti accodamento**  
 Consente di indicare se la trasformazione accoderà i dati ai file esistenti. Il valore predefinito è **false**.  
  
 **Forza troncamento**  
 Consente di indicare se la trasformazione eliminerà il contenuto di file esistenti prima di scrivere i dati. Il valore predefinito è **false**.  
  
 **Scrivi indicatore ordine byte**  
 Consente di specificare se scrivere un indicatore ordine byte (BOM) nel file. L'indicatore dell'ordine dei byte viene scritto solo se i dati hanno il tipo di dati **DT_NTEXT** o DT_WSTR e non sono accodati a un file di dati esistente.  
  
## <a name="export-column-transformation-editor-error-output-page"></a>Editor trasformazione Esportazione colonna (pagina Output degli errori)
  Utilizzare la pagina **Output degli errori** della finestra di dialogo **Editor trasformazione Esportazione colonna** per specificare le opzioni di gestione degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'output. Fare clic sul nome per espandere la visualizzazione e includere le colonne.  
  
 **Colonna**  
 Consente di visualizzare le colonne di output selezionate nella pagina **Colonne** della finestra di dialogo **Editor trasformazione Esportazione colonna** .  
  
 **Errore**  
 Consente di specificare l'azione che deve essere eseguita in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere l'esecuzione del componente.  
  
 **Troncamento**  
 Consente di specificare l'azione da eseguire in caso di troncamenti, ovvero ignorare l'errore, reindirizzare la riga o interrompere l'esecuzione del componente.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'operazione.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
  
