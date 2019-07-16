---
title: Esplorare i dati in una vista origine dati (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a7cb3d9895c7524bf0517270b50ac7830774dd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68177797"
---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Esplorare dati in una vista origine dati (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La finestra di dialogo **Esplora dati** in Progettazione vista origine dati di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] consente di esplorare i dati di una tabella, una vista o una query denominata in una vista origine dati. Quando si esplorano i dati in Progettazione vista origine dati, è possibile visualizzare il contenuto di ogni colonna di dati in una tabella, una vista o una query denominata selezionata. La visualizzazione del contenuto effettivo consente di determinare se sono necessarie tutte le colonne, se sono necessari calcoli denominati per incrementare la fruibilità e la facilità di utilizzo per gli utenti e se le query denominate o i calcoli denominati esistenti restituiscono i valori previsti.  
  
 Per visualizzare i dati, è necessario disporre di una connessione attiva alle origini dati per l'oggetto selezionato nella vista origine dati. Nella query vengono inviati anche i calcoli denominati contenuti in una tabella.  
  
 I dati restituiti in un formato tabulare che è possibile ordinare e copiare. Fare clic sull'intestazione di colonna per riordinare le righe in base alla colonna. È anche possibile evidenziare i dati nella griglia e premere CTRL-C per copiare la selezione negli Appunti.  
  
 È inoltre possibile controllare il metodo di campionamento e il conteggio campione. Per impostazione predefinita, vengono restituite le prime 5000 righe.  
  
## <a name="to-browse-data-or-change-sampling-options"></a>Per esplorare i dati o modificare le opzioni di campionamento  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si desidera esplorare i dati.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** , quindi fare doppio clic sulla vista origine dati.  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella, sulla vista o sulla query denominata contenente i dati che si desidera visualizzare, quindi scegliere **Esplora dati**.  
  
     L'origine dati sottostante la tabella, vista o query denominata nella vista origine dati sono le query e i risultati vengono visualizzati nei **Explore \<nome oggetto > tabella** scheda.  
  
4.  Nel **Explore \<nome dell'oggetto > tabella** sulla barra degli strumenti, fare clic sul **opzioni di campionamento** icona.  
  
     Verrà visualizzata la finestra di dialogo **Opzioni di esplorazione dati** . In tale finestra di dialogo è possibile specificare il metodo di campionamento (un numero di record inferiore o superiore alla dimensione di campionamento predefinita pari a 5000 righe) o il conteggio campione.  
  
5.  Fare clic su **OK** o **Annulla** , a seconda dei casi.  
  
6.  Per ricampionare i dati, fare clic su **Ricampiona dati** nel **Explore \<nome oggetto > tabella** sulla barra degli strumenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
