---
title: Impostare formule personalizzate membro per gli attributi in una dimensione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29b4d83956e6963aa7df0b4a1afd11edda6c83c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179103"
---
# <a name="bi-wizard---custom-member-formulas-for-attributes-in-a-dimension"></a>Procedura guidata per BI - Impostare formule personalizzate membro per gli attributi in una dimensione
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'aggiunta della funzionalità avanzata delle formule personalizzate membro a un cubo o a una dimensione consente di sostituire la funzione di aggregazione predefinita associata a un membro della dimensione con i risultati di un'espressione MDX (Multidimensional Expressions). Questa funzionalità avanzata imposta la proprietà **CustomRollupColumn** di un attributo specifico in una dimensione.  
  
> [!NOTE]  
>  Una formula personalizzata membro è disponibile solo per le dimensioni basate su origini dei dati esistenti. Per le dimensioni create senza l'utilizzo di un'origine dei dati è necessario eseguire Generazione guidata schema per creare una vista origine dati prima di aggiungere una formula personalizzata membro.  
  
 Per aggiungere una formula personalizzata membro, usare Configurazione guidata funzionalità di Business Intelligence e selezionare l'opzione **Creazione formula personalizzata membro** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi relativi alla selezione di una dimensione alla quale si desidera applicare una formula personalizzata membro e all'abilitazione della formula personalizzata membro specifica.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina **Creazione formula personalizzata membro** della procedura guidata specificare la dimensione alla quale applicare una formula personalizzata membro. L'aggiunta della funzionalità avanzata della formula personalizzata membro alla dimensione selezionata implica modifiche alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="enabling-a-custom-member-formula"></a>Abilitazione di una formula personalizzata membro  
 Nella seconda pagina **Creazione formula personalizzata membro** associare la colonna di origine contenente la formula personalizzata membro a uno o più attributi nella dimensione. Nella colonna **Attributo** selezionare la casella di controllo accanto all'attributo da associare alla colonna della formula personalizzata membro. Dopo aver selezionato ogni attributo, viene visualizzata la finestra di dialogo **Seleziona colonna** . In questa finestra di dialogo fare clic nella colonna della tabella della dimensione contenente la formula. Se dopo aver chiuso la finestra di dialogo **Seleziona colonna** si desidera modificare una selezione, fare clic nella cella **Colonna di origine** da modificare e quindi sui puntini di sospensione ( **...** ) per visualizzare nuovamente la finestra di dialogo **Seleziona colonna** .  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la Configurazione guidata funzionalità di Business Intelligence per migliorare le dimensioni](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
  
  
