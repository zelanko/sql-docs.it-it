---
title: Definire gruppi di membri | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1da226353847409f1d808472dc155cb2055395cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179595"
---
# <a name="attribute-properties---define-member-groups"></a>Proprietà degli attributi - Definire gruppi di membri
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se un attributo include un numero elevato di membri, è possibile scegliere di raggruppare tali membri in bucket, riducendo il numero di membri visualizzati dagli utenti durante la ricerca dei dati in una gerarchia. È inoltre possibile determinare il numero di bucket in cui sono raggruppati i membri e impostare uno schema di denominazione per i bucket. Per altre informazioni, vedere [Raggruppare membri di attributo &#40;discretizzazione&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
 I membri vengono raggruppati impostando la proprietà **DiscretizationMethod**, accessibile tramite la finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Durante la creazione di gruppi di membri, le modifiche apportate non sono disponibili per gli utenti fino a quando non è stata elaborata la dimensione. Per altre informazioni, vedere [Elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Per creare gruppi di membri  
  
1.  Aprire la dimensione che si desidera utilizzare. Per impostazione predefinita, verrà visualizzata la scheda **Struttura dimensione** .  
  
2.  In **Attributi**fare clic con il pulsante destro del mouse sull'attributo di cui si vuole raggruppare i membri e quindi scegliere **Proprietà**.  
  
3.  Selezionare un metodo di raggruppamento dei membri nell'elenco a discesa accanto alla proprietà **DiscretizationMethod**. Per altre informazioni sulle impostazioni della proprietà **DiscretizationMethod**, vedere [Raggruppare membri di attributo &#40;discretizzazione&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
  
