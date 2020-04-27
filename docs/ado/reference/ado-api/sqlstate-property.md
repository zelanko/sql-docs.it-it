---
title: Proprietà SQLState | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e43ace17f3f2b709c327f185a189a107b6b73065
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916881"
---
# <a name="sqlstate-property"></a>Proprietà SQLState
Indica lo stato SQL per un determinato oggetto [Error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **stringa** di cinque caratteri che segue lo standard ANSI SQL e indica il codice di errore.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **SQLSTATE** per leggere il codice di errore di cinque caratteri restituito dal provider quando si verifica un errore durante l'elaborazione di un'istruzione SQL. Ad esempio, quando si utilizza il provider Microsoft OLE DB per ODBC con un database Microsoft SQL Server, i codici di errore dello stato SQL provengono da ODBC, basati su errori specifici di ODBC o sugli errori che hanno origine da Microsoft SQL Server e vengono quindi mappati a errori ODBC. Questi codici di errore sono documentati nello standard ANSI SQL, ma possono essere implementati in modo diverso da origini dati diverse.  
  
## <a name="applies-to"></a>Si applica a  
 [Error (oggetto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
