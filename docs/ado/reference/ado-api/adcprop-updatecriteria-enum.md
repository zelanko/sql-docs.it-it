---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12d960e8fcd5e1f27ea8198ce52e080f6fddf7c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921411"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
Specifica i campi che è possibile utilizzare per rilevare i conflitti durante un aggiornamento ottimistico di una riga dell'origine dati con un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
 Utilizzare queste costanti con la proprietà dinamica "**criteri di aggiornamento**" del **Recordset** , a cui viene fatto riferimento nell' [indice della proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentato nel [servizio Microsoft Cursor per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentazione.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Rileva i conflitti se è stata modificata una colonna della riga dell'origine dati.|  
|**adCriteriaKey**|0|Rileva i conflitti se la colonna chiave della riga dell'origine dati è stata modificata, il che significa che la riga è stata eliminata.|  
|**adCriteriaTimeStamp**|3|Rileva i conflitti se il timestamp della riga dell'origine dati è stato modificato, il che significa che è stato eseguito l'accesso alla riga dopo che il **Recordset** è stato ottenuto.|  
|**adCriteriaUpdCols**|2|Rileva i conflitti se una delle colonne della riga dell'origine dati che corrispondono ai campi aggiornati del **Recordset** è stata modificata.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. AdcPropUpdateCriteria. ALLCOLS|  
|AdoEnums. AdcPropUpdateCriteria. KEY|  
|AdoEnums. AdcPropUpdateCriteria. TIMESTAMP|  
|AdoEnums. AdcPropUpdateCriteria. UPDCOLS|
