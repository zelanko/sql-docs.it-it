---
description: Proprietà CommandType (ADO)
title: Proprietà CommandType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: rothja
ms.author: jroth
ms.openlocfilehash: 435e2c0562abcccbb6ec6e139491af280e976cfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450813"
---
# <a name="commandtype-property-ado"></a>Proprietà CommandType (ADO)
Indica il tipo di un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce uno o più valori [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) .  
  
> [!NOTE]
>  Non usare i valori **CommandTypeEnum** di **adCmdFile** o **adCmdTableDirect** con **CommandType**. Questi valori possono essere usati solo come opzioni con i metodi [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Osservazioni  
 Usare la proprietà **CommandType** per ottimizzare la valutazione della proprietà [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) .  
  
 Se il valore della proprietà **CommandType** è impostato sul valore predefinito **adCmdUnknown**, è possibile che si verifichi un calo delle prestazioni perché ADO deve effettuare chiamate al provider per determinare se la proprietà **CommandText** è un'istruzione SQL, un stored procedure o un nome di tabella. Se si sa quale tipo di comando si sta usando, l'impostazione della proprietà **CommandType** indica a ADO di passare direttamente al codice pertinente. Se la proprietà **CommandType** non corrisponde al tipo di comando nella proprietà **CommandText** , si verifica un errore quando si chiama il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
