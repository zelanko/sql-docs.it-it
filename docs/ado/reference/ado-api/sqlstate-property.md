---
description: Proprietà SQLState
title: Proprietà SQLState | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bbc849f19c91f7b2387df5e0e71b3455efa0db09
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988862"
---
# <a name="sqlstate-property"></a>Proprietà SQLState
Indica lo stato SQL per un determinato oggetto [Error](./error-object.md) .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **stringa** di cinque caratteri che segue lo standard ANSI SQL e indica il codice di errore.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **SQLSTATE** per leggere il codice di errore di cinque caratteri restituito dal provider quando si verifica un errore durante l'elaborazione di un'istruzione SQL. Ad esempio, quando si utilizza il provider Microsoft OLE DB per ODBC con un database Microsoft SQL Server, i codici di errore dello stato SQL provengono da ODBC, basati su errori specifici di ODBC o sugli errori che hanno origine da Microsoft SQL Server e vengono quindi mappati a errori ODBC. Questi codici di errore sono documentati nello standard ANSI SQL, ma possono essere implementati in modo diverso da origini dati diverse.  
  
## <a name="applies-to"></a>Si applica a  
 [Error (oggetto)](./error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)