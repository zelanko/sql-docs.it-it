---
title: IMPORTAZIONE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2141a4f8ccc6e34ec3010ad3ce8e8e3789d09132
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892751"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carica nel server un modello o una struttura di data mining da un file con estensione abf (Analysis Services Backup File).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argomenti  
 *filename*  
 Stringa contenente il nome e il percorso del file da importare.  
  
## <a name="remarks"></a>Osservazioni  
 Se non è specificato alcun oggetto, verrà caricato tutto il contenuto del file con estensione dmb. Se il file con estensione dmb include un database che non esiste sul server, il database verrà creato.  
  
 Per esportare o importare oggetti è necessario essere un amministratore del server o del database.  
  
## <a name="import-from-file-example"></a>Esempio di importazione da file  
 Nell'esempio seguente viene importato nel server corrente l'intero contenuto del file contenente la struttura e il modello di associazione.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [ESPORTA &#40;DMX&#41;](../dmx/export-dmx.md)   
 [Esportare e importare gli oggetti di data mining](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
