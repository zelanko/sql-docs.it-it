---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223547"
---
  A partire da SQL Server 2005, il funzionamento degli schemi è stato modificato. È pertanto possibile che il codice in cui gli schemi vengono considerati equivalenti agli utenti del database non restituisca risultati corretti. Le viste del catalogo precedenti, inclusa sysobjects, non devono essere usate in un database in cui è stata usata una delle istruzioni DDL seguenti: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. In tali database è invece necessario usare le nuove viste del catalogo. Le nuove viste del catalogo prendono in considerazione la separazione tra entità e schemi introdotta in SQL Server 2005. Per altre informazioni sulle viste del catalogo, vedere [Viste del catalogo &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md).
   