---
title: Debugger Transact-SQL
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, introduction
ms.assetid: 6e914699-0d85-46c2-aa2d-3e339ac2c4ce
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfb1fd563506c06ede5832a06ba98eaae18e58ed
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718246"
---
# <a name="transact-sql-debugger"></a>Debugger Transact-SQL
  Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] consente di individuare errori nel codice [!INCLUDE[tsql](../../includes/tsql-md.md)] esaminandone il comportamento in fase di esecuzione. Dopo avere impostato la finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] sulla modalità di debug, è possibile sospendere l'esecuzione di righe specifiche di codice e controllare le informazioni e i dati utilizzati o restituiti da tali istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="stepping-through-transact-sql-code"></a>Esecuzione istruzione per istruzione del codice Transact-SQL  
 Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] fornisce le seguenti opzioni che è possibile usare per spostarsi nel codice di [!INCLUDE[tsql](../../includes/tsql-md.md)] quando la finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in modalità di debug:  
  
-   Impostare i punti di interruzione su singole istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     Un punto di interruzione specifica un punto in cui si desidera interrompere l'esecuzione per esaminare i dati. Quando viene avviato, il debugger sospende l'esecuzione in corrispondenza della prima riga di codice nella finestra dell'editor di query. Per proseguire l'esecuzione fino al primo punto di interruzione impostato, è possibile usare la funzionalità **Continua** . La funzionalità **Continua** può essere usata anche per procedere al successivo punto di interruzione da qualsiasi posizione in cui è stata attualmente messa in pausa la finestra. È possibile modificare i punti di interruzione per specificare alcune azioni, ad esempio le condizioni in base alle quali il punto deve interrompere l'esecuzione, le informazioni da visualizzare nella finestra di **output** e la modifica della posizione del punto di interruzione.  
  
-   Eseguire la successiva istruzione.  
  
     Questa opzione consente di spostarsi da un'istruzione alla successiva in un set di istruzioni e di osservare il comportamento di ognuna.  
  
-   Eseguire una chiamata o passare alla successiva chiamata a una stored procedure o una funzione.  
  
     Se si è sicuri che in una stored procedure non vi siano errori, è possibile superarla. La procedura viene eseguita completamente e i risultati vengono restituiti al codice.  
  
     Se si desidera eseguire il debug di una stored procedure o una funzione, è possibile eseguirlo nel modulo. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] apre una nuova finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] popolata con il codice sorgente per il modulo, imposta la finestra in modalità di debug, quindi sospende l'esecuzione della prima istruzione nel modulo. È possibile spostarsi quindi attraverso il codice del modulo, ad esempio, impostando dei punti di interruzione o avanzando nel codice.  
  
 Per altre informazioni sulle modalità con cui il debugger consente di spostarsi nel codice, vedere [Esecuzione istruzione per istruzione del codice Transact-SQL](step-through-transact-sql-code.md).  
  
## <a name="viewing-debugger-information"></a>Visualizzazione delle informazioni del debugger  
 Ogni volta che il debugger sospende l'esecuzione in corrispondenza di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] specifica, è possibile utilizzare le seguenti finestre del debugger per visualizzare lo stato corrente dell'esecuzione:  
  
-   **Variabili locali** ed **Espressione di controllo** In queste finestre vengono visualizzate le espressioni [!INCLUDE[tsql](../../includes/tsql-md.md)] attualmente allocate. Le espressioni sono clausole [!INCLUDE[tsql](../../includes/tsql-md.md)] che restituiscono una singola espressione scalare. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta la visualizzazione di espressioni che fanno riferimento a variabili, parametri oppure alle funzioni predefinite [!INCLUDE[tsql](../../includes/tsql-md.md)] i cui nomi iniziano con @@. In queste finestre vengono inoltre visualizzati i valori dei dati che sono attualmente assegnati alle espressioni.  
  
-   **Controllo immediato.** Questa finestra visualizza il valore di un'espressione [!INCLUDE[tsql](../../includes/tsql-md.md)] e consente di salvare l'espressione in una finestra **Espressione di controllo** .  
  
-   **Punti di interruzione.** In questa finestra vengono visualizzati i punti di interruzione attualmente impostati ed è possibile gestirli.  
  
-   **Stack di chiamate.** In questa finestra viene visualizzato il percorso di esecuzione corrente. Questa finestra fornisce inoltre informazioni sul modo in cui l'esecuzione è passata dalla finestra dell'editor di query originale attraverso qualsiasi funzione, stored procedure o trigger per raggiungere il percorso di esecuzione corrente.  
  
-   **Output.** In questa finestra vengono visualizzati i vari messaggi e dati del programma, ad esempio i messaggi di sistema inviati dal debugger.  
  
-   **Risultati** ed **Messaggi** In queste schede della finestra dell'editor di query vengono visualizzati i risultati delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] precedentemente eseguite.  
  
## <a name="transact-sql-debugger-tasks"></a>Attività del debugger Transact-SQL  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Descrive come configurare il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] per il debugging remoto.|[Configurazione del debugger Transact-SQL](configure-firewall-rules-before-running-the-tsql-debugger.md)|  
|Descrive come avviare, arrestare e controllare l'operazione del debugger.|[Eseguire il debugger Transact-SQL](transact-sql-debugger.md)|  
|Descrive come utilizzare il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] per avanzare nel codice.|[Eseguire istruzione per istruzione il codice Transact-SQL](step-through-transact-sql-code.md)|  
|Descrive come utilizzare il debugger per visualizzare dati [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio parametri e variabili, e informazioni sul sistema.|[Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Editor di query e di testo &#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
