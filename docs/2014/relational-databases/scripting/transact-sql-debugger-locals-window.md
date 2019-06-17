---
title: Finestra Variabili locali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 503a92349f7b7cfecdd4bd72de507da0a5835f7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063375"
---
# <a name="locals-window"></a>finestra Variabili locali
  Nella finestra **Variabili locali** vengono visualizzate informazioni sulle espressioni locali nell'ambito corrente del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] . L'ambito è impostato sul frame dello stack di chiamate corrente selezionato nella finestra **Stack di chiamate** . Per visualizzare espressioni locali, è necessario utilizzare la modalità di debug.  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla finestra Variabili locali**  
  
-   Scegliere **Finestre** dal menu **Debug**, quindi fare clic su **Variabili locali**.  
  
 **Per modificare il valore di un'espressione**  
  
-   Fare clic con il pulsante destro del mouse sull'espressione e scegliere **Modifica valore**.  
  
## <a name="columns"></a>Colonne  
 **Name**  
 Nome dell'espressione locale. Nel debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono elencati parametri, variabili e funzioni di sistema i cui nomi iniziano per @@.  
  
 **Value**  
 Consente di visualizzare il valore è assegnato attualmente all'espressione locale. Questa colonna è vuota quando non è stato assegnato alcun valore all'espressione.  
  
 Se la lunghezza di un'espressione è maggiore della larghezza della colonna **Valore** , il valore completo verrà visualizzato in una descrizione comandi quando si sposta il puntatore sulla cella **Valore** per l'espressione.  
  
 Un'icona di lente di ingrandimento in una cella **Valore** indica che è disponibile il visualizzatore del debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] . Nell'elenco è possibile specificare **Visualizzatore testo**, **Visualizzatore XML**o **Visualizzatore HTML**. Per avviare un visualizzatore del debugger, fare clic sull'icona di lente di ingrandimento. Tramite il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata una finestra di dialogo contenente dati in un formato appropriato per il tipo di dati.  
  
 **Tipo**  
 Consente di visualizzare il tipo di dati dell'espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](transact-sql-debugger.md)   
 [Informazioni del debugger Transact-SQL](transact-sql-debugger-information.md)   
 [finestra Espressioni di controllo](transact-sql-debugger-watch-window.md)   
 [Finestra Stack di chiamate](transact-sql-debugger-call-stack-window.md)   
 [Finestra di dialogo Controllo immediato](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Espressioni &#40; Transact-SQL &#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
