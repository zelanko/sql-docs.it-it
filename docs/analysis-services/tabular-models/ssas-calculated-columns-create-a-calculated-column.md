---
title: Creare una colonna calcolata in Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 705428d2c2a6671452a1d95e06e500f4860574e0
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071938"
---
# <a name="create-a-calculated-column"></a>Creare una colonna calcolata
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le colonne calcolate consentono di aggiungere nuovi dati al modello. Anziché incollare o importare i valori nella colonna, si crea una formula DAX che definisce i valori a livello di riga della colonna. I valori in ogni riga di una colonna calcolata vengono calcolati e popolati quando si crea una formula valida e si fa clic su INVIO. La colonna calcolata può essere aggiunta a un'applicazione di analisi o di creazione di report come qualsiasi altra colonna di dati. Questo articolo descrive come creare una nuova colonna calcolata usando la barra della formula DAX in Progettazione modelli.  
  
#### <a name="to-create-a-new-calculated-column"></a>Per creare una nuova colonna calcolata  
  
1.  In Vista dati di Progettazione modelli selezionare la tabella a cui si desidera aggiungere una colonna calcolata, fare clic sul menu **Colonna** , quindi scegliere **Aggiungi colonna**.  
  
     L'opzione**Aggiungi colonna** viene evidenziata nella colonna vuota più a destra e il cursore si sposta nella barra della formula.  
  
     Per creare una nuova colonna tra due colonne esistenti, fare clic con il pulsante destro del mouse su una colonna esistente e quindi scegliere **Inserisci colonna**.  
  
2.  Nella barra della formula effettuare una delle operazioni seguenti:  
  
    -   Digitare un segno di uguale seguito da una formula.  
  
    -   Digitare un segno di uguale, seguito da una funzione DAX e dagli argomenti e dai parametri come richiesto dalla funzione.  
  
    -   Fare clic sul pulsante della funzione (**fx**) e quindi nella finestra di dialogo **Inserisci funzione** selezionare una categoria e una funzione e fare clic su **OK**. Nella barra della formula digitare gli argomenti e i parametri restanti come richiesto dalla funzione.  
  
3.  Premere INVIO per accettare la formula.  
  
     L'intera colonna viene popolata con la formula e viene calcolato un valore per ogni riga.  
  
> [!TIP]  
>  È possibile utilizzare Completamento automatico formule DAX in una formula esistente con funzioni nidificate. Il testo immediatamente prima del punto di inserimento viene utilizzato per visualizzare i valori nell'elenco a discesa mentre tutto il testo dopo tale punto rimane invariato.  
  
## <a name="see-also"></a>Vedere anche  
 [Colonne calcolate](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Misure](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
