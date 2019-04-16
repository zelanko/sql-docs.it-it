---
title: Alias di colonna nella clausola ORDER BY non possono essere preceduti dall'alias della tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], columns
ms.assetid: fee7328f-6e8d-4005-930b-56fb6f17e0b2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 815e4105ca65b6bcdaa36de0554b9f6e0d3b478a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583264"
---
# <a name="column-aliases-in-order-by-clause-cannot-be-prefixed-by-table-alias"></a>Gli alias di colonna utilizzati nella clausola ORDER BY non possono essere preceduti dall'alias della tabella
  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successiva gli alias di colonna utilizzati nella clausola ORDER BY non possono essere preceduti dall'alias della tabella.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Ad esempio, la query seguente viene eseguita in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], ma restituisce un errore in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.l  
```  
  
 Il [!INCLUDE[ssDEversion10](../../includes/ssdeversion10-md.md)] non associa `p.l` nella clausola `ORDER BY` a una colonna valida nella tabella.  
  
### <a name="exception"></a>Eccezione  
 Se l'alias di colonna con prefisso specificato nella clausola ORDER BY è un nome di colonna valido nella tabella specificata, la query viene eseguita senza errori. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] la semantica dell'istruzione potrebbe essere diversa. Ad esempio, l'alias di colonna (`id`) specificato nell'istruzione seguente è un nome di colonna valido nella tabella `sysobjects`. Quando l'istruzione viene eseguita in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], l'operazione `CAST` viene eseguita dopo l'ordinamento del set di risultati. Questo significa che nell'operazione di ordinamento viene utilizzata la colonna `name`. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] l'operazione `CAST` viene eseguita prima dell'operazione di ordinamento. Questo significa che nell'operazione di ordinamento viene utilizzata la colonna `id` nelle tabelle e il set di risultati viene restituito in un ordine imprevisto.  
  
```  
SELECT CAST (o.name AS char(128)) AS id  
FROM sysobjects AS o  
ORDER BY o.id;  
```  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le query che utilizzano alias di colonna preceduti da alias di tabella nella clausola ORDER BY in uno dei modi seguenti:  
  
-   Se possibile, evitare di aggiungere un prefisso all'alias di colonna nella clausola ORDER BY.  
  
-   Sostituire l'alias di colonna con il nome della colonna.  
  
 Ad esempio, le due query seguenti vengono eseguite senza errori in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY l  
  
USE AdventureWorks2012;  
GO  
SELECT FirstName AS f, LastName AS l  
FROM Person.Contact p  
ORDER BY p.LastName  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
