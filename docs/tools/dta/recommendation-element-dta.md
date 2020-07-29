---
title: Elemento Recommendation (DTA)
description: Nell'utilità dta l'elemento Recommendation contiene informazioni sugli indici ipotetici che fanno parte di una configurazione specificata dall'utente.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 188d23afaabd31fa09d47ebed54ae7dbf952d376
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729583"
---
# <a name="recommendation-element-dta"></a>Elemento Recommendation (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Contiene informazioni sugli indici ipotetici che fanno parte di una configurazione specificata dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|No.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. Può essere usato una volta per ogni elemento **Table** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Table per Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**Elementi figlio**|[Elemento Create &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> Elemento **Drop**. Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Osservazioni  
 Questo elemento appartiene al nome **RecommendationTypecomplexType** nell'XML Schema dell'Ottimizzazione guidata motore di database. Viene utilizzato per specificare indici per una configurazione ipotetica. Non confondere l'elemento **Recommendation** con altri tipi che possono essere usati per specificare il partizionamento (**RecommendationPType**) o le visualizzazioni (**RecommendationViewType**). Per informazioni su questi altri tipi di elemento **Recommendation** , vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
