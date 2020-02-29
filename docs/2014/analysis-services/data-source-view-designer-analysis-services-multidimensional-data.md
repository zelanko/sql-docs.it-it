---
title: Progettazione vista origine dati (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd19f3a7f4978d2f8bcbd8e62cdf542e05437519
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175167"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>Progettazione vista origine dati (Analysis Services - Dati multidimensionali)
  Una vista origine dati è una vista logica di un'origine dati relazionale esterna utilizzata per creare cubi e dimensioni in un modello multidimensionale.

 Dopo la generazione di una vista origine dati, è possibile utilizzare **Progettazione vista origine dati** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per utilizzare direttamente la vista origine dati, un approccio che può essere utile se nell'origine dati sottostante mancano elementi dati necessari in un modello multidimensionale.

 Per aprire **Progettazione vista origine dati** :

-   Fare doppio clic su una vista origine dati in **Esplora soluzioni**.

-   Fare clic con il pulsante destro del mouse su una vista origine dati in **Esplora soluzioni** e scegliere **Apri** o **Progettazione viste**.

 In **Progettazione vista origine dati** è presente una barra degli strumenti, un diagramma che illustra oggetti e relazioni nella vista origine dati, un riquadro Tabelle con l'elenco in ordine alfabetico delle tabelle e delle query denominate e un riquadro Libreria diagrammi utilizzato per creare e visualizzare i diagrammi specifici della vista origine dati. È possibile fare clic con il pulsante destro del mouse su una tabella o una relazione per accedere ai comandi sensibili al contesto.

 ![Progettazione vista origine dati](media/ssas-dsvdesigner.PNG "Progettazione vista origine dati")

 In una vista origine dati vengono visualizzate almeno le tabelle di database relazionali che verranno utilizzate per popolare gli oggetti del modello durante l'elaborazione. Una vista origine dati viene solitamente generata tramite la Creazione guidata vista origine dati. Tabelle, colonne e relazioni nella vista origine dati diventano la base per dimensioni e misure in un cubo. Una volta creata la vista origine dati, è possibile utilizzare Progettazione vista origine dati per modificarla.

 La maggior parte degli sviluppatori di Analysis Services utilizza una vista origine dati così come viene generata, con alcune personalizzazioni. Questo avviene in genere se i dati di origine provengono da una vista in un database di SQL Server. In questo caso può essere preferibile gestire relazioni tra i dati e calcoli in una vista T-SQL anziché una vista origine dati di Analysis Services. Se tuttavia non si è il proprietario del database sottostante, è possibile modificare la vista origine dati in Analysis Services per sviluppare ulteriormente le strutture dei dati utilizzate nel modello.

## <a name="tasks-in-data-source-view-designer"></a>Attività in Progettazione vista origine dati
 Tramite la Progettazione vista origine dati è possibile apportare le seguenti modifiche a una vista origine dati:

|||
|-|-|
|Rinominare colonne o tabelle oppure creare nuove colonne calcolate. Ad esempio, concatenare un nome e un cognome in una nuova colonna per il nome completo.|[Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|
|Aggiungere manualmente relazioni tra tabelle.|[Definire relazioni logiche in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|
|Creare una query denominata per definire un nuovo oggetto basato su una query T-SQL.|[Definire query denominate in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|
|Esplorare i dati sottostanti per visualizzare i valori di dati effettivi rappresentati dagli oggetti del modello.<br /><br /> L'esplorazione dei dati consente di controllare visivamente e copiare i dati restituiti dalla query o dalla tabella dimensionale sottostante. L'esplorazione dei dati utilizza per impostazione predefinita la prima metodologia di campionamento di conteggio, con un conteggio di esempio di 5000, ma è possibile revisionare queste impostazioni.|[Esplorazione dei dati in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|
|Creare un diagramma di tutte o parte delle tabelle e relazioni in una vista origine dati.|[Utilizzare diagrammi in Progettazione vista origine dati &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|

## <a name="see-also"></a>Vedere anche
 [Viste origine dati in modelli multidimensionali](multidimensional-models/data-source-views-in-multidimensional-models.md) [l'aggiunta o la rimozione di tabelle o viste in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)


