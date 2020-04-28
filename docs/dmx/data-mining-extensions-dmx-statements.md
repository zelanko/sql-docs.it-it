---
title: Guida di riferimento alle istruzioni DMX (Data Mining Extensions) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a7a9c18599d13c4db510793a1d75c85bbb7a829
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070857"
---
# <a name="data-mining-extensions-dmx-statements"></a>Istruzioni DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  L'utilizzo dei modelli di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] data mining in prevede le attività primarie seguenti:  
  
-   Creazione di strutture e modelli di data mining  
  
-   Elaborazione di strutture e modelli di data mining  
  
-   Eliminazione di strutture e modelli di data mining  
  
-   Copia di modelli di data mining  
  
-   Visualizzazione di modelli di data mining  
  
-   Generazione di stime basate su modelli di data mining  
  
 È possibile utilizzare istruzioni DMX (Data Mining Extensions) per eseguire tali attività a livello di programmazione.  
  
 Creazione di strutture e modelli di data mining  
 Utilizzare l'istruzione [create mining structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md) per aggiungere una nuova struttura di data mining a un database. È quindi possibile utilizzare l'istruzione [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) per aggiungere modelli di data mining alla struttura di data mining.  
  
 Utilizzare l'istruzione [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md) per compilare un nuovo modello di data mining e la struttura di data mining associata.  
  
 Elaborazione di strutture e modelli di data mining  
 Utilizzare l'istruzione [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) per elaborare una struttura di data mining e un modello di data mining.  
  
 Eliminazione di strutture e modelli di data mining  
 Utilizzare l'istruzione [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) per rimuovere tutti i dati sottoposti a training da un modello di data mining o una struttura di data mining. Per rimuovere completamente una struttura o un modello di data mining da un database, utilizzare la [struttura Drop mining &#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) o [drop Mining Model &#40;istruzioni DMX&#41;](../dmx/drop-mining-model-dmx.md) .  
  
 Copia di modelli di data mining  
 Utilizzare l'istruzione [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) per copiare la struttura di un modello di data mining esistente in un nuovo modello di data mining e per eseguire il training del nuovo modello con gli stessi dati.  
  
 Visualizzazione di modelli di data mining  
 Utilizzare l'istruzione [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) per visualizzare le informazioni calcolate e archiviate dall'algoritmo Data mining nel modello di data mining durante il training del modello. Analogamente a [!INCLUDE[tsql](../includes/tsql-md.md)], è possibile utilizzare più clausole con l'istruzione SELECT per estenderne la potenza. Queste clausole includono [Distinct da \<Model>](../dmx/select-distinct-from-model-dmx.md), [dal \<modello>. Case](../dmx/select-from-model-cases-dmx.md), [da \<Model>. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md) [dal \<modello>. CONTENUTO](../dmx/select-from-model-content-dmx.md) e [dal \<modello>. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Generazione di stime basate su modelli di data mining  
 Utilizzare la clausola [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) dell'istruzione SELECT per creare stime basate su un modello di data mining esistente.  
  
 È inoltre possibile importare ed esportare modelli utilizzando le istruzioni [import &#40;dmx&#41;](../dmx/import-dmx.md) ed [export &#40;DMX&#41;](../dmx/export-dmx.md) .  
  
 Queste attività rientrano in due categorie, istruzioni per la definizione dei dati e istruzioni per la manipolazione dei dati, descritte nella tabella seguente.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Istruzioni DMX &#40;Data Mining Extensions&#41; per la definizione dei dati](../dmx/dmx-statements-data-definition.md)|Fanno parte del linguaggio DDL (Data Definition Language). Consentono di definire un nuovo modello di data mining (incluso il training) o di eliminare un modello di data mining esistente da un database.|  
|[Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)|Fanno parte del linguaggio DML (Data Manipulation Language). Consentono di utilizzare modelli di data mining esistenti, eseguendo operazioni quali la visualizzazione di un modello o la creazione di stime.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
