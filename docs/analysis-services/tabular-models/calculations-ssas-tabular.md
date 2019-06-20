---
title: Calcoli nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7096cac1f4721531f1905b11f2ca3b901661204
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263433"
---
# <a name="calculations-in-tabular-models"></a>Calcoli nei modelli tabulari
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Dopo aver importato dati nel modello, è possibile aggiungere calcoli per aggregare, filtrare, estendere, combinare e proteggere tali dati. Nei modelli tabulari viene utilizzato DAX (Data Analysis Expressions), un linguaggio delle formule per la creazione di calcoli personalizzati. In un modello tabulare, i calcoli che vengono creati tramite formule DAX vengono usati in *Colonne calcolate*, *Misure*e *Filtri di riga*.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Informazioni su DAX nei modelli tabulari](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Viene descritto il linguaggio delle formule Data Analysis Expressions (DAX) utilizzato per creare calcoli per colonne calcolate, misure e filtri di riga nei modelli tabulari.|  
|[Compatibilità delle formule DAX in modalità DirectQuery](http://msdn.microsoft.com/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Vengono descritte le differenze e vengono elencate le funzioni non supportate nella modalità DirectQuery e quelle supportate, ma che potrebbero restituire risultati diversi.|  
|[Riferimento a Data Analysis Expressions (DAX)](/dax/data-analysis-expressions-dax-reference)|In questa sezione vengono fornite descrizioni dettagliate della sintassi, degli operatori e delle funzioni DAX.|  
  
> [!NOTE]  
>  In questa sezione non vengono fornite attività dettagliate per la creazione dei calcoli. Poiché i calcoli vengono specificati in colonne calcolate, misure e filtri di riga (nei ruoli), le istruzioni sulla posizione in cui creare formule DAX vengono fornite nelle attività correlate a tali funzionalità. Per altre informazioni, vedere [crea una colonna calcolata](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [creare e gestire misure](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md), e [crea e Gestisci ruoli](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Mentre DAX può essere utilizzato anche per eseguire query su un modello tabulare, gli argomenti in questa sezione riguardano in particolare l'utilizzo di formule DAX per creare calcoli.  
  
  
