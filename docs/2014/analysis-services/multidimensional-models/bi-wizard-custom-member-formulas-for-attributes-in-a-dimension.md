---
title: Impostare formule personalizzate membro per gli attributi in una dimensione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], custom member formulas
- member formulas [Analysis Services]
- dimensions [Analysis Services], Business Intelligence enhancements
- custom member formulas [Analysis Services]
- CustomRollupColumn property
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8850ce0f77b69be681bf99bcdcaeddc5234656c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700994"
---
# <a name="set-custom-member-formulas-for-attributes-in-a-dimension"></a>Impostare formule personalizzate membro per gli attributi in una dimensione
  L'aggiunta della funzionalità avanzata delle formule personalizzate membro a un cubo o a una dimensione consente di sostituire la funzione di aggregazione predefinita associata a un membro della dimensione con i risultati di un'espressione MDX (Multidimensional Expressions). Questa funzionalità avanzata imposta la proprietà `CustomRollupColumn` di un attributo specifico in una dimensione.  
  
> [!NOTE]  
>  Una formula personalizzata membro è disponibile solo per le dimensioni basate su origini dei dati esistenti. Per le dimensioni create senza l'utilizzo di un'origine dei dati è necessario eseguire Generazione guidata schema per creare una vista origine dati prima di aggiungere una formula personalizzata membro.  
  
 Per aggiungere una formula personalizzata membro, usare Configurazione guidata funzionalità di Business Intelligence e selezionare l'opzione **Creazione formula personalizzata membro** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi relativi alla selezione di una dimensione alla quale si desidera applicare una formula personalizzata membro e all'abilitazione della formula personalizzata membro specifica.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Creazione formula personalizzata membro** della procedura guidata specificare la dimensione alla quale applicare una formula personalizzata membro. L'aggiunta della funzionalità avanzata della formula personalizzata membro alla dimensione selezionata implica modifiche alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="enabling-a-custom-member-formula"></a>Abilitazione di una formula personalizzata membro  
 Nella seconda pagina **Creazione formula personalizzata membro** associare la colonna di origine contenente la formula personalizzata membro a uno o più attributi nella dimensione. Nella colonna **Attributo** selezionare la casella di controllo accanto all'attributo da associare alla colonna della formula personalizzata membro. Dopo aver selezionato ogni attributo, viene visualizzata la finestra di dialogo **Seleziona colonna** . In questa finestra di dialogo fare clic nella colonna della tabella della dimensione contenente la formula. Se dopo aver chiuso la finestra di dialogo **Seleziona colonna** si desidera modificare una selezione, fare clic nella cella **Colonna di origine** da modificare e quindi sui puntini di sospensione (**...**) per visualizzare nuovamente la finestra di dialogo **Seleziona colonna** .  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la Configurazione guidata funzionalità di Business Intelligence per migliorare le dimensioni](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
  
  
