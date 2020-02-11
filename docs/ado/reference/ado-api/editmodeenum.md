---
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c4ddb27bbc6831095062af5491fb501b6d5b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933040"
---
# <a name="editmodeenum"></a>EditModeEnum
Specifica lo stato di modifica di un record.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica che non è in corso alcuna operazione di modifica.|  
|**adEditInProgress**|1|Indica che i dati nel record corrente sono stati modificati, ma non salvati.|  
|**adEditAdd**|2|Indica che il metodo [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) è stato chiamato e che il record corrente nel buffer di copia è un nuovo record che non è stato salvato nel database.|  
|**adEditDelete**|4|Indica che il record corrente è stato eliminato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. EditMode. NONE|  
|AdoEnums. EditMode. InProgress|  
|AdoEnums. EditMode. ADD|  
|AdoEnums. EditMode. DELETE|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)
