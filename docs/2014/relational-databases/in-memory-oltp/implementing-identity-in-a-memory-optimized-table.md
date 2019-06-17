---
title: Implementazione di IDENTITY in una tabella con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 591d86011ee769d054c069db98a40e2765b1ec27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157823"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementazione di IDENTITY in una tabella con ottimizzazione per la memoria
  IDENTITY(1, 1) è supportato in una tabella ottimizzata per la memoria. Tuttavia, le colonne Identity con la definizione di IDENTITY(x, y) dove x != 1 o y != 1 non sono supportate nelle tabelle ottimizzate per la memoria. La soluzione alternativa per i valori di identità usa l'oggetto di sequenza ([numeri di sequenza](../sequence-numbers/sequence-numbers.md)).  
  
 Rimuovere innanzitutto la proprietà IDENTITY della tabella che si converte in OLTP in memoria. Quindi, definire un nuovo oggetto SEQUENCE per la colonna della tabella. Gli oggetti SEQUENCE come le colonne IDENTITY possono creare valori DEFAULT per le colonne che utilizzano la sintassi NEXT VALUE FOR per ottenere un nuovo valore IDENTITY. Poiché i valori DEFAULT non sono supportati in OLTP in memoria, è necessario passare il valore SEQUENCE appena generato all'istruzione INSERT o a una stored procedure compilata in modo nativo che esegue l'inserimento. Nell'esempio seguente viene illustrato questo modello.  
  
```sql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 Dopo aver eseguito l'inserimento più volte, nella colonna [c1] vengono visualizzati valori validi a incremento progressivo costante. Questo set di risultati viene generato utilizzando la scansione della tabella e l'indice hash senza `ORDER BY` e quindi le righe non vengono ordinate.  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)  
  
  
