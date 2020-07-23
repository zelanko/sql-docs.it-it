---
title: Generare tabelle mirror e istanze di acquisizione di CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5b462a03b15042c6fbb801b121bb04a07b7966b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921596"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>Generare tabelle mirror e istanze di acquisizione di CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la pagina Generate Mirror Tables per generare le tabelle mirror per le tabelle incluse nell'istanza di CDC  
  
 Fare clic su **Run** per creare le tabelle mirror. Viene visualizzato lo stato di avanzamento della creazione di ogni tabella e un messaggio indica se ogni tabella mirror viene completata correttamente o con errori. Se si verifica un errore, fare clic su **Details** per visualizzare una finestra di dialogo contenente una spiegazione dell'errore.  
  
 Se alcune tabelle non vengono create completamente, è possibile scegliere di continuare o di eliminare tutte le tabelle che non sono state create completamente. Dopo avere completato la procedura guidata, è possibile decidere se correggere la tabella nel database di origine Oracle o se non utilizzarla nell'istanza di CDC. Se si corregge la tabella, è possibile aggiungerla alla modifica delle tabelle ( [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)).  
  
 Scegliere **Avanti** per aprire la pagina [Finish](../../integration-services/change-data-capture/finish.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)  
  
  
