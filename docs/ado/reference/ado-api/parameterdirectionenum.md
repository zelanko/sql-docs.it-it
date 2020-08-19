---
description: ParameterDirectionEnum
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: rothja
ms.author: jroth
ms.openlocfilehash: 8c586b4e7ce2e18411d147e8aafb4eb144e01e6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442783"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Specifica se il [parametro](../../../ado/reference/ado-api/parameter-object.md) rappresenta un parametro di input, un parametro di output, un parametro di input e un parametro di output o il valore restituito da un stored procedure.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Valore predefinito. Indica che il parametro rappresenta un parametro di input.|  
|**adParamInputOutput**|3|Indica che il parametro rappresenta un parametro di input e di output.|  
|**adParamOutput**|2|Indica che il parametro rappresenta un parametro di output.|  
|**adParamReturnValue**|4|Indica che il parametro rappresenta un valore restituito.|  
|**adParamUnknown**|0|Indica che la direzione del parametro è sconosciuta.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ParameterDirection. INPUT|  
|AdoEnums. ParameterDirection. INPUTOUTPUT|  
|AdoEnums. ParameterDirection. OUTPUT|  
|AdoEnums. ParameterDirection. RETURNVALUE|  
|AdoEnums. ParameterDirection. UNKNOWN|  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Proprietà Direction](../../../ado/reference/ado-api/direction-property.md)  
    :::column-end:::
:::row-end:::
