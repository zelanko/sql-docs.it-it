---
title: Proprietà Source (recordset ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f6ac84445272ae3657d4e25691dbbf150f32c5d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930924"
---
# <a name="source-property-ado-recordset"></a>Proprietà Source (Recordset - ADO)
Indica l'origine dati per un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta un valore **stringa** o un riferimento all'oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) ; restituisce solo un valore **stringa** che indica l'origine del **Recordset**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **source** per specificare un'origine dati per un oggetto **Recordset** utilizzando uno dei seguenti elementi: una variabile oggetto **comando** , un'istruzione SQL, un stored procedure o un nome di tabella.  
  
 Se si imposta la **proprietà Source** su un oggetto **Command** , la proprietà [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) dell'oggetto **Recordset** erediterà il valore della proprietà **ActiveConnection** per l'oggetto **comando** specificato. Tuttavia, la lettura della proprietà **source** non restituisce un oggetto **Command** ; Restituisce invece la proprietà [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) dell'oggetto **Command** a cui si imposta la proprietà **source** .  
  
 Se la proprietà **source** è un'istruzione SQL, un stored procedure o un nome di tabella, è possibile ottimizzare le prestazioni passando l'argomento *options* appropriato con la chiamata al metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) .  
  
 La proprietà di **origine** è in lettura/scrittura per gli oggetti **Recordset** chiusi e in sola lettura per gli oggetti **Recordset** aperti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Source (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Proprietà Source (Record - ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
