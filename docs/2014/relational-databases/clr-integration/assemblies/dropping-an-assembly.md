---
title: Eliminazione di un Assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7dceef4651804dabf4080d6f8b85d0597b1957b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919623"
---
# <a name="dropping-an-assembly"></a>Eliminazione di un assembly
  Gli assembly registrati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'istruzione CREATE ASSEMBLY possono essere eliminati quando la funzionalità che forniscono non è più necessaria. L'eliminazione di un assembly ne comporta la rimozione insieme a tutti i file associati, ad esempio i file di debug, dal database. Per eliminare un assembly, utilizzare l'istruzione DROP ASSEMBLY con la sintassi seguente:  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 DROP ASSEMBLY non interferisce con il codice che fa riferimento all'assembly attualmente in esecuzione. Tuttavia, dopo l'esecuzione di DROP ASSEMBLY qualsiasi tentativo di richiamare il codice dell'assembly avrà esito negativo.  
  
 DROP ASSEMBLY restituisce un errore se all'assembly viene fatto riferimento da un altro assembly esistente nel database oppure se viene utilizzato da funzioni CLR (Common Language Runtime), procedure, trigger, tipi definiti dall'utente o funzioni di aggregazione definite dall'utente nel database corrente. Utilizzare innanzitutto le istruzioni DROP AGGREGATE, DROP FUNCTION, DROP PROCEDURE, DROP TRIGGER e DROP TYPE per eliminare gli oggetti di database gestiti contenuti nell'assembly.  
  
## <a name="removing-a-udt-from-the-database"></a>Rimozione di un tipo definito dall'utente (UDT) dal database  
 L'istruzione DROP TYPE rimuove un tipo definito dall'utente (UDT) dal database corrente. Dopo avere eliminato un tipo definito dall'utente (UDT), è possibile utilizzare l'istruzione DROP ASSEMBLY per eliminare l'assembly dal database.  
  
 L'istruzione DROP TYPE non riesce se gli oggetti dipendono dal tipo definito dall'utente, come nelle situazioni seguenti:  
  
-   Tabelle del database che contengono colonne definite mediante il tipo definito dall'utente (UDT).  
  
-   Funzioni, stored procedure o trigger che utilizzano variabili o parametri del tipo definito dall'utente (UDT), creati nel database con la clausola WITH SCHEMABINDING.  
  
### <a name="finding-udt-dependencies"></a>Ricerca di dipendenze di tipi definiti dall'utente (UDT)  
 È necessario innanzitutto eliminare tutti gli oggetti dipendenti, quindi eseguire l'istruzione DROP TYPE. Quanto segue [!INCLUDE[tsql](../../../includes/tsql-md.md)] consente di individuare tutte le colonne e i parametri che utilizzano un tipo definito dall'utente nella query il **AdventureWorks** database.  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>Vedere anche  
 [La gestione degli assembly dell'integrazione CLR](managing-clr-integration-assemblies.md)   
 [Modifica di un Assembly](altering-an-assembly.md)   
 [Creazione di un Assembly](creating-an-assembly.md)   
 [DROP AGGREGATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-aggregate-transact-sql)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [DROP TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-type-transact-sql)  
  
  
