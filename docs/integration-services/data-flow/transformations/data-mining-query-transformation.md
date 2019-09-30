---
title: Trasformazione Query di data mining | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e3b6783969376b20921d960e79c8909b5fda4aa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291462"
---
# <a name="data-mining-query-transformation"></a>Query di data mining - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Query di data mining esegue query di stima basate su modelli di data mining. Questa trasformazione contiene un generatore di query per la creazione di query DMX (Data Mining Extensions). Il generatore di query consente di creare istruzioni personalizzate per la valutazione dei dati di input della trasformazione in base a un modello di data mining esistente, utilizzando il linguaggio DMX. Per altre informazioni, vedere [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Una singola trasformazione può eseguire più query di stima, se i modelli sono compilati in base alla stessa struttura di data mining. Per altre informazioni, vedere [Data Mining Query Tools](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)(Strumenti query di data mining).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configurazione della trasformazione Query di data mining  
 La trasformazione Query di data mining usa una gestione connessione [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per connettersi al progetto di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o all'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] che contiene la struttura e i modelli di data mining. Per altre informazioni, vedere [Gestione connessione Analysis Services](../../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>Editor trasformazione Query di data mining (scheda Modello di data mining)
  Utilizzare la scheda **Modello di data mining** della finestra di dialogo **Editor trasformazione Query di data mining** per selezionare la struttura di data mining e i relativi modelli.  
  
### <a name="options"></a>Opzioni  
 **Connessione**  
 Consente di selezionare una connessione Analysis Services esistente usando la casella di riepilogo o di creare una nuova connessione usando il pulsante **Nuova** descritto di seguito.  
  
 **Nuova**  
 Consente di creare una connessione usando la finestra di dialogo **Aggiungi gestione connessione Analysis Services** .  
  
 **Struttura di data mining**  
 Consente di selezionare una struttura modello di data mining nell'elenco di strutture disponibili.  
  
 **Modelli di data mining**  
 Consente di visualizzare l'elenco dei modelli di data mining associati alla struttura di data mining selezionata.  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>Editor trasformazione Query di data mining (scheda Query)
  La scheda **Query** della finestra di dialogo **Editor trasformazione Query di data mining** consente di creare una query di stima.  
  
### <a name="options"></a>Opzioni  
 **Query di data mining**  
 Consente di digitare una query DMX direttamente nella casella di testo.  
  
 **Compila nuova query**  
 Fare clic su **Compila nuova query** per creare una query DMX tramite il generatore di query grafico.  
  
