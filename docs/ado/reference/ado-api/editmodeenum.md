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
manager: jroth
ms.openlocfilehash: d98e6d27de571bc799cc8442fbe6ef9debc0beaa
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695243"
---
# <a name="editmodeenum"></a>EditModeEnum
Specifica lo stato di modifica di un record.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica che nessuna operazione di modifica è in corso.|  
|**adEditInProgress**|1|Indica che i dati presenti nel record corrente sono stati modificati ma non salvati.|  
|**adEditAdd**|2|Indica che il [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) chiamata al metodo e il record corrente nel buffer di copia è un nuovo record che non è stato salvato nel database.|  
|**adEditDelete**|4|Indica che il record corrente è stato eliminato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)
