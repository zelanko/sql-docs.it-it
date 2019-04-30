---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6612a90b94f10bdd08441d7814a7137121659045
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316003"
---
# <a name="commandtype-property-ado"></a>Proprietà CommandType (ADO)
Indica il tipo di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce uno o più [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valori.  
  
> [!NOTE]
>  Non usare la **CommandTypeEnum** i valori di **adCmdFile** oppure **adCmdTableDirect** con **CommandType**. Questi valori possono essere usati solo come opzioni con il [aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) metodi di una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Note  
 Usare la **CommandType** per ottimizzare la valutazione della proprietà il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà.  
  
 Se il **CommandType** valore della proprietà è impostato sul valore predefinito, **adCmdUnknown**, si potrebbe effetti negativi sulle prestazioni poiché ADO debba effettuare chiamate al provider per determinare se il  **CommandText** proprietà è un'istruzione SQL, una stored procedure o un nome di tabella. Se si conosce il tipo di comando in uso, impostando il **CommandType** proprietà indica ad ADO per passare direttamente al codice pertinente. Se il **CommandType** proprietà non corrisponde al tipo di comando nelle **CommandText** proprietà di un errore si verifica quando si chiama il [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) (metodo).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni ed esempio di proprietà direzione (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
