---
title: Rimuovere join (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac2b8ca912f02aecc5e1b3e76d04d84b501db89b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253489"
---
# <a name="remove-joins-visual-database-tools"></a>Rimozione di join (Visual Database Tools)
  Se non si desidera che le tabelle siano unite in join mediante un inner join o un outer join, sarà possibile rimuovere il join che le unisce. È ad esempio possibile rimuovere un join tra due tabelle creato automaticamente da [Progettazione query e Progettazione viste](visual-database-tools.md) .  
  
> [!NOTE]  
>  La rimozione di un join da una query non modifica la relazione sottostante nel database.  
  
 Se le due tabelle in join fanno parte di una query e si rimuovono tutte le condizioni di join tra di esse, la query risultante diventerà il prodotto di entrambe le tabelle. In altre parole, si trasformerà in un CROSS JOIN.  
  
### <a name="to-remove-a-join"></a>Per rimuovere un join  
  
-   Nel [riquadro Diagramma](diagram-pane-visual-database-tools.md)selezionare la linea relativa al join da rimuovere, quindi premere CANC. È possibile selezionare e rimuovere più linee di join contemporaneamente.  
  
 In Progettazione query e Progettazione viste verrà rimossa la linea di join e modificata l'istruzione nel [riquadro SQL](sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Unire tabelle automaticamente &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md)   
 [Join manuale &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)   
 [Eseguire query con join &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  
