---
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
ms.openlocfilehash: 88754f7dbd0064c765314d88b0fcc0d06f05bbb2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763402"
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
  
|||  
|-|-|  
|[Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Proprietà Direction](../../../ado/reference/ado-api/direction-property.md)|
