---
title: Implementare trigger DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a32b4b17974dfbd761ee56a16ec7f8f74e7d4b76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62698496"
---
# <a name="implement-ddl-triggers"></a>Implementazione di trigger DDL
  In questo argomento vengono fornite informazioni sulla creazione, la modifica, la disabilitazione o l'eliminazione di trigger DDL.  
  
## <a name="creating-ddl-triggers"></a>Creazione di trigger DDL  
 I trigger DDL vengono creati mediante l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER per trigger DDL.  
  
 **Per creare un trigger DDL**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
> [!IMPORTANT]  
>  La restituzione di set di risultati dai trigger verrà rimossa a partire da una delle prossime versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. I trigger che restituiscono set di risultati possono provocare comportamenti imprevisti nelle applicazioni che non sono state progettate per il loro utilizzo. Evitare di restituire set di risultati dai trigger in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni che attualmente li restituiscono. Per impedire che i trigger restituiscano set di risultati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], impostare l'opzione [Disallow Results From Triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) su 1. L'impostazione predefinita per questa opzione sarà 1 nella prossima versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="modifying-ddl-triggers"></a>Modifica di trigger DDL  
 Se è necessario modificare la definizione di un trigger DDL, è possibile eliminare e creare nuovamente il trigger oppure ridefinire il trigger esistente in un unico passaggio.  
  
 Se si modifica il nome di un oggetto a cui fa riferimento un trigger DDL, è necessario modificare il trigger in modo che il testo corrisponda al nuovo nome. Pertanto, prima di rinominare un oggetto, visualizzare le dipendenze dell'oggetto per determinare se la modifica proposta interessa i trigger.  
  
 È inoltre possibile modificare i trigger per crittografarne la definizione.  
  
 **Per modificare un trigger**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)  
  
 **Per visualizzare le dipendenze di un trigger**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>Disabilitazione ed eliminazione di trigger DDL  
 Quando un trigger DDL non è più necessario, è possibile disabilitarlo o eliminarlo.  
  
 La disabilitazione di un trigger DDL non ne comporta l'eliminazione. Il trigger continua a esistere come oggetto nel database corrente ma non viene attivato quando viene eseguita una qualsiasi istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] in cui è stato programmato. I trigger DDL disabilitati possono essere riabilitati. A seguito di tale operazione, il trigger DDL viene attivato nello stesso modo in cui è stato attivato al momento della creazione. Per impostazione predefinita, i trigger DDL vengono abilitati al momento della creazione.  
  
 Quando si elimina un trigger DDL, questo viene rimosso dal database corrente. Ciò non ha alcun effetto sugli oggetti o sui dati per il cui ambito il trigger DDL è stato definito.  
  
 **Per disabilitare un trigger DDL**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
 **Per abilitare un trigger DDL**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
 **Per eliminare un trigger DDL**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)  
  
  
