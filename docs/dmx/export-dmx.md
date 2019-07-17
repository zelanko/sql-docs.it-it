---
title: ESPORTAZIONE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2cf3cf85b0efb024d65744f6eea0f5eea47ead83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074849"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Estrae dal server un oggetto modello o struttura di data mining e lo salva in un file con estensione abf (Analysis Services Backup File).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argomenti  
 *tipo di oggetto*  
 Facoltativo. il tipo di oggetto da esportare (modello di data mining o struttura di data mining).  
  
 *nome dell'oggetto*  
 Facoltativo. Nome dell'oggetto da esportare.  
  
 *filename*  
 Nome e percorso del file da esportare, sotto forma di stringa.  
  
## <a name="remarks"></a>Note  
 Se l'istruzione specifica un modello di data mining, il file risultante conterrà anche la struttura di data mining associata. Se l'istruzione specifica **WITH DEPENDENCIES**, tutti gli oggetti necessari per elaborare l'oggetto (ad esempio, l'origine dati e vista origine dati) sono inclusi nel file con estensione ABF.  
  
 È necessario essere un database o amministratore del server per esportare o importare oggetti da un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database.  
  
## <a name="export-mining-structure-example"></a>Esempio di esportazione di una struttura di data mining  
 Nell'esempio seguente vengono esportati in un percorso di file specifico il modello di data mining Association e le strutture Targeted Mailing e Forecasting. Poiché il modello Association fa parte della struttura di data mining Market Basket, nell'esempio viene esportata anche tale struttura. Altri modelli di data mining che potrebbero esistere come parte della struttura di data mining Market Basket non verrà esportati perché il modello Association viene esportato utilizzando **modello di data MINING**, non **struttura di data MINING**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Esempio di esportazione di un modello di data mining  
 Nell'esempio seguente il modello di data mining Association viene esportato in un percorso di file specificato. Poiché l'istruzione specifica **WITH DEPENDENCIES**, l'origine dati e oggetti vista origine dati sono inclusi anche nel file con estensione ABF.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTAZIONE &#40;DMX&#41;](../dmx/import-dmx.md)   
 [Esportare e importare gli oggetti di data mining](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
