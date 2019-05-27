---
title: Eseguire istruzione per istruzione il codice Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e79a92bc1756003341cbb9e0581ade42a2bcee8b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090006"
---
# <a name="step-through-transact-sql-code"></a>Esecuzione istruzione per istruzione del codice Transact-SQL
  Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] consente di controllare quali istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono eseguite in una finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . È possibile sospendere l'esecuzione del debugger in corrispondenza di singole istruzioni e successivamente visualizzare lo stato degli elementi di codice in quei punti.  
  
## <a name="breakpoints"></a>Punti di interruzione  
 Un punto di interruzione indica al debugger di sospendere temporaneamente l'esecuzione in corrispondenza di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] specifica. Per ulteriori informazioni sui punti di interruzione, vedere Utilizzo di punti di interruzione Transact-SQL.  
  
## <a name="controlling-statement-execution"></a>Controllo dell'esecuzione di istruzioni  
 Nel debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] è possibile specificare le opzioni seguenti per eseguire il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] dall'istruzione corrente:  
  
-   Eseguire il codice fino al successivo punto di interruzione.  
  
-   Eseguire la successiva istruzione.  
  
     Se l'istruzione successiva richiama una stored procedure, una funzione o un trigger [!INCLUDE[tsql](../../includes/tsql-md.md)] , verrà visualizzata dal debugger una nuova finestra dell'editor di query contenente il codice del modulo. La finestra sarà in modalità di debug e l'esecuzione verrà sospesa in corrispondenza della prima istruzione nel modulo. È possibile spostarsi quindi nel codice del modulo, ad esempio, impostando dei punti di interruzione o avanzando istruzione per istruzione nel codice.  
  
-   Passare all'istruzione successiva.  
  
     Viene eseguita l'istruzione successiva. Tuttavia, se l'istruzione richiama una stored procedure, una funzione o un trigger, il codice del modulo viene eseguito fino alla fine e i risultati vengono restituiti al codice che ha effettuato la chiamata. Se si è sicuri che in una stored procedure non vi siano errori, è possibile superarla. L'esecuzione viene sospesa in corrispondenza dell'istruzione che segue la chiamata alla stored procedure, la funzione o il trigger.  
  
-   Uscire da una stored procedure, una funzione o un trigger.  
  
     L'esecuzione viene sospesa in corrispondenza dell'istruzione che segue la chiamata alla stored procedure, la funzione o il trigger.  
  
-   Eseguire il codice dalla posizione corrente alla posizione corrente del puntatore e ignorare tutti i punti di interruzione.  
  
 Nella tabella seguente sono elencate le varie procedure che consentono di controllare il modo in cui le istruzioni sono eseguite nel debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
|Azione|Routine|  
|------------|---------------|  
|Eseguire tutte le istruzioni dall'istruzione corrente al successivo punto di interruzione|Nel **Debug** menu, fare clic su **continua**.<br /><br /> Nel **Debug** sulla barra degli strumenti, fare clic sui **continua** pulsante.|  
|Eseguire la successiva istruzione o il successivo modulo.|Nel **Debug** menu, fare clic su **Esegui istruzione**.<br /><br /> Nel **Debug** sulla barra degli strumenti, fare clic sui **Esegui istruzione** pulsante.<br /><br /> Premere F11.|  
|Passare alla successiva istruzione o al successivo modulo.|Nel **Debug** menu, fare clic su **Esegui istruzione/routine**.<br /><br /> Nel **Debug** sulla barra degli strumenti, fare clic sui **Esegui istruzione/routine** pulsante.<br /><br /> Premere F10.|  
|Uscire da un modulo|Nel **Debug** menu, fare clic su **Esci da istruzione /**.<br /><br /> Nel **Debug** sulla barra degli strumenti, fare clic sui **Esci da istruzione /** pulsante.<br /><br /> Premere MAIUSC+F11.|  
|Eseguire il codice fino alla posizione corrente del cursore|Fare clic con il pulsante destro del mouse nella finestra dell'editor di query, quindi fare clic su **Esegui fino al cursore**.<br /><br /> Premere CTRL+F10.|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)  
  
  
