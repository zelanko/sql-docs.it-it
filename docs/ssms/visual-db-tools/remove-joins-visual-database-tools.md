---
title: Rimuovere join (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: 125da46c853c66d79abc7a28efa5000223711f50
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532822"
---
# <a name="remove-joins-visual-database-tools"></a>Rimozione di join (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Se non si desidera che le tabelle siano unite in join mediante un inner join o un outer join, sarà possibile rimuovere il join che le unisce. È ad esempio possibile rimuovere un join tra due tabelle creato automaticamente da [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) .  
  
> [!NOTE]  
> La rimozione di un join da una query non modifica la relazione sottostante nel database.  
  
Se le due tabelle in join fanno parte di una query e si rimuovono tutte le condizioni di join tra di esse, la query risultante diventerà il prodotto di entrambe le tabelle. In altre parole, si trasformerà in un CROSS JOIN.  
  
### <a name="to-remove-a-join"></a>Per rimuovere un join  
  
-   Nel [riquadro Diagramma](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)selezionare la linea relativa al join da rimuovere, quindi premere CANC. È possibile selezionare e rimuovere più linee di join contemporaneamente.  
  
In Progettazione query e Progettazione viste verrà rimossa la linea di join e modificata l'istruzione nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
[Unione di tabelle in modo automatico &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)  
[Unione di tabelle in modo manuale &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)  
[Eseguire query con join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
