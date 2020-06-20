---
title: Elemento Recommendation (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
ms.openlocfilehash: ebb2d9fc4e6c060aaee348297ab1732ffb2eb2a9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040292"
---
# <a name="recommendation-element-dta"></a>Elemento Recommendation (DTA)
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
|**Occorrenza**|Facoltativa. È possibile utilizzarlo una volta per ogni elemento `Table`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Table per Schema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**Elementi figlio**|[Elemento Create &#40;DTA&#41;](create-element-dta.md)<br /><br /> Elemento `Drop`. Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Osservazioni  
 Questo elemento appartiene al nome **RecommendationTypecomplexType** nell'XML Schema dell'Ottimizzazione guidata motore di database. Viene utilizzato per specificare indici per una configurazione ipotetica. Questo elemento `Recommendation` non deve essere confuso con altri tipi che è possibile utilizzare per specificare il partizionamento (`RecommendationPType`) o le viste (`RecommendationViewType`). Per informazioni su questi altri `Recommendation` tipi di elemento, vedere l' [XML Schema di ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
