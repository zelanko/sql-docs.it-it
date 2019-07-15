---
title: Elemento server per Configuration (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 276af9a4703d70a930d39e06cb4ad21e2d56c9e2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733474"
---
# <a name="server-element-for-configuration-dta"></a>Elemento Server per Configuration (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contiene le informazioni per l'identificazione del server in cui si desidera che Ottimizzazione guidata motore di database esegua la valutazione della configurazione ipotetica indicata dall'elemento **Configuration** ).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Richiesto una volta per l'elemento **Configuration** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Configuration &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
|**Elementi figlio**|[Elemento Name per Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Elemento Database per Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 È possibile specificare solo un elemento **Server** per l'elemento **Configuration** . Questo elemento appartiene al Name **ServerTypecomplexType** nell' [XML Schema dell'ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100). Non si deve confondere questo elemento **Server** con l'elemento figlio di **DTAInput**. Per altre informazioni, vedere [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
