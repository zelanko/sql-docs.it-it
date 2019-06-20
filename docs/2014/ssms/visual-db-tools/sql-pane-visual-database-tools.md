---
title: Riquadro SQL (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd223c0a66b533cb2b405dd0e766f7053b7a4e89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63275973"
---
# <a name="sql-pane-visual-database-tools"></a>Riquadro SQL (Visual Database Tools)
  Utilizzando il riquadro SQL è possibile creare un'istruzione SQL personalizzata. Per creare un'istruzione, è anche possibile utilizzare i riquadri Criteri e Diagramma, ma in questo caso le istruzioni SQL verranno comunque create nel riquadro SQL. Mentre si compila la query, il riquadro SQL viene aggiornato e riformattato automaticamente in modo da semplificarne la lettura.  
  
 Per aprire il riquadro SQL, aprire innanzitutto Progettazione query e Progettazione viste (con un oggetto di database selezionato in Esplora server, scegliere **Nuova query** dal menu **Database**). A questo punto, scegliere **Riquadro** dal menu **Progettazione query** e fare clic su **SQL**.  
  
 Nel riquadro SQL è possibile:  
  
-   Creare nuove query immettendo istruzioni SQL.  
  
-   Modificare l'istruzione SQL creata da Progettazione query e Progettazione viste in base alle impostazioni definite nei riquadri Diagramma e Criteri.  
  
-   Immettere istruzioni che sfruttano caratteristiche specifiche del database utilizzato.  
  
> [!NOTE]  
>  È importante conoscere le regole che consentono di identificare gli oggetti di database nel database utilizzato. Per informazioni dettagliate, vedere la documentazione relativa al sistema di gestione di database in uso.  
  
## <a name="statements-in-the-sql-pane"></a>Istruzioni nel riquadro SQL  
 È possibile modificare la query corrente direttamente nel riquadro SQL. Quando ci si sposta in un altro riquadro, l'istruzione viene formattata automaticamente in Progettazione query e Progettazione viste, quindi i riquadri Diagramma e Criteri vengono modificati in base all'istruzione.  
  
 Se l'istruzione non può essere rappresentata nei riquadri Diagramma e Criteri e se tali riquadri sono visibili, in Progettazione query e Progettazione viste verrà generato un errore e sarà possibile scegliere di procedere in due modi:  
  
-   Ignorare il fatto che l'istruzione non può essere rappresentata nei riquadri Diagramma e Criteri.  
  
-   Annullare la modifica che non può essere rappresentata e ripristinare la versione più recente dell'istruzione SQL.  
  
 Se si sceglie di ignorare il fatto che l'istruzione non può essere rappresentata nei riquadri Diagramma e Criteri, in Progettazione query e Progettazione viste gli altri riquadri saranno visualizzati con colori più sfumati in modo da indicare che non riflettono più il contenuto del riquadro SQL.  
  
 È possibile continuare a modificare l'istruzione ed eseguirla come qualsiasi istruzione SQL.  
  
> [!NOTE]  
>  Se si immette un'istruzione SQL ma successivamente si apportano ulteriori modifiche alla query, cambiando i riquadri Diagramma e Criteri, l'istruzione SQL verrà ricompilata e visualizzata nuovamente in Progettazione query e Progettazione viste. In alcuni casi, questa operazione ha come risultato un'istruzione SQL con una struttura diversa rispetto all'istruzione SQL immessa in origine (anche se i risultati generati sono gli stessi). Questa differenza è particolarmente frequente quando si utilizzano condizioni di ricerca che richiedono numerose clausole collegate con operatori AND e OR.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di query &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Eseguire query &#40;Visual Database Tools&#41;](run-queries-visual-database-tools.md)   
 [Procedure per le query e visualizzazioni di progettazione &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Riquadro Diagramma &#40;Visual Database Tools&#41;](diagram-pane-visual-database-tools.md)   
 [Riquadro Criteri &#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md)   
 [Riquadro Risultati &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)  
  
  
