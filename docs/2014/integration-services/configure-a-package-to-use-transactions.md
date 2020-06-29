---
title: Configurare un pacchetto per l'utilizzo di transazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 25c111830727c7ca75357a06a0eb40ebd00aee9f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434858"
---
# <a name="configure-a-package-to-use-transactions"></a>Configurazione di un pacchetto per l'utilizzo di transazioni
  Quando si configura un pacchetto per l'utilizzo di transazioni, sono disponibili due opzioni:  
  
-   Utilizzare una sola transazione per il pacchetto. In questo caso, è il pacchetto stesso che *inizializza* questa transazione, mentre le singole attività e i contenitori del pacchetto partecipano a questa unica transazione.  
  
-   Utilizzare più transazioni nel pacchetto. In questo caso, il pacchetto supporta le transazioni, ma sono le singole attività e i contenitori del pacchetto a inizializzare le transazioni.  
  
 Nelle procedure seguenti viene descritto come configurare entrambe le opzioni.  
  
## <a name="configuring-a-single-transaction"></a>Configurazione di una transazione singola  
 In questo caso, il pacchetto stesso inizializza un'unica transazione. Il pacchetto viene configurato per avviare la transazione impostando la proprietà TransactionOption del pacchetto su `Required` .  
  
 In questa unica transazione verranno quindi inserite le attività e i contenitori specifici. Per integrare un'attività o un contenitore in una transazione, impostare la proprietà TransactionOption dell'attività o del contenitore su `Supported` .  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>Per configurare un pacchetto per l'utilizzo di una transazione singola  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera configurare per l'utilizzo di una transazione.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo, quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su `Required` .  
  
6.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o il contenitore che si vuole integrare nella transazione e quindi scegliere **Proprietà**.  
  
7.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su `Supported` .  
  
    > [!NOTE]  
    >  Per integrare una connessione in una transazione, integrare nella transazione le attività che la utilizzano. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
8.  Ripetere i passaggi 6 e 7 per ogni attività e ogni contenitore che si desidera registrare nella transazione.  
  
## <a name="configuring-multiple-transactions"></a>Configurazione di più transazioni  
 In questo caso, il pacchetto supporta le transazioni ma non ne avvia alcuna. Il pacchetto viene configurato per supportare le transazioni impostando la proprietà TransactionOption del pacchetto su `Supported` .  
  
 Configurare quindi le attività e i contenitori desiderati all'interno del pacchetto in modo che inizializzino la transazione o vengano eseguiti con essa. Per configurare un'attività o un contenitore per avviare una transazione, impostare la proprietà TransactionOption dell'attività o del contenitore su `Required` .  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>Per configurare un pacchetto per l'utilizzo di più transazioni  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera configurare per l'utilizzo delle transazioni.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo, quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su `Supported` .  
  
    > [!NOTE]  
    >  Il pacchetto supporta le transazioni, ma le transazioni vengono avviate da attività o contenitori nel pacchetto.  
  
6.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o il contenitore del pacchetto per il quale si vuole avviare una transazione e quindi scegliere **Proprietà**.  
  
7.  Nella finestra **Proprietà** impostare la proprietà TransactionOption su `Required` .  
  
8.  Se la transazione viene avviata da un contenitore, fare clic con il pulsante destro del mouse sull'attività o il contenitore che si vuole includere nella transazione e quindi scegliere **Proprietà**.  
  
9. Nella finestra **Proprietà** impostare la proprietà TransactionOption su `Supported` .  
  
    > [!NOTE]  
    >  Per integrare una connessione in una transazione, integrare nella transazione le attività che la utilizzano. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md).  
  
10. Ripetere i passaggi da 6 a 9 per ogni attività e ogni contenitore che avvierà una transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni di Integration Services](integration-services-transactions.md)  
  
  
