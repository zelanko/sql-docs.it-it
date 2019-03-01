---
title: Ordinamento interattivo (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4124b909cf35ea071aef5f57672ff8a3701a44ca
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286369"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>Ordinamento interattivo (Generatore report e SSRS)
  È possibile aggiungere pulsanti di ordinamento interattivo per consentire a un utente di passare dall'ordine crescente a quello decrescente e viceversa per le righe di una tabella o per le righe e le colonne di una matrice. In genere l'ordinamento interattivo viene utilizzato per aggiungere un pulsante di ordinamento a ogni intestazione di colonna. L'utente può quindi scegliere la colonna in base alla quale eseguire l'ordinamento.  
  
 È tuttavia possibile aggiungere un pulsante di ordinamento interattivo a qualsiasi casella di testo, non solo alle intestazioni di colonna. Per una casella di testo in una riga al di fuori di un gruppo di righe, è ad esempio possibile specificare un ordinamento per le righe o le colonne del gruppo padre, del gruppo figlio o per le righe o le colonne di dettaglio. È inoltre possibile combinare più campi in una sola espressione di raggruppamento e quindi ordinare per più campi.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Quando si aggiunge un ordinamento interattivo, è necessario specificare quanto segue:  
  
-   **Tipo di ordinamento:** per righe o colonne.  
  
-   **Elemento in base al quale eseguire l'ordinamento:** un campo visualizzato in una colonna della tabella o un campo non visualizzato.  
  
-   **Contesto in cui eseguire l'ordinamento:** ad esempio, nelle righe associate a gruppi di righe, nelle colonne associate a gruppi di colonne, nelle righe di dettaglio, nei gruppi figlio all'interno di un gruppo padre o in gruppi padre e figlio insieme.  
  
-   **Casella di testo a cui aggiungere il pulsante di ordinamento:** nell'intestazione della colonna o nell'intestazione della riga di gruppo.  
  
-   **Eventuale sincronizzazione dell'ordinamento per più aree dati:** è possibile progettare un report per far sì che quando l'utente passa da un ordinamento all'altro vengano ordinate anche le altre aree dati con lo stesso predecessore.  
  
 Per istruzioni dettagliate, vedere [Aggiungere un ordinamento interattivo a una tabella o a una matrice &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Nella tabella seguente sono riepilogati gli effetti che è possibile ottenere tramite i pulsanti di ordinamento interattivo.  
  
|Azione|Elemento da ordinare|Posizione in cui aggiungere il pulsante di ordinamento|Elemento in base al quale effettuare l'ordinamento|Ambito dell'ordinamento|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|Ordinamento delle righe di dettaglio di una tabella senza gruppi|Dettagli|Intestazione della colonna|Campo del set di dati associato alla colonna|Area dati|  
|Ordinamento delle istanze di gruppo di livello superiore per una matrice|Gruppi|Intestazione della colonna|Espressione di raggruppamento per gruppo padre|Area dati|  
|Ordinamento delle righe di dettaglio per un gruppo figlio in una tabella|Dettagli|Riga dell'intestazione del gruppo figlio|Campo del set di dati in base al quale ordinare|Gruppo figlio|  
|Ordinamento delle righe per più gruppi di righe e righe di dettaglio in una tabella|Gruppi, ma è necessario ridefinire l'espressione di raggruppamento|Intestazione della colonna|Aggregazione del campo del set di dati in base al quale eseguire l'ordinamento|Area dati|  
|Sincronizzazione dell'ordinamento per più aree dati|Gruppi|In genere, intestazione della colonna|Espressione di raggruppamento|Set di dati|  
  
 Il componente Elaborazione report applica l'ordinamento interattivo dopo aver applicato le espressioni di ordinamento di tutti i gruppi e di tutte le aree dati. Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>Aggiunta dell'ordinamento interattivo per più gruppi  
 In una tabella che include gruppi di righe nidificati, ciascuno dei quali basato su un solo campo del set di dati, è possibile aggiungere un pulsante di ordinamento interattivo che ordini i valori del gruppo padre, quelli del gruppo figlio o delle righe di dettaglio. Tuttavia, potrebbe essere necessario mettere l'utente in condizione di ordinare la tabella in base ai valori del gruppo padre e figlio senza dovere fare clic più volte.  
  
 A questo scopo, è necessario riprogettare la tabella affinché venga raggruppata in un'espressione che combina più campi. Per un set di dati che include i conteggi dell'inventario, ad esempio, se nella tabella originale il raggruppamento è stato effettuato in base alla dimensione, quindi al colore, è possibile specificare un singolo gruppo con un'espressione di raggruppamento che rappresenti una combinazione di dimensione e colore. Per altre informazioni, vedere [Aggiungere un ordinamento interattivo a una tabella o a una matrice &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Ordinamento dei dati in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Aggiungere un ordinamento interattivo a una tabella o a una matrice &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
