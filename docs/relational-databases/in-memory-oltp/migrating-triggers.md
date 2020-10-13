---
title: Migrazione di trigger | Microsoft Docs
description: Informazioni sulle tabelle ottimizzate per la memoria e sui trigger DDL, che attivano per CREATE, ALTER, DROP, GRANT, DENY, REVOKE o UPDATE STATISTICs su un'istanza di SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c89850acc4457dbabc3ff1340675daac036ee32
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868504"
---
# <a name="migrating-triggers"></a>Migrazione di trigger
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  In questo argomento vengono illustrati i trigger DDL e le tabelle ottimizzate per la memoria.  
  
 I trigger DML sono supportati nelle tabelle ottimizzate per la memoria, ma solo con l'evento trigger FOR | AFTER. Ad esempio, vedere [Implementing UPDATE with FROM or Subqueries](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md)(Implementazione di UPDATE con FROM o sottoquery). 
  
 I trigger LOGON sono trigger definiti per l'attivazione in corrispondenza di eventi LOGON. I trigger LOGON non influiscono sulle tabelle ottimizzate per la memoria.  
  
## <a name="ddl-triggers"></a>Trigger DDL  
 I trigger DDL sono trigger definiti per l'attivazione quando un'istruzione CREATE, ALTER, DROP, GRANT, DENY, REVOKE o UPDATE STATISTICS viene eseguita nel database o nel server in cui è definita.  
  
 Non è possibile creare tabelle ottimizzate per la memoria se nel database o nel server sono definiti uno o più trigger DDL per l'evento CREATE_TABLE o per qualsiasi gruppo di eventi in cui questo sia incluso. Non è possibile eliminare una tabella ottimizzata per la memoria se nel database o nel server sono definiti uno o più trigger DDL per l'evento DROP_TABLE o per qualsiasi gruppo di eventi in cui questo sia incluso.  
  
 Non è possibile creare stored procedure compilate in modo nativo se sono presenti uno o più trigger DDL per gli eventi CREATE_PROCEDURE, DROP_PROCEDURE o per qualsiasi gruppo di eventi in cui questi siano inclusi.  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
