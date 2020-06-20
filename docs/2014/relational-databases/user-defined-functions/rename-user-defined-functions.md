---
title: Rinominare funzioni definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
ms.openlocfilehash: ec923be64cf7819c4018ebda71a472f58b29cf8b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054995"
---
# <a name="rename-user-defined-functions"></a>Ridenominare funzioni definite dall'utente
  È possibile rinominare funzioni definite dall'utente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Rinominare funzioni definite dall'utente tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   I nomi di funzione devono essere conformi alla regole per gli [identificatori](../databases/database-identifiers.md).  
  
-   La ridenominazione di una funzione definita dall'utente non comporta la modifica del nome dell'oggetto corrispondente nella colonna di definizione della vista del catalogo **sys.sql_modules** . È pertanto consigliabile evitare di rinominare questo tipo di oggetto. In alternativa, eliminare e ricreare la stored procedure con il nuovo nome.  
  
-   La modifica del nome o della definizione di una funzione definita dall'utente può provocare errori degli oggetti dipendenti se questi non vengono aggiornati in base alla modifica apportata alla funzione.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per eliminare la funzione, è necessaria l'autorizzazione ALTER per lo schema a cui appartiene la funzione o l'autorizzazione CONTROL per la funzione. Per ricreare la funzione, sono necessarie l'autorizzazione CREATE FUNCTION per il database e l'autorizzazione ALTER per lo schema in cui viene creata la funzione.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-rename-user-defined-functions"></a>Per rinominare funzioni definite dall'utente  
  
1.  In **Esplora oggetti**fare clic sul segno più accanto al database che contiene la funzione che si desidera rinominare.  
  
2.  Fare clic sul segno più accanto alla cartella **Programmabilità** .  
  
3.  Fare clic sul segno più accanto alla cartella che contiene la funzione che si desidera rinominare:  
  
    -   Table-valued Function  
  
    -   Funzione a valori scalari  
  
    -   Funzione di aggregazione  
  
4.  Fare clic con il pulsante destro del mouse sulla funzione da rinominare e scegliere **Rinomina**.  
  
5.  Immettere il nuovo nome della funzione.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
 **Per rinominare funzioni definite dall'utente**  
  
 Non è possibile eseguire questa attività utilizzando istruzioni Transact-SQL. Per rinominare una funzione definita dall'utente tramite Transact-SQL, è innanzitutto necessario eliminare la funzione esistente e quindi ricrearla con il nuovo nome. Assicurarsi che tutto il codice e tutte le applicazioni in cui è stato usato il nome precedente della funzione usino ora il nuovo nome.  
  
 Per altre informazioni, vedere [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql) e [DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)   
 [Visualizzare funzioni definite dall'utente](user-defined-functions.md)  
  
  
