---
title: Aggiungere un'aggregazione personalizzata a una dimensione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], custom aggregations
- aggregations [Analysis Services], custom
- unary operators
- custom aggregations [Analysis Services]
ms.assetid: 3199a6c2-a06d-47b9-bd1c-604dbb085318
author: minewiskan
ms.author: owend
ms.openlocfilehash: ed843b8b0005ff62f05b13ebd20024d528857388
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544607"
---
# <a name="add-a-custom-aggregation-to-a-dimension"></a>Aggiungere un'aggregazione personalizzata a una dimensione
  È possibile aggiungere una funzionalità avanzata di aggregazione personalizzata a un cubo o una dimensione per sostituire le aggregazioni predefinite associate a un membro di una dimensione con un operatore unario diverso. Questa funzionalità consente di specificare nella tabella della dimensione una colonna dell'operatore unario che definisce il rollup per i membri di una gerarchia padre-figlio. L'operatore unario funge da attributo padre nella gerarchia padre-figlio.  
  
> [!NOTE]  
>  Un'aggregazione personalizzata è disponibile solo per le dimensioni basate su origini dei dati esistenti. Per le dimensioni create senza utilizzare un'origine dei dati, prima di aggiungere l'aggregazione personalizzata è necessario eseguire la Generazione guidata schema per creare una vista origine dati.  
  
 Per aggiungere un'aggregazione personalizzata, usare la Configurazione guidata funzionalità di Business Intelligence e selezionare l'opzione **Impostazione operatore unario** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi necessari per selezionare una dimensione a cui si desidera applicare un'aggregazione personalizzata e identificare l'aggregazione personalizzata.  
  
> [!NOTE]  
>  Prima di eseguire la Configurazione guidata funzionalità di Business Intelligence per aggiungere un'aggregazione personalizzata, verificare che la dimensione a cui deve essere applicata la funzionalità avanzata contenga una gerarchia dell'attributo padre-figlio. Per ulteriori informazioni, vedere [gerarchia padre-figlio](parent-child-dimension.md).  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina di **Impostazione operatore unario** della procedura guidata specificare la dimensione a cui si vuole applicare un'aggregazione personalizzata. L'aggiunta dell'aggregazione personalizzata alla dimensione selezionata comporterà modifiche della dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="adding-custom-aggregation-unary-operator"></a>Aggiunta di un'aggregazione personalizzata (operatore unario)  
 Nella seconda pagina di **Impostazione operatore unario** specificare l'attributo padre desiderato per l'aggregazione personalizzata e la colonna di origine nella tabella della dimensione per l'operatore unario. **Attributo padre** elenca gli attributi la cui `Usage` proprietà è impostata su `Parent` . Se gli attributi padre sono più di uno, scegliere quello corrispondente alla relazione padre-figlio che si desidera utilizzare. Se non è indicato alcun attributo padre, significa che la dimensione non include una gerarchia padre-figlio valida.  
  
 In **Colonna di origine**selezionare la colonna stringa che contiene gli operatori unari. Questa selezione imposta la `UnaryOperatorColumn` proprietà sull'attributo padre. La tabella della dimensione deve inoltre contenere una colonna stringa che specifica l'operatore di rollup unario. I valori stringa di questa colonna devono contenere operatori di aggregazione validi. Se una riga è vuota, il membro corrispondente viene calcolato normalmente. Se la formula in una colonna non è valida, si verifica un errore di run-time ogni volta che viene recuperato il valore di una cella che utilizza il membro. Per altre informazioni, vedere [Operatori unari nelle dimensioni padre-figlio](parent-child-dimension-attributes-unary-operators.md).  
  
  
