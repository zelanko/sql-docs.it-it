---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: rothja
ms.author: jroth
ms.openlocfilehash: 909fd5a292f5f071ec287aba9c8e3f6dc3881ef3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763362"
---
# <a name="persistformatenum"></a>PersistFormatEnum
Specifica il formato in cui salvare un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica il formato Microsoft Advanced Data TableGram (ADTG).|  
|**adPersistADO**|1|Indica che verrà utilizzato il formato di Extensible Markup Language (XML) di ADO. Questo valore è uguale a adPersistXML ed è incluso per la compatibilità con le versioni precedenti.|  
|**adPersistXML**|1|Indica Extensible Markup Language formato (XML).|  
|**adPersistProviderSpecific**|2|Indica che il provider rende permanente il **Recordset** utilizzando il relativo formato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. PersistFormat. ADTG|  
|AdoEnums. PersistFormat. XML|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
