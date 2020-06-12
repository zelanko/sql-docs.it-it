---
title: Creazione di set denominati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculations [Analysis Services], named sets
- named sets [Analysis Services]
- members [Analysis Services], named sets
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6b5761e36bc98319665eaa779262502fd224aec8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535923"
---
# <a name="create-named-sets"></a>Creare set denominati
  Un set denominato è un set di membri delle dimensioni oppure un'espressione set creata per successivi utilizzi, ad esempio all'interno di query MDX (MultiDimensional Expressions). Per creare set denominati è possibile combinare dati di cubi, operatori aritmetici, numeri e funzioni. Ad esempio, è possibile creare un set denominato Top Ten Factories contenente i dieci membri della dimensione Factories con i valori più alti per la misura Production. Il set denominato Top Ten Factories può quindi essere utilizzato nelle query dagli utenti finali. Ad esempio, un utente finale può inserire Top Ten Factories su un asse e la dimensione Measures, che include la misura Production, su un altro asse. Per altre informazioni, vedere [Calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md) e [Compilazione di set denominati in MDX &#40;MDX&#41;](mdx/mdx-named-sets-building-named-sets.md).  
  
 Per creare un set denominato usare il comando **Nuovo set denominato** nella scheda **Calcoli** di Progettazione cubi. Questo comando è accessibile dal menu **Cubo** sulla barra degli strumenti della scheda **Calcoli** . e visualizza un form in cui è possibile specificare le opzioni seguenti per il set denominato:  
  
 **Nome**  
 Selezionare il nome del set denominato. Questo nome appare agli utenti finali quando visualizzano il cubo.  
  
 **Espressione**  
 Specificare l'espressione che genera il set denominato. Questa espressione può essere scritta in MDX e può contenere gli elementi seguenti:  
  
-   Espressioni di dati che rappresentano i componenti del cubo, quali dimensioni, livelli, misure e così via.  
  
-   Operatori aritmetici.  
  
-   Numeri.  
  
-   Funzioni.  
  
 È possibile copiare o trascinare componenti del cubo dalla scheda **Metadati** del riquadro **Strumenti di calcolo** nella casella **Espressione** del riquadro **Editor Form set denominato** . È possibile copiare o trascinare funzioni dalla scheda **Funzioni** del riquadro **Strumenti di calcolo** nella casella **Espressione** del riquadro **Editor Form set denominato** .  
  
> [!IMPORTANT]  
>  Se si crea l'espressione set assegnando in modo esplicito un nome ai membri del set, racchiudere l'elenco dei membri in una coppia di parentesi graffe ( {} ).  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md)  
  
  
