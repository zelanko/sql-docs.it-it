---
title: Usare un'espressione in un vincolo di precedenza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence constraints [Integration Services], adding expressions
- expressions [Integration Services], adding
ms.assetid: 601038bb-3b17-42ac-b09d-5b3a82fb6564
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 672d9c363f64037f5f40f51fc7c6cb1c4c3bc674
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054753"
---
# <a name="use-an-expression-in-a-precedence-constraint"></a>Utilizzo di un'espressione in un vincolo di precedenza
  Questa procedura descrive come aggiungere un'espressione a un vincolo di precedenza tramite la finestra di dialogo **Editor vincoli di precedenza** . È possibile aggiungere un'espressione a un vincolo di precedenza solo se il pacchetto include almeno due eseguibili, costituiti da attività o contenitori, connessi da un vincolo di precedenza.  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>Per aggiungere un'espressione a un vincolo di precedenza  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare doppio clic sul vincolo di precedenza. Verrà aperta la finestra di dialogo **Editor vincoli di precedenza** .  
  
5.  Selezionare **Espressione**, **Espressione e vincolo**o **Espressione o vincolo** nell'elenco **Operazione valutazione** .  
  
6.  Digitare un'espressione nella casella di testo **Espressione** o avviare Generatore di espressioni per creare un'espressione.  
  
7.  Per convalidare la sintassi dell'espressione, fare clic su **Test**.  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedi anche  
 [Vincoli di precedenza](control-flow/precedence-constraints.md)   
 [Connessione di attività e contenitori tramite un vincolo di precedenza predefinito](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Impostare il valore di un vincolo di precedenza tramite il menu di scelta rapida](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Impostare le proprietà di un vincolo di precedenza](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)  
  
  
