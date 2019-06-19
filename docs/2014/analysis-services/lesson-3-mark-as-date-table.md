---
title: 'Lezione 4: Contrassegna come tabella data | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26877c4892b050cbf9c8dcc6553530dff513f8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078790"
---
# <a name="lesson-4-mark-as-date-table"></a>Lezione 4: Contrassegna come tabella data
  Nella lezione 2: Aggiungere dati, è importato una tabella delle dimensioni denominata DimDate. Poi rinominata la tabella DimDate, nella lezione 3: Rinominare colonne Data. Mentre nel modello questa tabella è ora denominata Date, può anche essere nota come *tabella data*, in quanto sono contenuti dati relativi a data e ora.  
  
 Ogni volta che si usano le funzioni di Business Intelligence per le gerarchie temporali nei calcoli, come accadrà più avanti per creare le misure, è necessario specificare le proprietà della tabella relativa alla data, tra cui una *tabella data* e un identificatore univoco *colonna data* in tale tabella. È quindi possibile creare relazioni valide tra altre tabelle e la tabella data, che sono necessarie per eseguire calcoli utilizzando le funzioni di Business Intelligence per le gerarchie temporali DAX.  
  
 In questa lezione si contrassegnerà la tabella data importata e rinominata come *tabella data* e la colonna data (nella tabella data) come *colonna data* (identificatore univoco). Gli utilizzi del nome che data possa creare confusione, ma si riceverà a breve l'idea.  
  
 Tempo stimato per il completamento della lezione: **3 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 3: Rinominare le colonne](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Per impostare Contrassegna come tabella data  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Data** .  
  
2.  Fare clic sul menu **Tabella** , selezionare **Data**, quindi scegliere **Contrassegna come tabella data**.  
  
3.  Nella casella di riepilogo **Data** della finestra di dialogo **Contrassegna come tabella data** selezionare la colonna **Data** come identificatore univoco.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 5: Creare relazioni](lesson-4-create-relationships.md).  
  
  
