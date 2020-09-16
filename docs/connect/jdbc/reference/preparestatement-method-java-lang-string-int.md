---
description: Metodo prepareStatement (java.lang.String)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9cec12d2443e84ef3334e19253a64ff60fea1c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432863"
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
Oggetto PreparedStatement.

## <a name="exceptions"></a>Eccezioni  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Osservazioni
Questo metodo prepareStatement viene specificato dal metodo prepareStatement nell'interfaccia java.sql.Connection.

## <a name="see-also"></a>Vedere anche

[Metodo prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Membri di SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
