---
title: Sostituire una tabella o una Query denominata in una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- replacing tables
- data source views [Analysis Services], tables
- named queries [Analysis Services], replacing tables
- tables [Analysis Services], data source views
- partitions [Analysis Services], named queries
ms.assetid: 60c2a018-1299-4915-b60e-e73316524def
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9f1863fc3d707614b7c957dc5ef49561272d6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073126"
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>Sostituire una tabella o una query denominata in una vista origine dati (Analysis Services)
  In Progettazione vista origine dati è possibile sostituire una tabella, una vista o una query denominata di una vista origine dati con una tabella o una vista diversa della stessa origine dati o di un'origine diversa oppure con una query denominata definita nella vista origine dati. Quando si sostituisce una tabella, vengono mantenuti i relativi riferimenti eventualmente contenuti in tutti gli altri oggetti di un database o un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in quanto l'ID oggetto per la tabella della vista origine dati rimane invariato. Vengono mantenute anche le relazioni che sono ancora rilevanti, basate sulla corrispondenza tra nome e tipo di colonna. Se invece si elimina e quindi si aggiunge una tabella, i riferimenti e le relazioni vengono persi e devono essere ricreati.  
  
 Per sostituire una tabella con un'altra tabella, è necessario disporre di una connessione attiva all'origine dei dati in Progettazione vista origine dati in modalità progetto.  
  
 In genere, si sostituisce una tabella della vista origine dati con un'altra tabella dell'origine dei dati. È tuttavia possibile sostituire anche una query denominata con una tabella. Si supponga ad esempio di aver sostituito in precedenza una tabella con una query denominata che ora si desidera riconvertire in tabella.  
  
> [!IMPORTANT]  
>  Se si rinomina una tabella in un'origine dati, è necessario seguire la procedura per la sostituzione di una tabella e specificare la tabella rinominata come origine della tabella corrispondente nella vista origine dati prima di aggiornare la vista. Se si completa la sostituzione e si rinomina il processo, verranno mantenuti sia la tabella sia i riferimenti e le relazioni corrispondenti nella vista origine dati. In caso contrario, quando si aggiorna la vista origine dati, una tabella rinominata nell'origine dati verrà considerata come un elemento da eliminare. Per altre informazioni, vedere [Aggiornare lo schema in una vista origine dati &#40;Analysis Services&#41;](refresh-the-schema-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_nq"></a> Sostituire una tabella con una query denominata  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si vuole sostituire una tabella o una query denominata.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** e quindi fare doppio clic sulla vista origine dati.  
  
3.  Aprire la finestra di dialogo **Crea query denominata** . Nel riquadro **Tabelle** o **Diagramma** fare clic con il pulsante destro del mouse sulla tabella da sostituire, scegliere **Sostituisci tabella** e quindi fare clic su **Con nuova query denominata**.  
  
4.  Nella finestra di dialogo **Crea query denominata** definire la query denominata e quindi fare clic su **OK**.  
  
5.  Salvare la vista origine dati modificata.  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>Sostituire una tabella o una query denominata con una tabella  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si vuole sostituire una tabella o una query denominata.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** e quindi fare doppio clic sulla vista origine dati.  
  
3.  Aprire la finestra di dialogo **Sostituisci tabella con un'altra tabella** . Nel riquadro **Tabelle** o **Diagramma** fare clic con il pulsante destro del mouse sulla tabella o sulla query denominata da sostituire, scegliere **Sostituisci tabella** e quindi fare clic su **Con altra tabella**.  
  
4.  Nella finestra di dialogo **Sostituisci tabella con un'altra tabella** :  
  
    1.  Nell'elenco a discesa **Origine dati** selezionare l'origine dati desiderata.  
  
    2.  Selezionare la tabella con cui si desidera sostituire la tabella o la query denominata.  
  
5.  Fare clic su **OK**.  
  
6.  Salvare la vista origine dati modificata.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)  
  
  
