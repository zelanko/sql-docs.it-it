---
title: Estendere un set di dati tramite la trasformazione Merge join | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c3e144b1e866bd4bce8b7f8709c11f5b125b1f84
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291435"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>Estensione di un set di dati tramite la trasformazione Merge join

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una trasformazione Merge join solo se il pacchetto include già almeno un'attività Flusso di dati e due componenti flusso di dati che forniscono input alla trasformazione Merge join.  
  
 La trasformazione Merge join richiede due input ordinati. Per altre informazioni, vedere [Ordinare i dati per le trasformazioni Unione e Merge join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="to-extend-a-dataset"></a>Per estendere un set di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**trascinare la trasformazione Merge join sull'area di progettazione.  
  
4.  Connettere la trasformazione Merge join al flusso di dati trascinando il connettore da un'origine dati o una trasformazione precedente alla trasformazione Merge join.  
  
5.  Fare doppio clic sulla trasformazione Merge join.  
  
6.  Nella finestra di dialogo **Editor trasformazione Merge join** selezionare il tipo di join da usare nell'elenco **Tipo di join** .  
  
    > [!NOTE]  
    >  Se si seleziona il tipo **Left outer join** è possibile fare clic su **Inverti ordine input** per invertire gli input e convertire il left outer join in un right outer join.  
  
7.  Trascinare le colonne nell'input di sinistra verso quelle dell'input di destra per specificare le colonne di join. Se le colonne hanno lo stesso nome, sarà possibile selezionare la casella di controllo **Chiave di join** per creare il join automaticamente.  
  
    > [!NOTE]  
    >  È possibile creare join solo tra colonne con la stessa posizione di ordinamento e nell'ordine specificato dalla posizione di ordinamento. Se si tenta di creare i join senza rispettare l'ordine, **Editor trasformazione Merge join** richiederà di creare join aggiuntivi per le posizioni di ordinamento ignorate.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, l'output viene ordinato in base alle colonne di join.  
  
8.  Negli input sinistro e destro selezionare le caselle di controllo corrispondenti alle colonne aggiuntive da includere nell'output. Le colonne di join vengono incluse per impostazione predefinita.  
  
9. Facoltativamente, aggiornare i nomi delle colonne di output nella colonna **Alias di output** .  
  
10. Fare clic su **OK**.  
  
11. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)  
  
  
