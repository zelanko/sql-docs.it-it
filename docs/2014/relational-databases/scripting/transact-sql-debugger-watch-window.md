---
title: Finestra Espressioni di controllo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01caaf26257c06aae8cb7668693fd3ff6b8b5135
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328751"
---
# <a name="watch-window"></a>finestra Espressioni di controllo
  Nella finestra **Espressione di controllo** vengono visualizzate informazioni sulle espressioni selezionate. Possono essere presenti fino a quattro finestre Espressioni di controllo: **Espressione di controllo 1**, **guardare 2, 3 guarda**, e **guarda 4**. Le espressioni vengono valutate nell'ambito del frame dello stack di chiamate corrente selezionato nella finestra **Stack di chiamate** . Per controllare variabili ed espressioni, è necessario utilizzare la modalità di debug.  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alle finestre Espressione di controllo**  
  
-   Scegliere **Finestre** dal menu **Debug**, fare clic su **Espressione di controllo**, quindi su **Espressione di controllo 1**, **Espressione di controllo 2, Espressione di controllo 3**o **Espressione di controllo 4**.  
  
 **Per modificare il valore di un'espressione**  
  
-   Fare clic con il pulsante destro del mouse sull'espressione e scegliere **Modifica valore**.  
  
## <a name="columns"></a>Colonne  
 **Name**  
 Espressioni elencate dal debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] . Sono supportate le espressioni seguenti:  
  
-   Variabili.  
  
-   Parametri.  
  
-   Funzioni di sistema il cui nome inizia con @@.  
  
-   Espressioni compilate applicando operatori a uno o più parametri, variabili o funzioni di sistema, ad esempio @@IntegerCounter + 1 o FirstName + LastName.  
  
-   Istruzioni Transact-SQL che restituiscono un singolo valore, ad esempio: SELECT CharacterCol FROM MyTable in cui PrimaryKey = 1.  
  
 **Valore**  
 Consente di visualizzare il valore restituito dopo che il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] valuta l'espressione specificata in **Nome**.  
  
 Se la lunghezza di un'espressione è maggiore della larghezza della colonna **Valore** , il valore completo verrà visualizzato in una descrizione comandi quando si sposta il puntatore sulla cella **Valore** per l'espressione.  
  
 Un'icona di lente di ingrandimento in una cella **Valore** indica che è disponibile il visualizzatore del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nell'elenco è possibile specificare **Visualizzatore testo**, **Visualizzatore XML**o **Visualizzatore HTML**. Per avviare un visualizzatore del debugger, fare clic sull'icona di lente di ingrandimento. Nel debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] verrà visualizzata una finestra di dialogo contenente dati in un formato appropriato per il tipo di dati.  
  
 **Tipo**  
 Consente di visualizzare il tipo di dati dell'espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](transact-sql-debugger.md)   
 [Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)   
 [finestra Variabili locali](transact-sql-debugger-locals-window.md)   
 [Finestra Stack di chiamate](transact-sql-debugger-call-stack-window.md)   
 [Finestra di dialogo Controllo immediato](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Espressioni &#40; Transact-SQL &#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
