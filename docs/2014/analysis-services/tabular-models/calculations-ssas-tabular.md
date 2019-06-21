---
title: Calcoli (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9412d01809402dfa23c116c93c80e0ab32bee747
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284913"
---
# <a name="calculations-ssas-tabular"></a>Calcoli (SSAS tabulare)
  Dopo aver importato dati nel modello, è possibile aggiungere calcoli per aggregare, filtrare, estendere, combinare e proteggere tali dati. Nei modelli tabulari viene utilizzato DAX (Data Analysis Expressions), un linguaggio delle formule per la creazione di calcoli personalizzati. In un modello tabulare, i calcoli che vengono creati tramite formule DAX vengono usati in *Colonne calcolate*, *Misure*e *Filtri di riga*.  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Informazioni su DAX nei modelli tabulari &#40;SSAS tabulare&#41;](understanding-dax-in-tabular-models-ssas-tabular.md)|Viene descritto il linguaggio delle formule Data Analysis Expressions (DAX) utilizzato per creare calcoli per colonne calcolate, misure e filtri di riga nei modelli tabulari.|  
|[Compatibilità delle formule nella modalità DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Vengono descritte le differenze e vengono elencate le funzioni non supportate nella modalità DirectQuery e quelle supportate, ma che potrebbero restituire risultati diversi.|  
|[Data Analysis Expressions &#40;DAX&#41; riferimento](/dax/data-analysis-expressions-dax-reference)|In questa sezione vengono fornite descrizioni dettagliate della sintassi, degli operatori e delle funzioni DAX.|  
  
> [!NOTE]  
>  In questa sezione non vengono fornite attività dettagliate per la creazione dei calcoli. Poiché i calcoli vengono specificati in colonne calcolate, misure e filtri di riga (nei ruoli), le istruzioni sulla posizione in cui creare formule DAX vengono fornite nelle attività correlate a tali funzionalità. Per altre informazioni, vedere [Creare una colonna calcolata &#40;SSAS tabulare&#41;](ssas-calculated-columns-create-a-calculated-column.md), [Creare e gestire misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md), e [Creare e gestire ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Mentre DAX può essere utilizzato anche per eseguire query su un modello tabulare, gli argomenti in questa sezione riguardano in particolare l'utilizzo di formule DAX per creare calcoli.  
  
  
