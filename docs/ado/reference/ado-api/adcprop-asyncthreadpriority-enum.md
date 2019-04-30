---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0b9d4e0e6f844ef2dda18e95aadfcf3b910995d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065305"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Per un RDS [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, specifica la priorità di esecuzione del thread asincrona che recupera i dati.  
  
 Utilizzare queste costanti con il **Recordset** "**priorità del Thread in Background**" proprietà dinamiche, che viene fatto riferimento nell'indice per ADO, OLE DB proprietà dinamica e documentate nel [ Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentazione.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Imposta la priorità tra normale e più elevato.|  
|**adPriorityBelowNormal**|2|Imposta la priorità tra più basso e normale.|  
|**adPriorityHighest**|5|Imposta la priorità più elevata possibile.|  
|**AdPriorityLowest**|1|Imposta la priorità per il livello minimo possibile.|  
|**adPriorityNormal**|3|Imposta la priorità normale.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
