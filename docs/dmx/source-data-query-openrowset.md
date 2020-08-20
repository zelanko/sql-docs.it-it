---
description: '&lt;query sui dati &gt; di origine-OPENROWSET'
title: OPENROWSET (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8da3686e7772b7e997690d509c8092917635497a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500776"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;query sui dati &gt; di origine-OPENROWSET
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Sostituisce la query sui dati dell'origine con una query su un provider esterno. Le istruzioni INSERT, SELECT FROM PREDICtion JOIN e SELECT FROM NATURAL PREDICtion JOIN supportano **OPENROWSET**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>Argomenti  
 *provider_name*  
 Nome di un provider OLE DB.  
  
 *provider_string*  
 Stringa di connessione OLE DB per il provider specificato.  
  
 *query_syntax*  
 Sintassi di una query che restituisce un set di righe.  
  
## <a name="remarks"></a>Osservazioni  
 Il provider data mining stabilirà una connessione all'oggetto origine dati utilizzando *provider_name* e *provider_string* ed eseguirà la query specificata in *query_syntax* per recuperare il set di righe dai dati di origine.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente può essere utilizzato in un'istruzione PREDICTION JOIN per recuperare dati dal database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] tramite un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] di tipo SELECT.  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#60;query sui dati di origine&#62;](../dmx/source-data-query.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
