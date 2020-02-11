---
title: Aggiunta di un modello di regressione logistica alla struttura del Call Center (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 97abb77a-346c-44fa-8959-688dee1af6a8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 32e66a84dea20964c11c7de0aa568530aa8c28c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62823278"
---
# <a name="adding-a-logistic-regression-model-to-the-call-center-structure-intermediate-data-mining-tutorial"></a>Aggiunta di un modello di regressione logistica alla struttura del call center (Esercitazione intermedia sul data mining)
  Oltre ad analizzare i fattori che potrebbero influire sul funzionamento del call center, è inoltre necessario fornire alcuni consigli specifici su come il personale può migliorare la qualità del servizio. In questa attività verrà utilizzata la stessa struttura di data mining utilizzata per compilare il modello esplorativo e verrà aggiunto un modello di data mining che sarà utilizzato per la creazione di stime.  
  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] un modello di regressione logistica è basato sull'algoritmo Microsoft Neural Network e pertanto fornisce la stessa flessibilità e le funzionalità di un modello di rete neurale. La regressione logistica è tuttavia particolarmente appropriata per stimare risultati binari.  
  
 Per questo scenario si utilizzerà la stessa struttura di data mining utilizzata per il modello di rete neurale. Il nuovo modello verrà tuttavia personalizzato per soddisfare le esigenze aziendali. Si desidera migliorare la qualità del servizio e determinare quanti operatori esperti sono necessari, pertanto si configurerà il modello per stimare tali valori.  
  
 Per assicurarsi che i tutti i modelli basati sui dati del call center siano il più possibile simili, si utilizzerà lo stesso valore di inizializzazione precedente. L'impostazione del parametro del valore di inizializzazione assicura che il modello elabori i dati dallo stesso punto iniziale e riduca le variazioni causate dagli elementi nei dati.  
  
### <a name="to-add-a-new-mining-model-to-the-call-center-mining-structure"></a>Per aggiungere un nuovo modello di data mining alla struttura di data mining del call center  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Esplora soluzioni fare clic con il pulsante destro del mouse sulla struttura di data mining **Call Center**e scegliere **Apri finestra di progettazione**.  
  
2.  In Progettazione modelli di data mining fare clic sulla scheda **modelli di data mining** .  
  
3.  Fare clic su **Crea un modello di data mining correlato**.  
  
4.  Nella finestra di dialogo **nuovo modello di data mining** Digitare `Call Center - LR`per **nome modello**.  Per **Nome algoritmo**selezionare **regressione logistica Microsoft**.  
  
5.  Fare clic su **OK**.  
  
     Il nuovo modello di data mining viene visualizzato nella scheda **modelli di data mining** .  
  
### <a name="to-customize-the-logistic-regression-model"></a>Per personalizzare il modello di regressione logistica  
  
1.  Nella colonna per il nuovo modello di data mining `Call Center - LR`, lasciare fact callcenter ID come chiave.  
  
2.  Modificare il valore di ServiceGrade e di Level Two Operators in **Predict**.  
  
     Queste colonne verranno utilizzate sia per la stima che per l'input. In sostanza, si creano due modelli separati basati sugli stessi dati: uno che stima il numero di operatori e uno che stima il livello di servizio.  
  
3.  Modificare tutte le altre colonne in **input**.  
  
### <a name="to-specify-the-seed-and-process-the-models"></a>Per specificare il valore di inizializzazione ed elaborare i modelli  
  
1.  Nella scheda **modello di data mining** fare clic con il pulsante destro del mouse sulla colonna per il modello denominato Call Center-LR, quindi scegliere **Imposta parametri algoritmo**.  
  
2.  Nella riga relativa al parametro HOLDOUT_SEED fare clic sulla cella vuota in **valore**, quindi digitare `1`. Fare clic su **OK**.  
  
    > [!NOTE]  
    >  Il valore scelto come valore di inizializzazione non è importante, a condizione che si utilizzi lo stesso valore di inizializzazione per tutti i modelli correlati.  
  
3.  Scegliere **Elabora struttura di data mining e tutti i modelli**dal menu **modelli di data mining** . Fare clic su **Sì** per distribuire il progetto data mining aggiornato al server.  
  
4.  Nella finestra di dialogo **Elabora modello di data mining** fare clic su **Esegui**.  
  
5.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Stato elaborazione** , quindi fare di nuovo clic su **Chiudi** nella finestra di dialogo **Elabora modello di data mining** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di stime per i modelli di Call Center &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
