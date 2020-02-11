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
ms.openlocfilehash: 22a8cd4bb8d1bdddbaaa68e92349d9c728557ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921461"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Per un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) RDS, specifica la priorità di esecuzione del thread asincrono che recupera i dati.  
  
 Utilizzare queste costanti con la proprietà dinamica "**priorità thread in background**" del **Recordset** , a cui viene fatto riferimento nell'indice della proprietà dinamica ADO-to-OLE DB e documentato nel [servizio Microsoft Cursor per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentazione.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Imposta la priorità tra il normale e il massimo.|  
|**adPriorityBelowNormal**|2|Imposta la priorità tra il minimo e il normale.|  
|**adPriorityHighest**|5|Imposta la priorità sul massimo possibile.|  
|**AdPriorityLowest**|1|Imposta la priorità sul più basso possibile.|  
|**adPriorityNormal**|3|Imposta la priorità su Normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. massimo|  
|AdoEnums. AdcPropAsyncThreadPriority. minor|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|
