---
title: Colonne corrispondenti Data Quality (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ecbbaba1441fa150daaecbfcbc7cbdf65636de55
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482645"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Colonne corrispondenti Data Quality (componente aggiuntivo MDS per Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]dopo avere verificato la corrispondenza dei dati, nel gruppo **Data Quality** sulla barra multifunzione è possibile fare clic su **Mostra dettagli** per visualizzare le colonne con informazioni dettagliate sulla corrispondenza.  
  
 Nella tabella seguente vengono illustrate le colonne visualizzate quando si verifica la corrispondenza dei dati.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|**CLUSTER_ID**|Identificatore univoco utilizzato per raggruppare record simili. Il valore di **CLUSTER_ID**è lo stesso per tutte le righe simili. Se non è visualizzato alcun valore **CLUSTER_ID** per una riga, non sono stati trovati record simili.|  
|**RECORD_ID**|Identificatore univoco utilizzato per identificare i record. Simile al valore Codice archiviato nel repository MDS, è un valore utilizzato per identificare un record. Viene generato automaticamente ogni volta che viene eseguita la ricerca della corrispondenza.|  
|**PIVOT_MARK**|Record arbitrario con cui vengono confrontati gli altri record. Non dispone di un valore di punteggio.|  
|**Punteggio**|Rappresenta il livello di analogia dei record del gruppo con il record pivot. Il punteggio è determinato da DQS. Se non viene visualizzato alcun punteggio, il record rappresenta il pivot per gli altri record oppure non è stata trovata alcuna corrispondenza.|  
  
## <a name="see-also"></a>Vedi anche  
 [Corrispondenza Data Quality nel Componente aggiuntivo MDS per Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Corrisponde a dati simili &#40;Componente aggiuntivo MDS per Excel&#41;](match-similar-data-mds-add-in-for-excel.md)   
 [Corrispondenza di dati](../../data-quality-services/data-matching.md)  
  
  
