---
title: Data Mining Extensions (DMX) di riferimento alle istruzioni | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a7a9c18599d13c4db510793a1d75c85bbb7a829
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070857"
---
# <a name="data-mining-extensions-dmx-statements"></a>Istruzioni DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Utilizzare i dati di data mining in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] prevede le attività principali seguenti:  
  
-   Creazione di strutture e modelli di data mining  
  
-   Elaborazione di strutture e modelli di data mining  
  
-   Eliminazione di strutture e modelli di data mining  
  
-   Copia di modelli di data mining  
  
-   Visualizzazione di modelli di data mining  
  
-   Generazione di stime basate su modelli di data mining  
  
 È possibile utilizzare istruzioni DMX (Data Mining Extensions) per eseguire tali attività a livello di programmazione.  
  
 Creazione di strutture e modelli di data mining  
 Usare la [Crea struttura di data MINING &#40;DMX&#41; ](../dmx/create-mining-structure-dmx.md) istruzione per aggiungere una nuova struttura di data mining a un database. È quindi possibile usare la [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) istruzione per aggiungere modelli di data mining alla struttura di data mining.  
  
 Usare la [CREATE MINING MODEL &#40;DMX&#41; ](../dmx/create-mining-model-dmx.md) istruzione per creare una nuova struttura di data mining associato e modello di data mining.  
  
 Elaborazione di strutture e modelli di data mining  
 Usare la [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) istruzione per elaborare una struttura di data mining e modello di data mining.  
  
 Eliminazione di strutture e modelli di data mining  
 Usare la [eliminare &#40;DMX&#41; ](../dmx/delete-dmx.md) istruzione per rimuovere tutti i dati con Training da un modello di data mining o una struttura di data mining. Usare la [DROP MINING STRUCTURE &#40;DMX&#41; ](../dmx/drop-mining-structure-dmx.md) oppure [DROP MINING MODEL &#40;DMX&#41; ](../dmx/drop-mining-model-dmx.md) istruzioni per rimuovere completamente una struttura di data mining o un modello di data mining da un database.  
  
 Copia di modelli di data mining  
 Usare la [SELECT INTO &#40;DMX&#41; ](../dmx/select-into-dmx.md) istruzione per copiare la struttura di un modello di data mining esistente in un nuovo modello di data mining e per eseguire il training del nuovo modello con gli stessi dati.  
  
 Visualizzazione di modelli di data mining  
 Usare la [selezionare &#40;DMX&#41; ](../dmx/select-dmx.md) istruzione per visualizzare le informazioni che l'algoritmo di data mining calcola e archivia il modello di data mining durante il training del modello. Simile a quello con [!INCLUDE[tsql](../includes/tsql-md.md)], è possibile utilizzare numerose clausole con l'istruzione SELECT, per estenderne le funzionalità. Tali clausole includono [DISTINCT FROM \<modello >](../dmx/select-distinct-from-model-dmx.md), [FROM \<modello >. CASI](../dmx/select-from-model-cases-dmx.md), [FROM \<modello >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [FROM \<modello >. CONTENUTO](../dmx/select-from-model-content-dmx.md) e [FROM \<modello >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Generazione di stime basate su modelli di data mining  
 Usare la [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) clausola dell'istruzione SELECT per creare stime basate su un modello di data mining esistente.  
  
 È anche possibile importare ed esportare modelli utilizzando il [importare &#40;DMX&#41; ](../dmx/import-dmx.md) e [ESPORTA &#40;DMX&#41; ](../dmx/export-dmx.md) istruzioni.  
  
 Queste attività rientrano in due categorie, istruzioni per la definizione dei dati e istruzioni per la manipolazione dei dati, descritte nella tabella seguente.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Istruzioni DMX &#40;Data Mining Extensions&#41; per la definizione dei dati](../dmx/dmx-statements-data-definition.md)|Fanno parte del linguaggio DDL (Data Definition Language). Consentono di definire un nuovo modello di data mining (incluso il training) o di eliminare un modello di data mining esistente da un database.|  
|[Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)|Fanno parte del linguaggio DML (Data Manipulation Language). Consentono di utilizzare modelli di data mining esistenti, eseguendo operazioni quali la visualizzazione di un modello o la creazione di stime.|  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
