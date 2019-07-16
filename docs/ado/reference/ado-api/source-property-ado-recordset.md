---
title: Proprietà (Recordset ADO) dell'origine | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930924"
---
# <a name="source-property-ado-recordset"></a>Proprietà Source (Recordset - ADO)
Indica l'origine dati per un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Set di un **stringa** valore oppure [comando](../../../ado/reference/ado-api/command-object-ado.md) riferimento; oggetto restituisce solo un **stringa** valore che indica l'origine del **Recordset**.  
  
## <a name="remarks"></a>Note  
 Usare la **origine** proprietà per specificare un'origine dati per un **Recordset** dell'oggetto usando uno dei seguenti: una **comando** dell'oggetto variabile, un'istruzione SQL, una stored procedure, o un nome di tabella.  
  
 Se si imposta la **origine** proprietà a un **comando** oggetto, il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà del **Recordset** oggetto erediterà il valore di **ActiveConnection** proprietà per l'oggetto specificato **comando** oggetto. Tuttavia, la lettura il **origine** proprietà non restituisce un **comando** dell'oggetto; al contrario, restituisce il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà del **comando** dell'oggetto per cui impostare il **origine** proprietà.  
  
 Se il **origine** è un'istruzione SQL, una stored procedure o un nome di tabella, è possibile ottimizzare le prestazioni passando appropriato *opzioni* argomento con il [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)chiamata al metodo.  
  
 Il **origine** proprietà è di lettura/scrittura per chiuso **Recordset** oggetti e read-only per aprire **Recordset** oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Source (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Proprietà Source (Record ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
