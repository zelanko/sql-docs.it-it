---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 72e0b54f26c323c16efa8c67aea1c325e8ddf72d
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552288"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|137|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|P_SCALAR_VAR_NOTFOUND|  
|Testo del messaggio|Dichiarare la variabile scalare "%.*ls".|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore si verifica quando una variabile viene utilizzata in uno script SQL senza essere stata dichiarata in precedenza. Nell'esempio seguente viene restituito l'errore 137 per entrambe le istruzioni SET e SELECT perché **@mycol** non è dichiarato.  
  
 SET @mycol = 'ContactName';  
  
 SELECT @mycol;  
  
 Una delle cause più complesse di questo errore include l'utilizzo di una variabile dichiarata al di fuori dell'istruzione EXECUTE. La variabile **@mycol** specificata nell'istruzione SELECT, ad esempio, è locale per l'istruzione SELECT, quindi è esterna all'istruzione Execute.  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che qualsiasi variabile utilizzata in uno script SQL venga dichiarata prima di essere utilizzata.  
  
 Riscrivere lo script in modo che non faccia riferimento a variabili nell'istruzione EXECUTE dichiarate al di fuori dell'istruzione stessa. Ad esempio:  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20) ;  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>Vedere anche  
 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [Istruzioni SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
