---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d8e3b85f3d18b25f9dda1ef4f442ec0822257fae
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670028"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;query sui dati &gt; di origine-OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sostituisce la query sui dati dell'origine con una query su un'origine dei dati esistente. Le istruzioni INSERT, SELECT FROM PREDICtion JOIN e SELECT FROM NATURAL PREDICtion join supportano **OPENQUERY**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argomenti  
 *origine dati denominata*  
 Origine dati esistente nel [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database.  
  
 *sintassi di query*  
 Sintassi di una query che restituisce un set di righe.  
  
## <a name="remarks"></a>Commenti  
 **OPENQUERY** fornisce un modo più sicuro per accedere ai dati esterni, supportando le autorizzazioni dell'origine dati. Poiché la stringa di connessione viene archiviata nell'origine dati, gli amministratori possono utilizzare le proprietà dell'origine dati per gestire l'accesso ai dati. Per ulteriori informazioni sulle origini dati, vedere [origini dati supportate &#40;SSAS-&#41;multidimensionale ](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional).  
  
 È possibile ottenere un elenco delle origini dati disponibili in un server eseguendo una query sul set di righe dello schema **MDSCHEMA_INPUT_DATASOURCES** . Per ulteriori informazioni sull'utilizzo di **MDSCHEMA_INPUT_DATASOURCES**, vedere [MDSCHEMA_INPUT_DATASOURCES set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset).  
  
 È inoltre possibile restituire un elenco di origini dati del database di Analysis Services corrente mediante la seguente query DMX:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente viene utilizzata l'origine dati MyDS già definita nel [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database per creare una connessione al [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] database ed eseguire una query sulla vista **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#60;query sui dati di origine&#62;](../dmx/source-data-query.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
