---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 624fa1976792a700342a114f82aa5ca6b75c70ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931566"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Specifica gli attributi di un oggetto [Proprietà](../../../ado/reference/ado-api/property-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica che la proprietà non è supportata dal provider.|  
|**adPropRequired**|1|Indica che l'utente deve specificare un valore per questa proprietà prima dell'inizializzazione dell'origine dati.|  
|**adPropOptional**|2|Indica che l'utente non deve specificare un valore per questa proprietà prima dell'inizializzazione dell'origine dati.|  
|**adPropRead**|512|Indica che l'utente può leggere la proprietà.|  
|**adPropWrite**|1024|Indica che l'utente può impostare la proprietà.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. PropertyAttributes. NOTSUPPORTED|  
|AdoEnums. PropertyAttributes. REQUIRED|  
|AdoEnums. PropertyAttributes. OPTIONAL|  
|AdoEnums. PropertyAttributes. READ|  
|AdoEnums. PropertyAttributes. WRITE|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
