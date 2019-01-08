---
title: La comprensione di DMX Select-istruzione | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f76729b419fccf3d17e66ddd8ab00e8b54b1b264
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398074"
---
# <a name="understanding-the-dmx-select-statement"></a>Informazioni sull'istruzione DMX Select
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Il [selezionate](../dmx/select-dmx.md) istruzione costituisce la base per la maggior parte delle query create con Data Mining Extensions (DMX) nel [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Consente di eseguire diversi tipi di attività, ad esempio la visualizzazione di modelli di data mining o la stima basata su modelli di data mining.  
  
 Di seguito sono le attività che è possibile completare tramite la **seleziona** istruzione:  
  
-   Visualizzare un modello di data mining. La struttura di un modello è definita dal set di righe dello schema.  
  
-   Individuare i possibili valori di una colonna di un modello di data mining.  
  
-   Visualizzare i case assegnati ai nodi di un modello di data mining oppure ottenere un case rappresentativo.  
  
-   Creare stime utilizzando vari input.  
  
-   Copiare modelli di data mining.  
  
 Ognuna di queste attività viene utilizzato un diverso set di dati, che chiameremo una *dominio dati*. Si definisce il dominio dei dati nel **FROM** clausola dell'istruzione.  
  
-   Si desidera trovare gli oggetti nel modello di data mining stesso, ad esempio la regola con cui viene definito un set di dati, o una formula utilizzata per eseguire le stime.  
  
     In questo caso, è necessario esaminare i metadati archiviati nel modello stesso. Pertanto, il dominio dati sarà costituito dalle colonne del set di righe dello schema di data mining.  
  
-   Si desidera ottenere informazioni dettagliate dai case utilizzati per compilare il modello.  
  
     In questo caso, è necessario eseguire il drill-through nella struttura di data mining, vale a dire il dominio dati, ed esaminare le singole righe in colonne quali Gender, Bike Buyer e così via.  
  
 **IMPORTANTE:** Tutti gli elementi inclusi nell'elenco dell'espressione o nel **in cui** clausola deve appartenere al dominio dati definito dalle **FROM** clausola. Non è possibile combinare i domini dati.  
  
##  <a name="Select_Types"></a> Selezionare i tipi  
 La sintassi del **seleziona** istruzione supporta molte attività diverse. Utilizzare i modelli seguenti per effettuare queste attività:  
  
-   [Stima](#Predicting)  
  
-   [Esplorazione](#Browsing)  
  
-   [Copia](#Copying)  
  
-   [Drill-through](#Drillthrough)  
  
###  <a name="Predicting"></a> Stima  
 È possibile eseguire stime basate su un modello di data mining utilizzando i tipi di query seguenti.  
  
 È possibile includere uno di visualizzazione o stima **selezionate** istruzioni all'interno di **FROM** e **in cui** clausole di un prediction join **selezionare** istruzione.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELECT FROM [NATURAL] PREDICTION JOIN|Restituisce una stima creata unendo in join le colonne del modello di data mining alle colonne di un'origine dei dati interna.<br /><br /> Per questo tipo di query il dominio è costituito dalle colonne stimabili del modello e dalle colonne dell'origine dei dati di input.<br /><br /> [SELECT FROM &#60;modello&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Query di stima &#40;Data Mining&#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
|SELECT FROM  *\<modello >*|Restituisce lo stato più probabile di una colonna stimabile, in base al solo modello di data mining. Questo tipo di query consente di creare rapidamente una stima con un PREDICTION JOIN vuoto.<br /><br /> Per questo tipo di query il dominio è costituito dalle colonne stimabili del modello.<br /><br /> [SELECT FROM &#60;modello&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Query di stima &#40;Data Mining&#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
  
 [Selezionare i tipi di informazioni al](#Select_Types)  
  
###  <a name="Browsing"></a> Esplorazione  
 È possibile visualizzare il contenuto di un modello di data mining utilizzando i tipi di query seguenti.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELECT DISTINCT FROM  *\<modello >*|Restituisce tutti i valori di stato dal modello di data mining per la colonna specificata.<br /><br /> Per questo tipo di query il dominio dati è costituito dal modello di data mining.<br /><br /> [SELECT DISTINCT FROM &#60;modello &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Query sul contenuto &#40;Data mining&#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<modello >*. CONTENUTO|Restituisce il contenuto che descrive il modello di data mining.<br /><br /> Per questo tipo di query il dominio dati è costituito dal set di righe dello schema relativo al contenuto.<br /><br /> [SELECT FROM &#60;modello&#62;. CONTENUTO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Query sul contenuto &#40;Data mining&#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<modello >*. DIMENSION_CONTENT|Restituisce il contenuto che descrive il modello di data mining.<br /><br /> Per questo tipo di query il dominio dati è costituito dal set di righe dello schema relativo al contenuto.<br /><br /> [SELECT FROM &#60;modello&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|SELECT FROM  *\<modello >*. PMML|Restituisce la rappresentazione PMML (Predictive Model Markup Language) del modello di data mining, per gli algoritmi che supportano questa funzionalità.<br /><br /> Per questo tipo di query il dominio è costituito dal set di righe dello schema relativo alla rappresentazione PMML.<br /><br /> [Set di righe DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|  
  
 [Selezionare i tipi di informazioni al](#Select_Types)  
  
###  <a name="Copying"></a> Copia  
 È possibile copiare un modello di data mining e la struttura di data mining associata in un nuovo modello e, successivamente, rinominare il modello nell'istruzione.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELECT INTO  *\<nuovo modello >*|Crea una copia del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [SELECT INTO &AMP;#40;DMX&AMP;#41;](../dmx/select-into-dmx.md)|  
  
 [Selezionare i tipi di informazioni al](#Select_Types)  
  
###  <a name="Drillthrough"></a> Drill-through  
 Tramite il tipo di query seguente è possibile visualizzare i case utilizzati per il training del modello oppure una rappresentazione di tali case.  
  
|Tipo di query|Descrizione|  
|----------------|-----------------|  
|SELECT FROM  *\<modello >*. CASE|Restituisce i case utilizzati per eseguire il training del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [SELECT FROM &#60;modello&#62;. I casi &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Creare query drill-through tramite DMX](../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)|  
|SELECT FROM  *\<modello >*. SAMPLE_CASES|Restituisce un case di esempio, rappresentativo dei case utilizzati per eseguire il training del modello di data mining.<br /><br /> Per questo tipo di query il dominio è costituito dal modello di data mining.<br /><br /> [SELECT FROM &#60;modello&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|SELECT FROM  *\<struttura >*. CASE|Restituisce le righe di dati dettagliate dalla struttura di data mining sottostante, anche se alcuni dettagli non sono stati utilizzati per eseguire il training del modello di data mining.<br /><br /> [SELECT FROM &#60;struttura&#62;. CASE](../dmx/select-from-structure-cases.md)<br /><br /> [Query drill-through &#40;Data Mining&#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)|  
  
 [Selezionare i tipi di informazioni al](#Select_Types)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
