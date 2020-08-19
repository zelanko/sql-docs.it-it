---
description: Proprietà Direction
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 37987e58829b1b6957b4fe1de440aaeb4aae1763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444053"
---
# <a name="direction-property"></a>Proprietà Direction
Indica se il [parametro](../../../ado/reference/ado-api/parameter-object.md) rappresenta un parametro di input, un parametro di output, un input e un parametro di output o se il parametro è il valore restituito da un stored procedure.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Direction** per specificare il modo in cui un parametro viene passato a o da una routine. La proprietà **Direction** è di lettura/scrittura; in questo modo è possibile lavorare con i provider che non restituiscono queste informazioni o per impostare queste informazioni quando non si desidera che ADO effettui una chiamata aggiuntiva al provider per recuperare le informazioni sui parametri.  
  
 Non tutti i provider possono determinare la direzione dei parametri nelle stored procedure. In questi casi, è necessario impostare la proprietà **Direction** prima di eseguire la query.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
