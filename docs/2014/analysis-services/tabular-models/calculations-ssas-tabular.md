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
ms.openlocfilehash: 2da86ae5c5652c8b2614cae4bbb721802700d973
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939902"
---
# <a name="calculations-ssas-tabular"></a>Calcoli (SSAS tabulare)
  Dopo aver importato dati nel modello, è possibile aggiungere calcoli per aggregare, filtrare, estendere, combinare e proteggere tali dati. Nei modelli tabulari viene utilizzato DAX (Data Analysis Expressions), un linguaggio delle formule per la creazione di calcoli personalizzati. In un modello tabulare, i calcoli che vengono creati tramite formule DAX vengono usati in *Colonne calcolate*, *Misure*e *Filtri di riga*.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Informazioni su DAX nei modelli tabulari &#40;SSAS tabulare&#41;](understanding-dax-in-tabular-models-ssas-tabular.md)|Viene descritto il linguaggio delle formule Data Analysis Expressions (DAX) utilizzato per creare calcoli per colonne calcolate, misure e filtri di riga nei modelli tabulari.|  
|[Compatibilità delle formule nella modalità DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Vengono descritte le differenze e vengono elencate le funzioni non supportate nella modalità DirectQuery e quelle supportate, ma che potrebbero restituire risultati diversi.|  
|[Informazioni di riferimento sulle espressioni di analisi dei dati &#40;&#41; DAX](/dax/data-analysis-expressions-dax-reference)|In questa sezione vengono fornite descrizioni dettagliate della sintassi, degli operatori e delle funzioni DAX.|  
  
> [!NOTE]  
>  In questa sezione non vengono fornite attività dettagliate per la creazione dei calcoli. Poiché i calcoli vengono specificati in colonne calcolate, misure e filtri di riga (nei ruoli), le istruzioni sulla posizione in cui creare formule DAX vengono fornite nelle attività correlate a tali funzionalità. Per altre informazioni, vedere [Creare una colonna calcolata &#40;SSAS tabulare&#41;](ssas-calculated-columns-create-a-calculated-column.md), [Creare e gestire misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md), e [Creare e gestire ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Mentre DAX può essere utilizzato anche per eseguire query su un modello tabulare, gli argomenti in questa sezione riguardano in particolare l'utilizzo di formule DAX per creare calcoli.  
  
  
