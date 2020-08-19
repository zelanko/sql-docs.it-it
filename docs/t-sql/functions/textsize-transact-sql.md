---
description: '&#x40;&#x40;TEXTSIZE (Transact-SQL)'
title: '@@TEXTSIZE (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TEXTSIZE'
- '@@TEXTSIZE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, TEXTSIZE option
- SELECT statement [SQL Server], text size returned
- TEXTSIZE option
- '@@TEXTSIZE function'
- text size returned [SQL Server]
ms.assetid: 4308a7b9-8e8f-49e9-8246-8224e32f4953
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 349ef2067c50a9955643c02cb8ba5226a1f15ddc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422565"
---
# <a name="x40x40textsize-transact-sql"></a>&#x40;&#x40;TEXTSIZE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce il valore corrente dell'opzione [TEXTSIZE](../../t-sql/statements/set-textsize-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@TEXTSIZE  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 **integer**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene usato `SELECT` per visualizzare il valore `@@TEXTSIZE` prima e dopo la relativa modifica tramite l'istruzione `SET``TEXTSIZE`.  
  
```  
-- Set the TEXTSIZE option to the default size of 4096 bytes.  
SET TEXTSIZE 0  
SELECT @@TEXTSIZE AS 'Text Size'  
SET TEXTSIZE 2048  
SELECT @@TEXTSIZE AS 'Text Size'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Text Size
-----------
4096
Text Size
-----------
2048
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di configurazione &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)  
  
  
