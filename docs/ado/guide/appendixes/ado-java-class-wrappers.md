---
title: Wrapper di classe Java ADO | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 34a4ab7327edfb6f6f4204fb457ade97be4f5975
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702923"
---
# <a name="ado-java-class-wrappers"></a>Wrapper di classe Java ADO
Questo codice dichiara un'istanza di ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) wrapper di classe e la inizializza, tutti sulla stessa riga del codice. Inoltre, vengono dichiarate le variabili per ognuno degli argomenti in di [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo, in particolare per [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) e [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (poiché Java non supporta enumerati tipi). Apre e chiude il **Recordset** oggetto. Impostazione Rs1 su NULL semplicemente pianifica tale variabile deve essere rilasciato quando Java viene eseguito il rilascio sistematico e intermittente di oggetti inutilizzati.  
  
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
