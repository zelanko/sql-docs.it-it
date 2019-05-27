---
title: Rinominare una tabella o colonna (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9d9f11b8713ea26cd79e95b9edc3f36c0bf3564
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066692"
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>Rinominare una tabella o una colonna (SSAS tabulare)
  È possibile modificare il nome di una tabella durante il processo di importazione digitando un **Nome descrittivo** nella pagina **Selezione tabelle e viste** dell' **Importazione guidata tabella**. È possibile modificare anche i nomi di tabelle e colonne se si importano dati specificando una query nella pagina **Specifica di una query SQL** dell' **Importazione guidata tabella**.  
  
 Dopo aver aggiunto i dati al modello, il nome o titolo di una tabella viene visualizzato nella scheda della tabella nella parte inferiore di Progettazione modelli. È possibile modificare il nome della tabella al fine di assegnarne uno più appropriato. È possibile anche rinominare una colonna dopo l'aggiunta dei dati al modello. Questa opzione risulta particolarmente importante quando si importano dati da più origini e si vuole essere sicuri che le colonne nelle differenti tabelle abbiano nomi facilmente distinguibili.  
  
### <a name="to-rename-a-table"></a>Per rinominare una tabella  
  
1.  In Progettazione modelli fare clic con il pulsante destro del mouse sulla scheda contenente la tabella da rinominare, quindi scegliere **Rinomina**.  
  
2.  Digitare il nuovo nome.  
  
    > [!NOTE]  
    >  È possibile modificare altre proprietà di una tabella, incluse le informazioni di connessione e i mapping di colonne, tramite la finestra di dialogo **Modifica proprietà tabella** . Tuttavia, in questa finestra non è possibile modificare il nome.  
  
### <a name="to-rename-a-column"></a>Per rinominare una colonna  
  
1.  In Progettazione modelli fare doppio clic sull'intestazione della colonna da rinominare o fare clic con il pulsante destro del mouse e selezionare **Rinomina colonna** nel menu di scelta rapida.  
  
2.  Digitare il nuovo nome.  
  
## <a name="naming-requirements-for-columns-and-tables"></a>Requisiti di denominazione per colonne e tabelle  
 Nel nome di una tabella o di una colonna non è possibile utilizzare le parole e i caratteri seguenti:  
  
-   Spazi iniziali o finali  
  
-   Caratteri di controllo  
  
-   I caratteri seguenti (che non sono validi nei nomi degli oggetti di Analysis Services):., ': / \\*|? & % $! + = [] (){}<>  
  
-   Le parole chiave riservate di Analysis Services, inclusi i nomi delle funzioni e gli operatori MDX (Multidimensional Expressions) e DMX (Data Mining Extensions).  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>Effetto della ridenominazione su tabelle, colonne e calcoli esistenti  
 Modificando il nome di una tabella, si modifica il nome dell'oggetto tabella sottostante, che può contenere più colonne o misure. È pertanto necessario aggiornare tutte le colonne presenti nella tabella, nonché tutte le relazioni che coinvolgono la tabella, in modo che utilizzino il nuovo nome nelle relative definizioni. Tale aggiornamento viene eseguito automaticamente in alcuni casi. Le misure non sono aggiornate automaticamente.  
  
 È necessario aggiornare inoltre tutti i calcoli che utilizzano la tabella rinominata o le relative colonne, nonché i dati da essi derivati, che devono essere ricalcolati. A seconda del numero di tabelle e di calcoli interessati, l'operazione può richiedere del tempo prima di essere completata. Il momento migliore per rinominare le tabelle ricade pertanto nell'arco del processo di importazione o prima dell'inizio della compilazione di relazioni e calcoli complessi.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne &#40;SSAS tabulare&#41;](tables-and-columns-ssas-tabular.md)   
 [Importare da PowerPivot &#40;tabulare di SSAS&#41;](import-from-power-pivot-ssas-tabular.md)   
 [Importare da Analysis Services &#40;SSAS tabulare&#41;](import-from-analysis-services-ssas-tabular.md)  
  
  
