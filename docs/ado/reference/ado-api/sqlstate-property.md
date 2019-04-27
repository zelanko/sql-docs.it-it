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
manager: craigg
ms.openlocfilehash: 00ab80a10b2c7c411cee0fb6061467d67cfbd4a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740361"
---
# <a name="sqlstate-property"></a>Proprietà SQLState
Indica lo stato SQL per un determinato [errore](../../../ado/reference/ado-api/error-object.md) oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce five-character **stringa** valore conforme allo standard ANSI SQL e indica il codice di errore.  
  
## <a name="remarks"></a>Note  
 Usare la **SQLState** proprietà da leggere il codice di errore di cinque caratteri che il provider restituisce quando si verifica un errore durante l'elaborazione di un'istruzione SQL. Ad esempio, quando si usa il Provider Microsoft OLE DB per ODBC con un database Microsoft SQL Server, codici di errore di stato SQL hanno origine da ODBC, in base agli errori specifici di ODBC o sugli errori che hanno origine da Microsoft SQL Server e quindi vengono eseguito il mapping a ODBC errori. Questi codici di errore sono documentati in allo standard ANSI SQL, ma possono essere implementati in modo diverso da diverse origini dati.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState proprietà esempio (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState esempio di proprietà (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
