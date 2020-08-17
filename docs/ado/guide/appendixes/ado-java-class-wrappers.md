---
description: Wrapper di classe Java ADO
title: Wrapper della classe Java ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: rothja
ms.author: jroth
ms.openlocfilehash: c02865fc20d741fc8b3f80ccecd56fcb105ad45e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355217"
---
# <a name="ado-java-class-wrappers"></a>Wrapper di classe Java ADO
Questo codice dichiara un'istanza del wrapper della classe [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ADO e la inizializza, all sulla stessa riga di codice. Dichiara inoltre le variabili per ogni argomento nel metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) , specialmente per [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) e [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (perché Java non supporta i tipi enumerati). Viene aperto e chiuso l'oggetto **Recordset** . Impostando RS1 su NULL si pianifica semplicemente la variabile da rilasciare quando Java esegue la versione sistematica e intermittente degli oggetti inutilizzati.  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Microsoft SDK per Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
