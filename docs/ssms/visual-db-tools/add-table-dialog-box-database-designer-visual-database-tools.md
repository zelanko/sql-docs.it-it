---
title: Finestra di dialogo Aggiungi tabella (Progettazione database)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 9c005a61a742a0c589cf5ccc26f818b8479b6a14
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000768"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Finestra di dialogo Aggiungi tabella (Progettazione database) (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Consente di aggiungere tabelle in Progettazione database.  
  
> [!NOTE]  
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
**Aggiorna**  
Aggiorna l'elenco delle tabelle in modo che rispecchi lo stato corrente del database.  
  
**Aggiungere**  
Aggiunge la tabella o le tabelle selezionate.  
  
> [!NOTE]  
> Per aggiungere più tabelle al diagramma, è possibile selezionarle tutte prima di fare clic su **Aggiungi**. In alternativa, è possibile fare doppio clic su ogni tabella da aggiungere e al termine fare clic su **Chiudi** .  
  
**Close**  
Chiude la finestra di dialogo senza aggiungere ulteriori tabelle.  
  
## <a name="see-also"></a>Vedere anche  
[Aggiunta di tabelle a diagrammi &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
