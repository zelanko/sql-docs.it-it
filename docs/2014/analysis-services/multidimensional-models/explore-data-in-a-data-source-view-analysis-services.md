---
title: Esplorazione dei dati in una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- exploring data [Analysis Services]
- data source views [Analysis Services], exploring data
- viewing source data
ms.assetid: 2c922c35-fbcb-45b2-96b1-c7a846d8b419
author: minewiskan
ms.author: owend
ms.openlocfilehash: 28db322a38ae90206ae0c43db1c8c039e6395b8b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546743"
---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Esplorare dati in una vista origine dati (Analysis Services)
  La finestra di dialogo **Esplora dati** in Progettazione vista origine dati di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] consente di esplorare i dati di una tabella, una vista o una query denominata in una vista origine dati. Quando si esplorano i dati in Progettazione vista origine dati, è possibile visualizzare il contenuto di ogni colonna di dati in una tabella, una vista o una query denominata selezionata. La visualizzazione del contenuto effettivo consente di determinare se sono necessarie tutte le colonne, se sono necessari calcoli denominati per incrementare la fruibilità e la facilità di utilizzo per gli utenti e se le query denominate o i calcoli denominati esistenti restituiscono i valori previsti.  
  
 Per visualizzare i dati, è necessario disporre di una connessione attiva alle origini dati per l'oggetto selezionato nella vista origine dati. Nella query vengono inviati anche i calcoli denominati contenuti in una tabella.  
  
 I dati restituiti in un formato tabulare che è possibile ordinare e copiare. Fare clic sull'intestazione di colonna per riordinare le righe in base alla colonna. È anche possibile evidenziare i dati nella griglia e premere CTRL-C per copiare la selezione negli Appunti.  
  
 È inoltre possibile controllare il metodo di campionamento e il conteggio campione. Per impostazione predefinita, vengono restituite le prime 5000 righe.  
  
## <a name="to-browse-data-or-change-sampling-options"></a>Per esplorare i dati o modificare le opzioni di campionamento  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si desidera esplorare i dati.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** e quindi fare doppio clic sulla vista origine dati.  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella, sulla vista o sulla query denominata contenente i dati che si desidera visualizzare, quindi scegliere **Esplora dati**.  
  
     L'origine dati sottostante la tabella, la vista o la query denominata nella vista origine dati è una query e i risultati vengono visualizzati nella scheda **Esplora \<object name> tabella** .  
  
4.  Sulla barra degli strumenti **Esplora \<object name> tabella** fare clic sull'icona **Opzioni di campionamento** .  
  
     Verrà visualizzata la finestra di dialogo **Opzioni di esplorazione dati** . In tale finestra di dialogo è possibile specificare il metodo di campionamento (un numero di record inferiore o superiore alla dimensione di campionamento predefinita pari a 5000 righe) o il conteggio campione.  
  
5.  Fare clic su **OK** o **Annulla** , a seconda dei casi.  
  
6.  Per ricampionare i dati, fare clic su **Ricampiona dati** sulla barra degli strumenti della ** \<object name> tabella Esplora** .  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)  
  
  
