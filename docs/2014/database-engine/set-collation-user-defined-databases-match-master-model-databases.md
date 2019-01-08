---
title: Impostare i database definiti dall'utente di regole di confronto corrispondono a quelle del master e i database modello | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfb00b1cc1a9930f7a374403b40e2c0d793eb090
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371083"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>Impostazione delle regole di confronto dei database definiti dall'utente in modo che corrispondano a quelle dei database master e modello
  Questa regola consente di controllare se i database definiti dall'utente vengono configurati utilizzando le stesse regole di confronto di quelle per i database master e modello.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 È consigliabile fare in modo che le regole di confronto dei database definiti dall'utente corrispondano a quelle dei database master e modello. In caso contrario, possono verificarsi conflitti relativi alle regole di confronto che potrebbero impedire l'esecuzione del codice. Quando, ad esempio, una stored procedure crea un join tra una tabella e una tabella temporanea, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] potrebbe terminare il batch e restituire un errore di conflitto tra regole di confronto se le regole di confronto del database definito dall'utente differiscono da quelle del database modello. Questo problema si verifica perché le tabelle temporanee vengono create in tempdb, che basa le proprie regole di confronto su quelle del modello.  
  
 In caso di errori di conflitto tra regole di confronto, considerare una delle soluzioni seguenti:  
  
-   Esportare i dati dal database utente e importarli nelle nuove tabelle che utilizzano le stesse regole di confronto dei database master e modello.  
  
-   Ricompilare i database di sistema in modo che vengano utilizzate regole di confronto corrispondenti a quelle del database utente. Per altre informazioni su come ricompilare i database di sistema, vedere [ricompilare database di sistema](../relational-databases/databases/system-databases.md).  
  
-   Modificare qualsiasi stored procedure che crea join tra tabelle utente e tabelle in tempdb per creare le tabelle in tempdb utilizzando le regole di confronto del database utente. A tale scopo, aggiungere la clausola `COLLATE database_default` alle definizioni di colonna della tabella temporanea, come illustrato nell'esempio seguente:  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Impostare o modificare le regole di confronto del database](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [Impostare o modificare le regole di confronto delle colonne](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Articolo 325335 della Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [Come si fa: Installare SQL Server 2008 dal Prompt dei comandi](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
