---
title: -- (commento) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7e9aaab99194646874c0823abb61100cdc524aa
ms.sourcegitcommit: 639842f0b70e8c2c9ad5e86f9bfc3a4aad61a1df
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2020
ms.locfileid: "78261706"
---
# <a name="---comment-transact-sql"></a>-- (commento) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Evidenzia il testo inserito dall'utente. I commenti possono essere inseriti su una riga distinta oppure nidificati alla fine di una riga di comando di [!INCLUDE[tsql](../../includes/tsql-md.md)] o in un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]. Nel server il commento non viene valutato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>Argomenti  
 *text_of_comment*  
 Stringa di caratteri contenente il testo del commento.  
  
## <a name="remarks"></a>Osservazioni  
Usare due trattini ( **--** ) per commenti su una sola riga o annidati. I commenti inseriti con **--** vengono terminati da una nuova riga, specificata con un carattere di ritorno a capo (U+000A), un carattere di avanzamento riga (U+000D) o una combinazione dei due. I commenti possono essere di qualsiasi lunghezza. Nella tabella seguente sono elencati i tasti di scelta rapida che è possibile utilizzare per impostare o meno il testo come commento.
  
|Azione|Standard|  
|------------|--------------|  
|Impostare il testo selezionato come commento|CTRL+K, CTRL+C|  
|Rimuovere il commento dal testo selezionato|CTRL+K, CTRL + U|  
  
 Per altre informazioni sui tasti di scelta rapida, vedere [Tasti di scelta rapida di SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Per commenti su più righe, vedere [Barra asterisco &#40;blocco di commento&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono utilizzati i caratteri -- per l'inserimento di un commento.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi del linguaggio per il controllo di flusso &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
