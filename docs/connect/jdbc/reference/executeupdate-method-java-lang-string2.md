---
title: Metodo executeUpdate (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8c408098ebe1e9e732b171390eb1901f01014292
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66804145"
---
# <a name="executeupdate-method-javalangstring"></a>Metodo executeUpdate (java.lang.String)

Esegue l'istruzione SQL specificata, che può essere un'istruzione INSERT, UPDATE, MERGE o DELETE, oppure un'istruzione SQL che non restituisce nulla, quale un'istruzione SQL DDL.

## <a name="syntax"></a>Sintassi

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parametri
*sql*

Valore **String** contenente l'istruzione SQL.

## <a name="return-value"></a>Valore restituito
Valore **int** che indica il numero di righe interessate oppure 0 se si usa un'istruzione DDL.

## <a name="exceptions"></a>Eccezioni
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Questo metodo executeUpdate viene specificato dal metodo executeUpdate nell'interfaccia java.sql.PreparedStatement.

La chiamata di questo metodo genera un'eccezione perché l'istruzione SQL per l'oggetto SQLServerPreparedStatement viene specificata quando viene creato l'oggetto.

## <a name="see-also"></a>Vedere anche

[Metodo executeUpdate &#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[Membri di SQLServerPreparedStatement](./sqlserverpreparedstatement-members.md)

[Classe SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)
