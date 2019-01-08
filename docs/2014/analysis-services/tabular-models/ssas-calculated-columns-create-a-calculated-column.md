---
title: Creare una colonna calcolata (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 40e802ac33c7aa9b97267a725b20eb0d2f00dbb1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410358"
---
# <a name="create-a-calculated-column-ssas-tabular"></a>Creare una colonna calcolata (SSAS tabulare)
  Le colonne calcolate consentono di aggiungere nuovi dati al modello. Anziché incollare o importare i valori nella colonna, si crea una formula DAX che definisce i valori a livello di riga della colonna. I valori in ogni riga di una colonna calcolata vengono calcolati e popolati quando si crea una formula valida e si fa clic su INVIO. La colonna calcolata può essere aggiunta a un'applicazione di analisi o di creazione di report come qualsiasi altra colonna di dati. In questo argomento viene descritto come creare una nuova colonna calcolata tramite la barra della formula DAX in Progettazione modelli.  
  
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
 [Colonne calcolate &#40;SSAS tabulare&#41;](ssas-calculated-columns.md)   
 [Misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md)  
  
  
