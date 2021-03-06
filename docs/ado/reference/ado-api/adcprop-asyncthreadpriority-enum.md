---
description: ADCPROP_ASYNCTHREADPRIORITY_ENUM
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e01a004ded0b6ed3151ba28c747d3ea245462f92
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976872"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Per un oggetto [Recordset](./recordset-object-ado.md) RDS, specifica la priorità di esecuzione del thread asincrono che recupera i dati.  
  
 Utilizzare queste costanti con la proprietà dinamica "**priorità thread in background**" del **Recordset** , a cui viene fatto riferimento nell'indice della proprietà dinamica ADO-to-OLE DB e documentato nel [servizio Microsoft Cursor per OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentazione.  
  
|Costante|Valore|Descrizione|  
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