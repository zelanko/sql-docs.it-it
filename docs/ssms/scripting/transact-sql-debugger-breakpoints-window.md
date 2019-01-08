---
title: Finestra Punti di interruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Breakpoints Window [Transact-SQL]
ms.assetid: bad88d10-fdd5-4d3d-b5ea-a4f063847485
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27acef25d749b088ff5ffae98d504c2da89c2bdf
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328182"
---
# <a name="transact-sql-debugger---breakpoints-window"></a>Debugger Transact-SQL - Finestra Punti di interruzione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Nella finestra **Punti di interruzione** sono elencati tutti i punti di interruzione impostati nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] corrente. Per gestire i punti di interruzione, usare la barra degli strumenti nella finestra **Punti di interruzione** . I punti di interruzione sono posizioni nel codice in cui viene sospesa l'esecuzione in modalità di debug per consentire la visualizzazione dei dati di debug.  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla finestra Punti di interruzione**  
  
-   Scegliere **Finestre** dal menu **Debug**, quindi fare clic su **Punti di interruzione**.  
  
## <a name="breakpoints-window-columns"></a>Colonne della finestra Punti di interruzione  
 Per impostazione predefinita, la finestra **Punti di interruzione** include le colonne seguenti.  
  
 **Nome**  
 Consente di visualizzare il nome del punto di interruzione. I nomi dei punti di interruzione vengono forniti dal debugger. Questo nome include il nome della finestra dell'editor di query del Motore di database che contiene il punto di interruzione e il numero di riga nell'editor di query in cui è impostato il punto di interruzione.  
  
 **Condizione**  
 Viene visualizzato **(nessuna condizione)**. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] non supporta l'impostazione di condizioni per i punti di interruzione.  
  
 **Passaggi**  
 Viene visualizzato**interrompi sempre**.  
  
 È possibile aggiungere e rimuovere le colonne seguenti selezionandole nell'elenco **Colonne** .  
  
 **Filter**  
 Viene visualizzato **(nessuno)**. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] non supporta l'impostazione di filtri per i punti di interruzione.  
  
 **Quando raggiunto**  
 Viene visualizzato **Interrompi**.  
  
 **Linguaggio**  
 Viene visualizzato **Transact-SQL** per [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Funzione**  
 Consente di visualizzare il numero della riga in cui è impostato il punto di interruzione.  
  
 **File**  
 Consente di visualizzare il nome del file di origine che contiene il punto di interruzione e il numero della riga in cui è impostato il punto di interruzione.  
  
 **Indirizzo**  
 Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] non supporta questa caratteristica.  
  
 **Process**  
 Viene visualizzato **[SQL]** , a indicare che si tratta di un processo del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , seguito dal nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in cui viene eseguito il codice.  
  
## <a name="breakpoints-window-toolbar"></a>Barra degli strumenti della finestra Punti di interruzione  
 Quando la finestra dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] corrente include punti di interruzione attivi, nella finestra **Punti di interruzione** viene visualizzata una barra degli strumenti che può essere usata per gestire i punti di interruzione.  
  
 **Elimina**  
 Consente di eliminare il punto di interruzione selezionato.  
  
 **Elimina tutti i punti di interruzione**  
 Consente di eliminare tutti i punti di interruzione visualizzati nella finestra **Punti di interruzione** .  
  
 **Disabilita tutti i punti di interruzione**  
 Consente di disabilitare tutti i punti di interruzione perché non arrestino più l'esecuzione del codice. I punti di interruzione, tuttavia, non vengono eliminati. Quando tutti i punti di interruzione sono disabilitati, il nome di questo pulsante diventa **Abilita tutti i punti di interruzione**.  
  
 **Abilita tutti i punti di interruzione**  
 Consente di abilitare tutti i punti di interruzione in modo che arrestino l'esecuzione del codice. Quando tutti i punti di interruzione sono abilitati, il nome di questo pulsante diventa **Disabilita tutti i punti di interruzione**.  
  
 **Vai a codice sorgente**  
 Consente di posizionare il cursore sulla riga dell'editor di query che contiene il punto di interruzione selezionato.  
  
 **Colonne**  
 Vengono elencate tutte le colonne che è possibile visualizzare nella finestra **Punti di interruzione** . Una casella di controllo indica le colonne visualizzate. Per aggiungere o rimuovere una colonna nella finestra **Punti di interruzione** , selezionarla nell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
