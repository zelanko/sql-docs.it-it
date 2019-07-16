---
title: Prospettive in Analysis Services i modelli multidimensionali | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae14c0e76564ebcaffecb7591d14c283fffd2906
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208560"
---
# <a name="perspectives-in-multidimensional-models"></a>Prospettive nei modelli multidimensionali
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una prospettiva è un subset di un cubo creato per una determinata applicazione o un determinato gruppo di utenti. La prospettiva predefinita è costituita dal cubo. Una prospettiva viene esposta a un client come un cubo. Quando viene visualizzata da un utente, una prospettiva si presenta come un altro cubo. Qualsiasi modifica apportata ai dati del cubo tramite writeback nella prospettiva viene apportata al cubo originale. Per altre informazioni sulle viste in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [Prospettive](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Usare la scheda **Prospettive** di Progettazione cubi per creare o modificare prospettive in un cubo. Nella prima colonna **Oggetti cubo** della scheda **Prospettive** sono elencati tutti gli oggetti del cubo. Corrisponde alla prospettiva predefinita per il cubo, costituita dal cubo stesso.  
  
## <a name="creating-or-deleting-perspectives"></a>Creazione o eliminazione di prospettive  
 È possibile aggiungere una prospettiva alla scheda **Prospettive** scegliendo **Nuova prospettiva** dal menu **Cubo** . È anche possibile fare clic sul pulsante **Nuova prospettiva** sulla barra degli strumenti oppure fare clic con il pulsante destro del mouse in un punto qualsiasi del riquadro e quindi scegliere **Nuova prospettiva** dal menu di scelta rapida. A un cubo può essere aggiunto qualsiasi numero di prospettive.  
  
 Per rimuovere una prospettiva, fare innanzitutto clic su qualsiasi cella della colonna per la prospettiva che si desidera eliminare. Scegliere quindi **Elimina prospettiva** dal menu **Cubo**. È anche possibile fare clic sul pulsante **Elimina prospettiva** sulla barra degli strumenti oppure fare clic con il pulsante destro del mouse su qualsiasi cella della prospettiva che si desidera eliminare e quindi scegliere **Elimina prospettiva** dal menu di scelta rapida.  
  
## <a name="renaming-perspectives"></a>ridenominazione di prospettive  
 Nella prima riga di ogni prospettiva ne viene visualizzato il nome. Quando si crea una prospettiva, il nome corrisponde inizialmente a "Prospettiva", seguito da un numero ordinale a partire da 1 se è già presente una prospettiva denominata "Prospettiva". È possibile fare clic sul nome per modificarlo.  
  
## <a name="hiding-objects-from-a-perspective"></a>Come nascondere oggetti in una prospettiva  
 Per nascondere un oggetto in una prospettiva, deselezionare la casella di controllo nella riga corrispondente all'oggetto della colonna per la prospettiva. In una prospettiva possono essere nascosti gli oggetti del cubo seguenti:  
  
-   Gruppi di misure  
  
-   Misure  
  
-   Dimensioni  
  
-   Gerarchie  
  
-   Set denominati  
  
-   KPI  
  
-   Azioni  
  
-   Membri calcolati  
  
 Per visualizzare qualsiasi oggetto, espandere la categoria (**Gruppi di misure**, **Dimensioni**, **KPI**, **Calcoli**o **Azioni**) per qualsiasi tipo di oggetto in **Oggetti cubo**. Per visualizzare le gerarchie o gli attributi di una dimensione, espandere innanzitutto una dimensione e quindi la riga **Gerarchie** o **Attributi** . Per visualizzare le misure in un gruppo di misure, espandere il gruppo di misure.  
  
## <a name="see-also"></a>Vedere anche  
 [Cubi nei modelli multidimensionali](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
