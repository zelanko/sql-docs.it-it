---
description: EXPORT (DMX)
title: EXPORT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 689ab632604d26a349dbb3f2a40d5f1b7cf8d702
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353227"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Estrae dal server un oggetto modello o struttura di data mining e lo salva in un file con estensione abf (Analysis Services Backup File).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argomenti  
 *tipo di oggetto*  
 Facoltativo. tipo di oggetto da esportare (modello di data mining o struttura di data mining).  
  
 *nome oggetto*  
 Facoltativo. Nome dell'oggetto da esportare.  
  
 *filename*  
 Nome e percorso del file da esportare, sotto forma di stringa.  
  
## <a name="remarks"></a>Osservazioni  
 Se l'istruzione specifica un modello di data mining, il file risultante conterrà anche la struttura di data mining associata. Se l'istruzione specifica **con dipendenze**, tutti gli oggetti necessari per l'elaborazione dell'oggetto, ad esempio l'origine dati e la vista origine dati, vengono inclusi nel file con estensione abf.  
  
 Per esportare o importare oggetti da un database, è necessario essere un amministratore del server o del database [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="export-mining-structure-example"></a>Esempio di esportazione di una struttura di data mining  
 Nell'esempio seguente vengono esportati in un percorso di file specifico il modello di data mining Association e le strutture Targeted Mailing e Forecasting. Poiché il modello Association fa parte della struttura di data mining Market Basket, nell'esempio viene esportata anche tale struttura. Tutti gli altri modelli di data mining che possono esistere come parte della struttura di data mining Market basket non verranno esportati, perché il modello di associazione è stato esportato utilizzando il **modello di data mining**, non la **struttura**di  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Esempio di esportazione di un modello di data mining  
 Nell'esempio seguente il modello di data mining Association viene esportato in un percorso di file specificato. Poiché l'istruzione specifica **con dipendenze**, anche gli oggetti origine dati e vista origine dati sono inclusi nel file con estensione abf.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [IMPORTA &#40;DMX&#41;](../dmx/import-dmx.md)   
 [Esportare e importare gli oggetti di data mining](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
