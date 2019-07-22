---
title: Dividere un set di dati tramite la trasformazione Suddivisione condizionale | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d6342cf8409a9133a5e21205b0864af97ceeac75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928100"
---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>Divisione di un set di dati tramite la trasformazione Suddivisione condizionale

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una trasformazione Suddivisione condizionale solo se il pacchetto include già almeno un'attività Flusso di dati e un'origine.  
  
### <a name="to-conditionally-split-a-dataset"></a>Per eseguire la suddivisione condizionale di un set di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**, trascinare la trasformazione Suddivisione condizionale sull'area di progettazione.  
  
4.  Connettere la trasformazione Suddivisione condizionale al flusso di dati trascinando il connettore dall'origine dati o dalla trasformazione precedente alla trasformazione Suddivisione condizionale.  
  
5.  Fare doppio clic sulla trasformazione Suddivisione condizionale.  
  
6.  Nella finestra di dialogo **Editor trasformazione Suddivisione condizionale**compilare le espressioni da usare come condizioni trascinando variabili, colonne, funzioni e operatori nella colonna **Condizione** della griglia. In alternativa, digitare l'espressione nella colonna **Condizione** .  
  
    > [!NOTE]  
    >  È possibile utilizzare una stessa variabile o colonna in più espressioni.  
  
    > [!NOTE]  
    >  Se l'espressione non è valida, il testo dell'espressione viene evidenziato e tramite una descrizione comando nella colonna vengono descritti gli errori.  
  
7.  Facoltativamente, modificare i valori nella colonna **Nome output** . I nomi predefiniti sono Case 1, Case 2 e così via.  
  
8.  Per modificare la sequenza in cui vengono valutate le condizioni, fare clic sulla freccia in su o sulla freccia in giù.  
  
    > [!NOTE]  
    >  Collocare le condizioni più probabili all'inizio dell'elenco.  
  
9. Facoltativamente, modificare il nome dell'output predefinito per le righe di dati che non soddisfano alcuna condizione.  
  
10. Per configurare un output degli errori, fare clic su **Configura output errori**. Per altre informazioni, vedere [Debug di un flusso di dati](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Fare clic su **OK**.  
  
12. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
