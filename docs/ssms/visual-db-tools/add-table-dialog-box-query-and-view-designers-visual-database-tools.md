---
title: Finestra di dialogo Aggiungi tabella (Progettazione query e Progettazione visualizzazioni)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.query.addtable
- vdtsql.chm:65565
ms.assetid: fce7adcc-4cf5-4a52-9203-11c13d1ecf08
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 167b1e86c28a56c9d3159a4e01fe337ba428e1b7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253402"
---
# <a name="add-table-dialog-box-query-and-view-designers-visual-database-tools"></a>Finestra di dialogo Aggiungi tabella (Progettazione query e Progettazione viste) (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Questa finestra di dialogo consente di aggiungere tabelle, viste, funzioni definite dall'utente o sinonimi a una query o a una vista.  
  
> [!NOTE]  
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="options"></a>Opzioni  
**Tabelle**  
Elenca le tabelle che è possibile aggiungere al riquadro **Diagramma** . Per aggiungere una tabella, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più tabelle, selezionarle e fare clic su **Aggiungi**.  
  
**Visualizzazioni**  
Elenca le viste che è possibile aggiungere al riquadro **Diagramma** . Per aggiungere una vista, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più viste, selezionarle e fare clic su **Aggiungi**.  
  
**Funzioni**  
Elenca le funzioni definite dall'utente che è possibile aggiungere al riquadro **Diagramma** . Per aggiungere una funzione, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più funzioni, selezionarle e fare clic su **Aggiungi**.  
  
**Sinonimi**  
Elenca i sinonimi che è possibile aggiungere al riquadro **Diagramma** . Per aggiungere un sinonimo, selezionarlo e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più sinonimi, selezionarli e fare clic su **Aggiungi**.  
  
**Aggiorna**  
Aggiorna l'elenco includendo tutte le modifiche apportate al database da quando l'elenco è stato recuperato l'ultima volta.  
  
**Aggiungere**  
Aggiunge l'elemento o gli elementi selezionati.  
  
## <a name="see-also"></a>Vedere anche  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
