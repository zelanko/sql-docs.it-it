---
title: Aggregare valori in un set di dati tramite la trasformazione Aggregazione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f3e4a41f3fef4cb8b8d64de6015c5e3011490d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019537"
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>Aggregazione di valori in un set di dati utilizzando la trasformazione Aggregazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una trasformazione Aggregazione solo se il pacchetto include almeno un'attività Flusso di dati e un'origine.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>Per aggregare valori in un set di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**, trascinare la trasformazione Aggregazione sull'area di progettazione.  
  
4.  Connettere la trasformazione Aggregazione al flusso di dati trascinando un connettore dall'origine o da una trasformazione precedente alla trasformazione Aggregazione.  
  
5.  Fare doppio clic sulla trasformazione.  
  
6.  Nella finestra di dialogo **Editor trasformazione Aggregazione** fare clic sulla scheda **Aggregazioni** .  
  
7.  Nell'elenco **Colonne di input disponibili** selezionare le caselle di controllo corrispondenti alle colonne in cui si vogliono aggregare i valori. Le colonne selezionate verranno visualizzate nella tabella.  
  
    > [!NOTE]  
    >  È possibile selezionare una stessa colonna più volte e applicarvi più trasformazioni. Per identificare univocamente le aggregazioni, viene aggiunto un numero al nome predefinito dell'alias di output della colonna.  
  
8.  Facoltativamente, modificare il valore nelle colonne **Alias di output** .  
  
9. Per modificare l'operazione di aggregazione predefinita, **Group by**, selezionare un'operazione diversa nell'elenco **Operazione** .  
  
10. Per modificare il tipo di confronto predefinito, selezionare nella colonna **Flag di confronto** i singoli flag di confronto da usare. Per impostazione predefinita, nel confronto vengono ignorati i caratteri senza spaziatura, la distinzione tra maiuscole e minuscole, la distinzione tra Katakana e Hiragana e la larghezza dei caratteri.  
  
11. Facoltativamente, per l'aggregazione **Count distinct** specificare un numero esatto di valori distinct nella colonna **Chiavi conteggio valori distinct** oppure selezionare un numero approssimativo nella colonna **Scala conteggio valori distinct** .  
  
    > [!NOTE]  
    >  L'indicazione del numero dei valori distinct, esatto o approssimativo, consente di ottimizzare le prestazioni, perché la trasformazione può preallocare la quantità di memoria appropriata per l'esecuzione delle operazioni necessarie.  
  
12. Facoltativamente, fare clic su **Avanzate** e aggiornare il nome dell'output della trasformazione Aggregazione. Se le aggregazioni includono operazioni **Group By** , sarà possibile selezionare un numero approssimativo di valori di chiavi di raggruppamento nella colonna **Scala chiavi** oppure specificare un numero esatto di valori di chiavi di raggruppamento nella colonna **Chiavi** .  
  
    > [!NOTE]  
    >  L'indicazione del numero dei valori distinct, esatto o approssimativo, consente di ottimizzare le prestazioni, perché la trasformazione può preallocare la quantità di memoria appropriata per l'esecuzione delle operazioni necessarie.  
  
    > [!NOTE]  
    >  Le opzioni **Scala chiavi** e **Chiavi** si escludono a vicenda. Se si immettono valori in entrambe le colonne, verrà usato il valore più elevato di **Scala chiavi** e **Chiavi** .  
  
13. Facoltativamente, fare clic sulla scheda **Avanzate** e impostare gli attributi relativi all'ottimizzazione di tutte le operazioni eseguite dalla trasformazione Aggregazione.  
  
14. Fare clic su **OK**.  
  
15. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Aggregazione](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)  
  
  
