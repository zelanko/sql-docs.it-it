---
title: Metodo prepareStatement (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4fd42fccc0e6e3e15feb3d866ccb8d40531a1d4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796695"
---
# <a name="preparestatement-method-javalangstring"></a>Metodo prepareStatement (java.lang.String)

Crea un oggetto [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) per l'invio di istruzioni SQL con parametri al database.

## <a name="syntax"></a>Sintassi

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parametri
*sql*

Valore **String** contenente un'istruzione SQL.

## <a name="return-value"></a>Valore restituito
Un oggetto di impostazione PreparedStatement.

## <a name="exceptions"></a>Eccezioni  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Questo metodo prepareStatement viene specificato dal metodo prepareStatement nell'interfaccia Java.

## <a name="see-also"></a>Vedere anche

[Metodo prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Membri di SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
