---
title: Proprietà Source (errore ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b55ebbe5a167b7d70cf606fc4e37e7ede36b486
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916907"
---
# <a name="source-property-ado-error"></a>Proprietà Source (Error - ADO)
Indica il nome dell'oggetto o dell'applicazione che ha generato originariamente un errore.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **stringa** che indica il nome di un oggetto o di un'applicazione.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **source** in un oggetto [Error](../../../ado/reference/ado-api/error-object.md) per determinare il nome dell'oggetto o dell'applicazione che ha generato originariamente un errore. Potrebbe trattarsi del nome della classe o dell'ID a livello di codice dell'oggetto. Per gli errori in ADO, il valore della proprietà sarà **ADODB.** _ObjectName_, dove *nomeoggetto* è il nome dell'oggetto che ha generato l'errore. Per ADOX e ADO MD, il valore sarà **ADOX.** _ObjectName_ e **ADOMD.** _ObjectName_, rispettivamente.  
  
 In base alla documentazione degli errori delle proprietà di **origine**, [numero](../../../ado/reference/ado-api/number-property-ado.md)e [Descrizione](../../../ado/reference/ado-api/description-property.md) degli oggetti **errore** , è possibile scrivere codice che gestirà l'errore in modo appropriato.  
  
 La proprietà di **origine** è di sola lettura per gli oggetti **Error** .  
  
## <a name="applies-to"></a>Si applica a  
 [Error (oggetto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description (proprietà)](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, proprietà di filelima](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Proprietà Source (record ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Proprietà Source (Recordset ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
