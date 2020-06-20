---
title: Finestra di dialogo Aggiorna tabella (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 426c842b85d6404ba101b57a9b572107dbc76bb5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064258"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Finestra di dialogo Aggiorna tabella (Visual Database Tools)
  Questa finestra di dialogo consente di specificare la tabella da aggiornare.  
  
 Viene visualizzata quando nel riquadro Diagramma sono aperte più tabelle e si cambia il tipo di query in modo da disporre di una query di aggiornamento (Update).  
  
 Selezionare la tabella da aggiornare e quindi scegliere **OK**. \  
  
> [!NOTE]  
>  Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare query di aggiornamento &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
