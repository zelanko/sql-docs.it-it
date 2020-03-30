---
title: Destinazione Training modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f064ad734e90d2748b959e7fdc9d5868b22c25cf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293115"
---
# <a name="data-mining-model-training-destination"></a>Training modello di data mining - destinazione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione Training modello di data mining consente di eseguire il training dei modelli di data mining passando i dati ricevuti dalla destinazione agli algoritmi dei modelli di data mining. È possibile eseguire il training di più modelli di data mining con una singola destinazione, se i modelli sono compilati in base alla stessa struttura di data mining. Per altre informazioni, vedere [Colonne della struttura di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-structure-columns) e [Colonne del modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>Configurazione della destinazione Training modello di data mining  
 Se una colonna livello case della struttura di destinazione e i modelli compilati sulla struttura presentano il tipo di contenuto KEY TIME o KEY SEQUENCE, i dati di input devono essere ordinati in base a questa colonna. I modelli compilati utilizzando l'algoritmo Microsoft Time Series, ad esempio, hanno tipo di contenuto KEY TIME. Se i dati di input non sono ordinati, non sarà possibile elaborare il modello. Se sono necessari dati ordinati, sarà possibile inserire una trasformazione Ordinamento in un punto precedente del flusso di dati per ordinare i dati. Questo non è vale per le colonne con tipo di contenuto KEY. Per altre informazioni, vedere [Tipi di contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining) e [Trasformazione ordinamento](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
> [!NOTE]  
>  L'input della destinazione Training modello di data mining deve essere ordinato. Per ordinare i dati è possibile includere una trasformazione Ordinamento in un punto a monte della destinazione Training modello di data mining nel flusso di dati. Per altre informazioni, vedere [Trasformazione ordinamento](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
 Questa destinazione include un input e nessun output.  
  
 La destinazione Training modello di data mining usa una gestione connessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene la struttura e i modelli di data mining di cui eseguire il training. Per altre informazioni, vedere [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate della destinazione Training modello di data mining](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>Editor training modelli di data mining (scheda Connessione)
  Utilizzare la pagina **Connessione** della finestra di dialogo **Editor training modelli di data mining** per selezionare un modello di mining per cui eseguire il training.  
  
### <a name="options"></a>Opzioni  
 **Connection manager**  
 Selezionare una connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente dall'elenco oppure creare una nuova connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando il pulsante **Nuova** descritto di seguito.  
  
 **Nuovo**  
 Consente di creare una connessione usando la finestra di dialogo **Aggiungi gestione connessione Analysis Services** .  
  
 **Struttura di data mining**  
 Selezionare una struttura di data mining dall'elenco di quelle disponibili oppure creare una nuova struttura facendo clic su **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova struttura e un nuovo modello di data mining mediante la **Creazione guidata modello di data mining**.  
  
 **Modelli di data mining**  
 Consente di visualizzare l'elenco dei modelli di data mining associati alla struttura di data mining selezionata.  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>Editor training modelli di data mining (scheda Colonne)
  Utilizzare la pagina **Colonne** della finestra di dialogo **Editor training modelli di data mining** per eseguire il mapping tra le colonne di input e le colonne della struttura di data mining.  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Trascinare le colonne di input per eseguirne il mapping alle colonne della struttura di data mining.  
  
 **Colonne della struttura di data mining**  
 Consente di visualizzare l'elenco delle colonne della struttura di data mining. Trascinare le colonne della struttura di data mining per eseguirne il mapping alle colonne di input disponibili.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate nella tabella precedente. Per modificare o eliminare una selezione di mapping, utilizzare l'elenco **Colonne di input disponibili**.  
  
 **Colonne della struttura di data mining**  
 Consente di visualizzare tutte le colonne di destinazione disponibili, indipendentemente dal fatto che ne venga eseguito il mapping.  
  
