---
title: Proprietà Direction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 244cf01b2845e7f5ef6729efd9ea7a7cfa6b994c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695412"
---
# <a name="direction-property"></a>Proprietà Direction
Indica se il [parametro](../../../ado/reference/ado-api/parameter-object.md) rappresenta un parametro di input, un parametro di output, input e un parametro di output o se il parametro è il valore restituito da una stored procedure.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valore.  
  
## <a name="remarks"></a>Note  
 Usare la **direzione** proprietà per specificare come un parametro viene passato a o da una procedura. Il **direzione** è di lettura/scrittura; in questo modo è possibile interagire con i provider che non restituiscono queste informazioni o per impostare queste informazioni quando non si desidera ADO per effettuare una chiamata aggiuntiva al provider per recuperare le informazioni sui parametri.  
  
 Non tutti i provider possono determinare la direzione dei parametri nella stored procedure. In questi casi, è necessario impostare il **direzione** proprietà prima di eseguire la query.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni ed esempio di proprietà direzione (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
