---
title: Aggiungere un attributo a una dimensione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c45184e5be13193dc8b77924bc05debdc1911361
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62701922"
---
# <a name="add-an--attribute-to-a-dimension"></a>Aggiungere un attributo a una dimensione
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile aggiungere un attributo a una dimensione automaticamente o manualmente.  
  
 Per creare un attributo automaticamente, nella scheda **Struttura dimensione** di Progettazione dimensioni, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selezionare la colonna di cui si vuole eseguire il mapping a un attributo e quindi trascinare tale colonna nel riquadro **Attributi** dal riquadro **Vista origine dati** . Verrà creato un attributo di cui viene eseguito il mapping alla colonna al quale verrà assegnato lo stesso nome della colonna. Se esiste già un attributo con lo stesso nome, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aggiungerà al nome un suffisso composto da un numero ordinale, a partire da "1" per il primo nome duplicato.  
  
 Per creare un attributo manualmente, attivare la visualizzazione griglia nel riquadro **Attributi** . Nella colonna nome dell'ultima riga della griglia, scegliere il  **\<nuovo attributo >** elemento. Digitare un nome per il nuovo attributo. Verrà creato un attributo di cui viene eseguito il mapping a una colonna con le impostazioni predefinite per tutte le proprietà. È possibile impostare il mapping nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] configurando la proprietà **KeyColumns** del nuovo attributo.  
  
 Per altre informazioni, vedere [Definire automaticamente un nuovo attributo](attribute-properties-define-a-new-attribute-automatically.md), [Definire manualmente un nuovo attributo](../define-a-new-attribute-manually.md), [Associare un attributo a una colonna del nome](attribute-properties-bind-an-attribute-to-a-name-column.md)e [Modificare la proprietà KeyColumn di un attributo](attribute-properties-modify-the-keycolumn-property.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributi delle dimensioni](dimension-attribute-properties-reference.md)  
  
  
