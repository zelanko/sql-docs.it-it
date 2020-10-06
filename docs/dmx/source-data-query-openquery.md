---
description: '&lt;query sui dati &gt; di origine-OPENQUERY'
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 62d638b6b6028ffa861460e07f2283cb7380e129
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726108"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;query sui dati &gt; di origine-OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

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
  
## <a name="remarks"></a>Osservazioni  
 **OPENQUERY** fornisce un modo più sicuro per accedere ai dati esterni, supportando le autorizzazioni dell'origine dati. Poiché la stringa di connessione viene archiviata nell'origine dati, gli amministratori possono utilizzare le proprietà dell'origine dati per gestire l'accesso ai dati. Per ulteriori informazioni sulle origini dati, vedere [origini dati supportate &#40;SSAS-&#41;multidimensionale ](/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional).  
  
 È possibile ottenere un elenco delle origini dati disponibili in un server eseguendo una query sul set di righe dello schema **MDSCHEMA_INPUT_DATASOURCES** . Per ulteriori informazioni sull'utilizzo di **MDSCHEMA_INPUT_DATASOURCES**, vedere [MDSCHEMA_INPUT_DATASOURCES set di righe](/previous-versions/sql/sql-server-2012/ms126243(v=sql.110)).  
  
 È inoltre possibile restituire un elenco di origini dati del database di Analysis Services corrente mediante la seguente query DMX:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'origine dati MyDS già definita nel [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database per creare una connessione al [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] database ed eseguire una query sulla vista **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#60;query sui dati di origine&#62;](../dmx/source-data-query.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
