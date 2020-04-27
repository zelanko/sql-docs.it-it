---
title: Annulla estrazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2057c78f953645c9b1a5915b9912ab99263cb005
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62773397"
---
# <a name="undo-checkouts"></a>Annullare estrazioni
  È possibile utilizzare il comando **Annulla estrazione** per annullare un'estrazione esistente. che risulta particolarmente utile quando è necessario eseguire il rollback delle modifiche dopo avere modificato e salvato un file.  
  
 A seconda delle opzioni impostate nella finestra di dialogo **Annulla estrazione avanzata opzioni** , l'ambiente Studio lascia la copia di lavoro dell'elemento sul disco locale o la sostituisce con la versione più recente controllata dal codice sorgente. Se l'elemento è stato modificato all'esterno del contesto del sistema di controllo del codice sorgente, è possibile che la versione recuperata non sia quella più recente.  
  
### <a name="to-undo-a-checkout"></a>Per annullare un'estrazione  
  
1.  In Esplora soluzioni selezionare il progetto.  
  
2.  Scegliere **controllo del codice sorgente**dal menu **file** , quindi fare clic su **Annulla estrazione**.  
  
3.  Nella finestra di dialogo **Annulla estrazione** selezionare le opzioni appropriate e quindi fare clic sul pulsante **Annulla estrazione** .  
  
     **Colonne**  
     Consente di specificare le colonne da visualizzare e il relativo ordine.  
  
     **Visualizzazione semplice**  
     Consente di visualizzare gli elementi come elenchi semplici sotto la relativa connessione del controllo del codice sorgente.  
  
     **Nome**  
     Consente di visualizzare i nomi degli elementi per i quali annullare l'estrazione. Accanto agli elementi viene visualizzata la casella di controllo selezionata. Se non si desidera annullare l'estrazione di un elemento, deselezionare la casella di controllo corrispondente.  
  
     **Opzioni**  
     Consente di visualizzare le opzioni di annullamento dell'estrazione specifiche del plug-in del controllo del codice sorgente quando si fa clic sulla freccia a destra del pulsante.  
  
     **Ordina**  
     Consente di eseguire l'ordinamento delle colonne visualizzate.  
  
     **Visualizzazione albero**  
     Consente di visualizzare la gerarchie di cartelle e di elementi per gli elementi di cui si sta annullando l'estrazione.  
  
     **Annulla estrazione**  
     Consente di annullare l'estrazione, eliminando le eventuali modifiche apportate al file estratto.  
  
## <a name="see-also"></a>Vedi anche  
 [Estrai file](../../2014/database-engine/check-out-files.md)   
 [Gestione delle estrazioni](../../2014/database-engine/manage-checkouts.md)  
  
  
