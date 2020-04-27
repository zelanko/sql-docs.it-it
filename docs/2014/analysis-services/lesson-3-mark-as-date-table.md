---
title: 'Lezione 4: contrassegnare come tabella data | Microsoft Docs'
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078790"
---
# <a name="lesson-4-mark-as-date-table"></a>Lezione 4: Contrassegna come tabella data
  Nella Lezione 2: Aggiungere dati è stata importata una tabella delle dimensioni denominata DimDate. Nella Lezione 3: Rinominare colonne è stato quindi modificato il nome della tabella DimDate in Data. Mentre nel modello questa tabella è ora denominata Date, può anche essere nota come *tabella data*, in quanto sono contenuti dati relativi a data e ora.  
  
 Ogni volta che si usano le funzioni di Business Intelligence per le gerarchie temporali nei calcoli, come accadrà più avanti per creare le misure, è necessario specificare le proprietà della tabella relativa alla data, tra cui una *tabella data* e un identificatore univoco *colonna data* in tale tabella. È quindi possibile creare relazioni valide tra altre tabelle e la tabella data, che sono necessarie per eseguire calcoli utilizzando le funzioni di Business Intelligence per le gerarchie temporali DAX.  
  
 In questa lezione si contrassegnerà la tabella data importata e rinominata come *tabella data* e la colonna data (nella tabella data) come *colonna data* (identificatore univoco). L'uso della data Name può creare confusione, ma si otterrà presto un'idea.  
  
 Tempo stimato per il completamento della lezione: **3 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 3: Rinominare colonne](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Per impostare Contrassegna come tabella data  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Data** .  
  
2.  Scegliere **Data**dal menu **tabella** , quindi fare clic su **Contrassegna come tabella data**.  
  
3.  Nella casella di riepilogo **Data** della finestra di dialogo **Contrassegna come tabella data** selezionare la colonna **Data** come identificatore univoco.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 5: Creare relazioni](lesson-4-create-relationships.md).  
  
  
