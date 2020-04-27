---
title: Implementazione di un outer join | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 67084043-6b23-4975-b9db-6e49923d4bab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 532cdf5466445f08d5d415799b9f4afab347e77f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63158168"
---
# <a name="implementing-an-outer-join"></a>Implementazione di un outer join
  L'outer join non è supportato in stored procedure compilate in modo nativo. Nell'esempio seguente viene illustrata una modalità per implementare la funzionalità di un left outer join in una stored procedure compilata in modo nativo.  
  
 Negli esempi vengono utilizzate una variabile di tabella per simulare un cursore sul lato sinistro del join e una variabile di tabella per costruire un unico set di risultati, vale a dire l'unico appropriato per l'elaborazione di un numero limitato di righe in quanto comporta la creazione di una copia aggiuntiva delle righe di dati.  
  
 Una variabile (@outer) di tipo t1_type viene utilizzata per scorrere le righe da T1, utilizzando un ciclo while per simulare un cursore. La variabile @result di tipo t1t2_join_type viene quindi utilizzata per costruire il set di risultati.  
  
 È necessario eseguire il test delle prestazioni di questa soluzione alternativa, per assicurarsi che venga eseguita come previsto nell'applicazione.  
  
```  
-- original query:  
select   
   t1.c1 as t1c1,  
   t1.c2 as t1c2,  
   t2.c2 as t2c2,  
   t2.c3 as t2c3  
   from t1 left join t2 on t1.c2=t2.c3  
GO  
  
create table dbo.t1  
(c1 int not null primary key nonclustered,  
c2 int not null) with (memory_optimized=on)  
  
create table dbo.t2  
(c2 int not null primary key nonclustered,  
c3 int not null) with (memory_optimized=on)  
  
INSERT t1 VALUES (1,2)  
INSERT t1 VALUES (2,3)  
INSERT t1 VALUES (3,2)  
INSERT t2 VALUES (2,3)  
INSERT t2 VALUES (4,3)  
GO  
  
create type dbo.t1_type as table  
(  
   id int identity not null primary key nonclustered hash with (bucket_count=1024),  
   c1 int,  
   c2 int  
) with (memory_optimized=on)  
GO  
  
create type dbo.t1t2_join_type as table  
(  
   t1c1 int not null index ix_t1c1,  
   t1c2 int not null,  
   t2c2 int,  
   t2c3 int  
) with (memory_optimized=on)  
GO  
  
-- ====== scenario: generic left join  
  
-- stored procedure including the workaround  
create procedure dbo.usp_left_join  
with native_compilation, execute as owner, schemabinding  
as  
begin atomic with (transaction isolation level = snapshot, language = N'us_english')  
  
   DECLARE @outer dbo.t1_type  
   DECLARE @result dbo.t1t2_join_type  
  
   -- populate the variable used for iterating over the outer rows  
   INSERT @outer(c1, c2) select c1,c2 from dbo.t1  
  
   DECLARE @i int = 1  
   DECLARE @max int = scope_identity()  
  
   DECLARE @t1c1 int  
   DECLARE @t1c2 int  
  
   while @i <= @max  
   begin     
      select @t1c1 = c1, @t1c2 = c2 from @outer where id = @i  
  
      INSERT @result select @t1c1, @t1c2, c2, c3 from dbo.t2 where c3 = @t1c2  
  
      if @@rowcount = 0   
         INSERT @result (t1c1, t1c2) VALUES (@t1c1, @t1c2)  
  
      set @i += 1  
   end  
  
   select   
      t1c1,  
      t1c2,  
      t2c2,  
      t2c3  
   from @result  
end  
GO  
  
exec dbo.usp_left_join  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di migrazione per le stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
