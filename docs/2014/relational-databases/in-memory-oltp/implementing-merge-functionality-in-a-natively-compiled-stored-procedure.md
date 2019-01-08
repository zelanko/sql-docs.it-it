---
title: Implementazione della funzionalità di tipo MERGE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faf6112fa3f8ec588d00480d09ff072a71051a02
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508163"
---
# <a name="implementing-merge-functionality"></a>Implementazione della funzionalità MERGE
  Potrebbe essere necessario eseguire in un database l'inserimento di un aggiornamento, a seconda se una determinata riga esiste già nel database.  
  
 Senza utilizzare l'istruzione `MERGE`, di seguito è riportato un approccio che è possibile utilizzare in [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```tsql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 Un altro metodo di [!INCLUDE[tsql](../../includes/tsql-md.md)] per l'implementazione di un merge:  
  
```tsql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE....  
ELSE  
    INSERT  
```  
  
 Per una stored procedure compilata in modo nativo  
  
```tsql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT....  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
