---
title: Simulazione di un'istruzione IF-WHILE EXISTS in un modulo compilato in modo nativo
description: Informazioni su come simulare la clausola EXISTS nelle istruzioni condizionali, operazione non supportata dalle stored procedure compilate in modo nativo in SQL Server.
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f62b799a124eb7ed47ffad9e63d0433172984c18
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735023"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simulazione di un'istruzione IF-WHILE EXISTS in un modulo compilato in modo nativo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Le stored procedure compilate in modo nativo non supportano la clausola **EXISTS** nelle istruzioni condizionali come IF e WHILE.  
  
 L'esempio seguente illustra una soluzione alternativa che usa una variabile BIT con un'istruzione SELECT per simulare una clausola EXISTS:  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Costrutti Transact-SQL non supportati da OLTP in memoria](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
