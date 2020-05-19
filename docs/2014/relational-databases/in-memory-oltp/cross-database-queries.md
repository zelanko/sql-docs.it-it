---
title: Query tra database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6e829bc3bc7216532bd76f083335f126166347f4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706513"
---
# <a name="cross-database-queries"></a>Query tra database
  In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] le tabelle ottimizzate per la memoria non supportano le transazioni tra database. Non è possibile accedere a un altro database dalla stessa transazione o dalla stessa query che accede anche a una tabella ottimizzata per la memoria. Non è possibile copiare facilmente i dati da una tabella in un database a una tabella ottimizzata per la memoria in un altro database.  
  
 Le variabili di tabella non sono transazionali. Pertanto, le variabili di tabella ottimizzata per la memoria possono essere utilizzate nelle query tra database e possono quindi facilitare lo spostamento di dati da un database nelle tabelle ottimizzate per la memoria a un altro. È possibile utilizzare due transazioni. Nella prima transazione, inserire i dati della tabella remota nella variabile. Nella seconda transazione, inserire i dati nella tabella ottimizzata per la memoria locale dalla variabile.  
  
 Ad esempio, per copiare la riga dalla tabella T1 nel database DB1 alla tabella T2 in DB2, usando @v1 una variabile di tipo dbo. TT1, è possibile usare qualcosa di simile a quanto segue:  
  
```sql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)  
  
  
