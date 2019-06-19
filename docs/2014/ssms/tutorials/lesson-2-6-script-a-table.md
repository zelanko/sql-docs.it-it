---
title: Generare lo script per una tabella | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22fae65a5e62be579f751dd3d6d3d0c9a73e7409
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316401"
---
# <a name="script-a-table"></a>Generare lo script per una tabella
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] consente di creare script per selezionare, inserire, aggiornare ed eliminare tabelle o per creare, modificare, eliminare o eseguire stored procedure.  
  
 Talvolta è necessario creare uno script con più opzioni disponibili, come ad esempio le opzioni per eliminare e poi creare una procedura o per creare una tabella e modificarne un'altra. Per creare script combinati, salvare il primo script in una finestra dell'editor di query e il secondo negli Appunti in modo da incollarlo nella finestra dopo il primo script.  
  
## <a name="creating-an-update-script"></a>Creazione di uno script di aggiornamento  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>Per creare lo script di inserimento per una tabella  
  
1.  In Esplora oggetti espandere il server, espandere **Database**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]e **Tabelle**, fare clic con il pulsante destro del mouse su **HumanResources.Employee**, quindi scegliere **Crea script per tabella**.  
  
2.  Menu di scelta rapida ha sette opzioni di scripting disponibili: **Per creare**, **SCENDE a**, **DROP e CREATE in**, **selezionare questa opzione per**, **dell'istruzione INSERT per**, **aggiornamento**, e **DELETE a**. Scegliere **Genera codice per istruzione UPDATE in**e quindi fare clic su **Nuova finestra editor di query**.  
  
3.  Viene aperta una finestra dell'editor di query che esegue una connessione e presenta l'intera istruzione di aggiornamento.  
  
     In questa procedura vengono illustrate le potenzialità della funzionalità di creazione di script per numerose operazioni e non soltanto per la creazione di tabelle e stored procedure. Questa nuova funzionalità consente di aggiungere rapidamente script per la manipolazione dei dati al progetto e per l'esecuzione di stored procedure. Ciò comporta un notevole risparmio di tempo nei casi di tabelle e procedure contenenti molti campi.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Riepilogo: Scrittura di codice Transact-SQL](../../tutorials/summary-writing-transact-sql.md)  
  
  
