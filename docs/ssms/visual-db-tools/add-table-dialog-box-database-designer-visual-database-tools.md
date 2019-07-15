---
title: Finestra di dialogo Aggiungi tabella (Progettazione database) (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 52803db358a4a43ec7b5dc9064f940247f9515a2
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686564"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Finestra di dialogo Aggiungi tabella (Progettazione database) (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Consente di aggiungere tabelle in Progettazione database.  
  
> [!NOTE]  
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
**Aggiorna**  
Aggiorna l'elenco delle tabelle in modo che rispecchi lo stato corrente del database.  
  
**Aggiungi**  
Aggiunge la tabella o le tabelle selezionate.  
  
> [!NOTE]  
> Per aggiungere più tabelle al diagramma, è possibile selezionarle tutte prima di fare clic su **Aggiungi**. In alternativa, è possibile fare doppio clic su ogni tabella da aggiungere e al termine fare clic su **Chiudi** .  
  
**Chiudi**  
Chiude la finestra di dialogo senza aggiungere ulteriori tabelle.  
  
## <a name="see-also"></a>Vedere anche  
[Aggiunta di tabelle a diagrammi &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
