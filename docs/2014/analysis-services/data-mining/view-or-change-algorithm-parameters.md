---
title: Visualizzare o modificare i parametri dell'algoritmo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services], algorithms
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7f41394c2adb8cbaaee2011e52ba6155a24e2e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082684"
---
# <a name="view-or-change-algorithm-parameters"></a>Visualizzare o modificare i parametri dell'algoritmo
  È possibile modificare i parametri forniti con gli algoritmi utilizzati per compilare modelli di data mining per personalizzare i risultati del modello.  
  
 I parametri dell'algoritmo forniti [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cambiano molto più delle sole proprietà del modello: possono essere usati per modificare in modo sostanziale la modalità di elaborazione, raggruppamento e visualizzazione dei dati. Ad esempio, è possibile utilizzare i parametri dell'algoritmo per effettuare le operazioni seguenti:  
  
-   Modificare il metodo di analisi, ad esempio il metodo di clustering.  
  
-   Controllare il comportamento di selezione delle funzionalità.  
  
-   Specificare le dimensioni dei set di elementi o la probabilità delle regole.  
  
-   Controllare la diramazione e la profondità degli alberi delle decisioni.  
  
-   Specificare un valore di inizializzazione o le dimensioni del set di dati di controllo interni utilizzato per la creazione del modello.  
  
 I parametri forniti per ogni algoritmo variano notevolmente; per un elenco dei parametri che è possibile impostare per ogni algoritmo, vedere gli argomenti di riferimento tecnici in questa sezione: [Algoritmi di data mining &#40;Analysis Services - Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="change-an-algorithm-parameter"></a>Modificare un parametro di un algoritmo  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse sul modello di data mining per il quale si vuole ottimizzare l'algoritmo e quindi scegliere **Imposta parametri algoritmo**.  
  
     Verrà visualizzata la finestra di dialogo **Parametri algoritmo** .  
  
2.  Nella colonna **Valore** impostare un nuovo valore per l'algoritmo che si vuole modificare.  
  
     Se non si immette un valore nella colonna **Valore** , in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene usato il valore predefinito del parametro. La colonna **Intervallo** descrive i valori che è possibile immettere.  
  
3.  Fare clic su **OK**.  
  
     Il parametro dell'algoritmo viene impostato con il nuovo valore. Le modifiche al parametro non verranno applicate al modello di data mining fino a quando non si rielabora il modello.  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>Visualizzare i parametri utilizzati in un modello esistente  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire una finestra di query DMX.  
  
2.  Digitare una query come la seguente:  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](mining-model-tasks-and-how-tos.md)  
  
  
