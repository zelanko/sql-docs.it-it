---
title: Eseguire il debug di uno script impostando punti di interruzione in un'attività e in un componente Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3a05344f1fc20e575566d0a0fa527ac64b32363f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968405"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Eseguire il debug di uno script impostando punti di interruzione in un'attività e in un componente Script
  In questa procedura viene descritto come impostare i punti di interruzione negli script utilizzati nell'attività e nel componente Script.  
  
 Dopo aver impostato i punti di interruzione nello script, nella finestra di dialogo Imposta punti di **interruzione- \<object name> ** vengono elencati i punti di interruzione, insieme ai punti di interruzione predefiniti.  
  
> [!IMPORTANT]  
>  In determinate circostanze, i punti di interruzione nell'attività Script e il componente Script vengono ignorati. Per ulteriori informazioni, vedere la sezione **debug dell'attività script** in [codifica e debug dell'attività script](../control-flow/script-task.md) e la sezione **debug del componente script** in [codifica e debug del componente script] (.. /extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.  
  
### <a name="to-set-a-breakpoint-in-script"></a>Per impostare un punto di interruzione in uno script  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  Fare doppio clic sul pacchetto che include lo script in cui si desidera impostare i punti di interruzione.  
  
3.  Per aprire l'attività Script, fare clic sulla scheda **Flusso di controllo**, quindi fare doppio clic sull'attività.  
  
4.  Per aprire il componente Script, fare clic sulla scheda **Flusso di dati**, quindi fare doppio clic sul componente.  
  
5.  Fare clic su **Script**, quindi su **Modifica script**.  
  
6.  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) individuare la riga di script in cui si vuole impostare un punto di interruzione, fare clic con il pulsante destro del mouse sulla riga, scegliere **Punto di interruzione** e quindi fare clic su **Inserisci punto di interruzione**.  
  
     Nella riga di codice verrà visualizzata l'icona del punto di interruzione.  
  
7.  Scegliere **Esci** dal menu **File**.  
  
8.  Fare clic su **OK**.  
  
9. Per salvare il pacchetto, scegliere **Salva elementi selezionati** dal menu **File** .  
  
  
