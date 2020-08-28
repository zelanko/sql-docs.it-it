---
description: EditModeEnum
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e10479aca06eab4a7aa5215f0016dd1f82eab1c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973852"
---
# <a name="editmodeenum"></a>EditModeEnum
Specifica lo stato di modifica di un record.  
  
|Costante|Valore|Descrizione|  
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
