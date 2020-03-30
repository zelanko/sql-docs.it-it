---
title: Finestra di dialogo Aggiorna tabella
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 5af6b442486a1c80a1b9ec9f8d870f167c67de35
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246036"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>Finestra di dialogo Aggiorna tabella (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Questa finestra di dialogo consente di specificare la tabella da aggiornare.

Viene visualizzata quando nel riquadro Diagramma sono aperte più tabelle e si cambia il tipo di query in modo da disporre di una query di aggiornamento (Update).  

Selezionare la tabella da aggiornare e scegliere **OK**.

> [!NOTE]
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.

## <a name="see-also"></a>Vedere anche

[Creare query di aggiornamento](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)