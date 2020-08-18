---
description: Informazioni sull'istruzione DMX Select
title: Informazioni sull'istruzione DMX SELECT | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 93744da59ad7149203da8fd14179045b63dc798f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395217"
---
# <a name="understanding-the-dmx-select-statement"></a>Informazioni sull'istruzione DMX Select
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  L'istruzione [Select](../dmx/select-dmx.md) costituisce la base per la maggior parte delle query create con DMX (Data Mining Extensions) in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Consente di eseguire diversi tipi di attività, ad esempio la visualizzazione di modelli di data mining o la stima basata su modelli di data mining.  
  
 Di seguito sono riportate le attività che è possibile completare utilizzando l'istruzione **Select** :  
  
-   Visualizzare un modello di data mining. La struttura di un modello è definita dal set di righe dello schema.  
  
-   Individuare i possibili valori di una colonna di un modello di data mining.  
  
-   Visualizzare i case assegnati ai nodi di un modello di data mining oppure ottenere un case rappresentativo.  
  
-   Creare stime utilizzando vari input.  
  
-   Copiare modelli di data mining.  
  
 Ognuna di queste attività usa un set di dati diverso, che chiameremo un dominio di *dati*. Il dominio dei dati viene definito nella clausola **from** dell'istruzione.  
  
-   Si desidera trovare gli oggetti nel modello di data mining stesso, ad esempio la regola con cui viene definito un set di dati, o una formula utilizzata per eseguire le stime.  
  
     In questo caso, è necessario esaminare i metadati archiviati nel modello stesso. Pertanto, il dominio dati sarà costituito dalle colonne del set di righe dello schema di data mining.  
  
-   Si desidera ottenere informazioni dettagliate dai case utilizzati per compilare il modello.  
  
     In questo caso, è necessario eseguire il drill-through nella struttura di data mining, vale a dire il dominio dati, ed esaminare le singole righe in colonne quali Gender, Bike Buyer e così via.  
  
 **Importante:** Qualsiasi elemento incluso nell'elenco di espressioni o nella clausola **where** deve provenire dal dominio di dati definito dalla clausola **from** . Non è possibile combinare i domini dati.  
  
##  <a name="select-types"></a><a name="Select_Types"></a> Selezione tipi  
 La sintassi dell'istruzione **Select** supporta molte attività diverse. Utilizzare i modelli seguenti per effettuare queste attività:  
  
-   [Stima](#Predicting)  
  
-   [Esplorazione](#Browsing)  
  
-   [Copia](#Copying)  
  
-   [Drill-through](#Drillthrough)  
  
###  <a name="predicting"></a><a name="Predicting"></a> Prevedere  
 È possibile eseguire stime basate su un modello di data mining utilizzando i tipi di query seguenti.  
  
 Nelle clausole **from** e **where** di un'istruzione **Select** di prediction join è possibile includere una qualsiasi delle istruzioni **Select** di esplorazione o stima.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELECT FROM [NATURAL] PREDICTION JOIN|Restituisce una stima creata unendo in join le colonne del modello di data mining alle colonne di un'origine dei dati interna.<br /><br /> Per questo tipo di query il dominio è costituito dalle colonne stimabili del modello e dalle colonne dell'origine dei dati di input.<br /><br /> [SELECT FROM &#60;Model&#62; PREDICtion JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Query di stima &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|SELEZIONA DA *\<model>*|Restituisce lo stato più probabile di una colonna stimabile, in base al solo modello di data mining. Questo tipo di query consente di creare rapidamente una stima con un PREDICTION JOIN vuoto.<br /><br /> Per questo tipo di query il dominio è costituito dalle colonne stimabili del modello.<br /><br /> [Selezionare da &#60;modello&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Query di stima &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Torna a Tipi di istruzioni SELECT](#Select_Types)  
  
###  <a name="browsing"></a><a name="Browsing"></a> Navigazione  
 È possibile visualizzare il contenuto di un modello di data mining utilizzando i tipi di query seguenti.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELEZIONARE DISTINCT FROM *\<model>*|Restituisce tutti i valori di stato dal modello di data mining per la colonna specificata.<br /><br /> Per questo tipo di query il dominio dati è costituito dal modello di data mining.<br /><br /> [Selezionare DISTINCT FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Query sul contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Selezionare da *\<model>* . CONTENUTO|Restituisce il contenuto che descrive il modello di data mining.<br /><br /> Per questo tipo di query il dominio dati è costituito dal set di righe dello schema relativo al contenuto.<br /><br /> [Selezionare da &#60;modello&#62;. CONTENUTO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Query sul contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Selezionare da *\<model>* . DIMENSION_CONTENT|Restituisce il contenuto che descrive il modello di data mining.<br /><br /> Per questo tipo di query il dominio dati è costituito dal set di righe dello schema relativo al contenuto.<br /><br /> [Selezionare da &#60;modello&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|Selezionare da *\<model>* . PMML|Restituisce la rappresentazione PMML (Predictive Model Markup Language) del modello di data mining, per gli algoritmi che supportano questa funzionalità.<br /><br /> Per questo tipo di query il dominio è costituito dal set di righe dello schema relativo alla rappresentazione PMML.<br /><br /> [Set di righe DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126283(v=sql.110))|  
  
 [Torna a Tipi di istruzioni SELECT](#Select_Types)  
  
###  <a name="copying"></a><a name="Copying"></a> Copia  
 È possibile copiare un modello di data mining e la struttura di data mining associata in un nuovo modello e, successivamente, rinominare il modello nell'istruzione.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELEZIONA IN *\<new model>*|Crea una copia del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Torna a Tipi di istruzioni SELECT](#Select_Types)  
  
###  <a name="drillthrough"></a><a name="Drillthrough"></a> Drillthrough  
 Tramite il tipo di query seguente è possibile visualizzare i case utilizzati per il training del modello oppure una rappresentazione di tali case.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|Selezionare da *\<model>* . CASI|Restituisce i case utilizzati per eseguire il training del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [Selezionare da &#60;modello&#62;. CASI &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Creare query drill-through tramite DMX](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|Selezionare da *\<model>* . SAMPLE_CASES|Restituisce un case di esempio, rappresentativo dei case utilizzati per eseguire il training del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [Selezionare da &#60;modello&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|Selezionare da *\<structure>* . CASI|Restituisce le righe di dati dettagliate dalla struttura di data mining sottostante, anche se alcuni dettagli non sono stati utilizzati per eseguire il training del modello di data mining.<br /><br /> [Selezionare una&#62; struttura &#60;. CASI](../dmx/select-from-structure-cases.md)<br /><br /> [Query drill-through &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Torna a Tipi di istruzioni SELECT](#Select_Types)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
