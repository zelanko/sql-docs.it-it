---
title: Aggiungere colonne a una tabella di modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726f7dd8ef72ad30bd055d2f76cc58c7db6183d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163121"
---
# <a name="add-columns-to-a-table"></a>Aggiungere colonne a una tabella
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive come aggiungere colonne a una tabella esistente.  
  
## <a name="add-columns-from-the-datasource"></a>Aggiungere colonne dall'origine dati  
 Quando si utilizza l'Importazione guidata tabella per importare dati da una tabella dell'origine dati, viene creata una nuova tabella del modello in cui sono incluse tutte le colonne nella tabella di origine oppure, se si sceglie di escludere determinate colonne utilizzando la funzionalità Visualizza anteprima e applica filtro, solo quelle colonne e quei dati filtrati vengono selezionati. È inoltre possibile scrivere una query SQL che consente di specificare solo determinate colonne da importare. Tuttavia, successivamente è possibile determinare che una tabella di origine disponga di colonne aggiuntive da aggiungere al modello oppure che sia necessario aggiungere una colonna calcolata con i valori derivati da una formula DAX.  
  
 Si supponga, ad esempio, che sia stata eseguita inizialmente un'importazione da un'origine dati utilizzando la funzionalità Visualizza anteprima e applica filtro nell'Importazione guidata tabella per selezionare un numero limitato di colonne dalla tabella di origine e che, in un secondo momento, si determini la necessità di aggiungere un'altra colonna che è disponibile nella tabella di origine, ma che non esiste ancora nella tabella del modello. Oppure, si supponga che sia stata aggiunta una nuova colonna AdjustedProfit alla tabella FactSales nell'origine dati e che si desideri aggiungere la stessa colonna AdjustedProfit e gli stessi dati alla tabella Sales nel modello.  
  
 In questi casi, è possibile utilizzare la finestra di dialogo Modifica proprietà tabella per selezionare colonne dalla tabella di origine e aggiungerle alla tabella del modello. Nella finestra di dialogo Modifica proprietà tabella è inclusa la finestra di anteprima della tabella in cui viene visualizzata la tabella nell'origine. Le colonne già incluse nella definizione della tabella del modello sono già selezionate, mentre non sono selezionate quelle non ancora incluse in tale definizione. È possibile aggiungere colonne dall'origine alla definizione della tabella del modello selezionando la colonna e facendo clic su OK. La finestra di anteprima della tabella nella finestra di dialogo Modifica proprietà tabella fornisce la stessa vista e le stesse funzionalità della finestra di anteprima della tabella nella pagina Visualizza anteprima e applica filtro dell'Importazione guidata tabella.  
  
> [!IMPORTANT]  
>  Quando si aggiunge una colonna a una tabella contenente due o più partizioni, prima di aggiungere la colonna alla definizione della tabella tramite la finestra di dialogo Modifica proprietà tabella, è necessario utilizzare innanzitutto Gestione partizioni per aggiungere la colonna a tutte le partizioni definite. Dopo aver aggiunto la colonna alle partizioni definite, è possibile aggiungere la stessa colonna alla definizione della tabella tramite la finestra di dialogo Modifica proprietà tabella.  
  
> [!NOTE]  
>  Se è stata utilizzata una query SQL per selezionare tabelle e colonne quando è stata utilizzata inizialmente l'Importazione guidata tabella per importare dati, è necessario utilizzare di nuovo una query SQL nella finestra di dialogo Modifica proprietà tabella per aggiungere colonne alla tabella del modello.  
  
#### <a name="to-add-a-column-from-the-data-source-by-using-the-edit-table-properties-dialog-box"></a>Per aggiungere una colonna dall'origine dati tramite la finestra di dialogo Modifica proprietà tabella  
  
1.  In Progettazione modelli fare clic sulla tabella in cui si vuole aggiungere una colonna, selezionare il menu **Tabella** e quindi scegliere  **Proprietà tabella**.  
  
2.  Nella finestra di anteprima della tabella della finestra di dialogo **Modifica proprietà tabella** selezionare la colonna di origine da aggiungere e quindi fare clic su OK. Le colonne già incluse nella definizione della tabella saranno già selezionate.  
  
## <a name="add-a-calculated-column"></a>Aggiungere una colonna calcolata  
 In una colonna calcolata una formula viene utilizzata per definire un valore per ogni riga. Ad esempio, è possibile creare una colonna calcolata con una formula semplice (=1), mediante la quale si aggiunge un valore 1 a ogni riga. Le colonne calcolate possono disporre anche di formule più complesse che consentono di calcolare valori in base ad altri dati nel modello. Tali colonne sono illustrate in modo più dettagliato in altri argomenti. Per altre informazioni, vedere [Colonne calcolate](../../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
#### <a name="to-create-a-calculated-column"></a>Per creare una colonna calcolata  
  
1.  In Vista dati di Progettazione modelli selezionare la tabella in cui si vuole aggiungere una nuova colonna calcolata vuota, scorrere fino alla colonna più a destra oppure fare clic sul menu **Colonna** e quindi scegliere **Aggiungi colonna**.  
  
     Per creare una nuova colonna tra due colonne esistenti, fare clic con il pulsante destro del mouse su una colonna esistente e quindi scegliere **Inserisci colonna**.  
  
2.  Nella barra della formula digitare una formula DAX per aggiungere attributi per ogni riga.  
  
## <a name="add-a-blank-column"></a>Aggiungere una colonna vuota  
 È possibile creare una colonna denominata, vuota in una tabella del modello. Le colonne vuote possono essere utili se si desidera incollare dati da un'altra origine. Tenere presente che i dati incollati vengono archiviati in modo diverso da quelli importati. Per altre informazioni, vedere [copiare e incollare dati](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
#### <a name="to-create-a-named-blank-column"></a>Per creare una colonna denominata, vuota  
  
1.  In Vista dati di Progettazione modelli selezionare la tabella in cui si vuole aggiungere una colonna vuota, scorrere fino alla colonna più a destra oppure fare clic sul menu **Colonna** e quindi scegliere **Aggiungi colonna**.  
  
     Per creare una nuova colonna tra due colonne esistenti, fare clic con il pulsante destro del mouse su una colonna esistente e quindi scegliere **Inserisci colonna**.  
  
2.  Fare clic sulla prima cella, quindi digitare un nome e premere INVIO.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica finestra di dialogo Proprietà tabella](http://msdn.microsoft.com/library/8d913e83-7246-44cc-8fc7-31729023c0d8)   
 [Modificare i mapping di filtri tabella, colonna o riga](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)  
  
  
