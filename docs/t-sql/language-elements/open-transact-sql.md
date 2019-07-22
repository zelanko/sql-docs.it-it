---
title: OPEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs:
- TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
author: rothja
ms.author: jroth
ms.openlocfilehash: 70f3b23244095b79dc8340d3060e6d30d5009a2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121929"
---
# <a name="open-transact-sql"></a>OPEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Apre un cursore server [!INCLUDE[tsql](../../includes/tsql-md.md)] e popola il cursore mediante l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] specificata nell'istruzione DECLARE CURSOR o SET *cursor_variable*.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argomenti  
 GLOBAL  
 Specifica che *cursor_name* fa riferimento a un cursore globale.  
  
 *cursor_name*  
 Nome del cursore dichiarato. Se esistono sia un cursore globale che un cursore locale con il nome *cursor_name*, *cursor_name* fa riferimento al cursore globale se viene specificato l'argomento GLOBAL. In caso contrario, *cursor_name* fa riferimento al cursore locale.  
  
 *cursor_variable_name*  
 Nome di una variabile di cursore che fa riferimento a un cursore.  
  
## <a name="remarks"></a>Remarks  
 Se il cursore viene dichiarato con l'opzione INSENSITIVE o STATIC, OPEN crea una tabella temporanea per il set di risultati. OPEN ha esito negativo se le dimensioni di una riga del set dei risultati supera le dimensioni massime consentite per le righe delle tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se il cursore viene dichiarato con l'opzione KEYSET, OPEN crea una tabella temporanea per il keyset. Le tabelle temporanee vengono archiviate in tempdb.  
  
 Dopo l'apertura di un cursore, usare la funzione @@CURSOR_ROWS per ricevere il numero delle righe risultanti nell'ultimo cursore aperto.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta la generazione asincrona di cursori [!INCLUDE[tsql](../../includes/tsql-md.md)] gestiti da keyset o statici. [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio OPEN o FETCH, vengono eseguite in batch. Non è quindi necessario generare i cursori [!INCLUDE[tsql](../../includes/tsql-md.md)] in modo asincrono. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta ancora i cursori API del server statici o gestiti da keyset asincroni nei casi in cui l'istruzione OPEN a bassa latenza costituisce un problema, a causa dei round trip del client per ogni operazione del cursore.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene aperto un cursore e vengono recuperate tutte le righe.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
