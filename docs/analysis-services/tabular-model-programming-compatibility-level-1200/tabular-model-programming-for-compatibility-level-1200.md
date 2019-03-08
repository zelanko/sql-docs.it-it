---
title: Analysis Services in modalità tabulare modello di programmazione per il livello di compatibilità 1200 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7493c09964db2e0a8cbd17c6a2278dd554a2dcc
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579451"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Livello di compatibilità di programmazione dei modelli tabulari 1200 e superiori
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Partendo con livello di compatibilità 1200, dei metadati tabulari viene utilizzato per descrivere i costrutti del modello, sostituendo cronologici metadati multidimensionali come descrittori per gli oggetti del modello tabulare. I metadati per le tabelle, colonne e relazioni sono tabelle, colonne e relazione, anziché gli equivalenti multidimensionali (dimensione e attributo).  
  
È possibile creare nuovi modelli a livello di compatibilità 1200 o superiore con APIs Microsoft.AnalysisServices.Tabular, la versione più recente di SQL Server Data Tools (SSDT), oppure modificando la **CompatibilityLevel** di un tabulari esistenti modello per aggiornarlo (eseguita anche in SSDT). Questa operazione associa il modello a versioni più recenti del server, strumenti e interfacce di programmazione.   
  
L'aggiornamento di una soluzione tabulare esistente è consigliata ma non richiesta. Script esistente e soluzioni personalizzate che accedono o gestiscono i modelli tabulari o i database possono essere usate come-è. Livelli di compatibilità precedenti sono completamente supportati in SQL Server 2016 usando le funzionalità disponibili in tale livello. Azure Analysis Services supporta solo il livello di compatibilità 1200 o superiore.
  
 Nuovi modelli tabulari richiederanno diversi codici e script, riepilogate di seguito.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definizioni di modello a oggetti come costrutti di metadati tabulari  
 Il modello a oggetti tabulare per i modelli 1200 o superiori viene esposto in JSON tramite il [Tabular Model Scripting Language](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) e tramite il linguaggio di definizione dati AMO tramite un nuovo spazio dei nomi, [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Script per database e i modelli tabulari  
 TMSL è un linguaggio di scripting di JSON per i modelli tabulari, con supporto per la creazione, lettura, aggiornamento, un operazioni di eliminazione. È possibile aggiornare i dati tramite TMSL e richiamare operazioni del database per il collegamento, dissociare, backup, ripristino e sincronizzazione.  
  
 PowerShell per AMO accetta script TMSL come input.  
  
 Visualizzare [Tabular Model Scripting Language &#40;TMSL&#41; riferimento](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) e [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) per altre informazioni.  
  
## <a name="query-languages"></a>Linguaggi di query  
 DAX e MDX sono supportati per tutti i modelli tabulari.  
  
## <a name="expression-language"></a>Expression Language  
 I filtri e le espressioni usate per creare oggetti calcolati, tra cui le misure e indicatori KPI, vengono formulate in DAX. Visualizzare [capire DAX nei modelli tabulari](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) e [Data Analysis Expressions &#40;DAX&#41; in Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Codice gestito per i modelli tabulari e i database  
 AMO include un nuovo spazio dei nomi, Microsoft.AnalysisServices.Tabular, per l'uso di modelli a livello di codice. Visualizzare [Microsoft. AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) per altre informazioni.  
  
> [!NOTE]  
>  Le librerie client Analysis Services Management Objects (AMO), ADOMD.NET e modello a oggetti tabulare (TOM) è ora destinato al runtime di .NET 4.0.   
  
## <a name="see-also"></a>Vedere anche  
 [Documentazione per gli sviluppatori di Analysis Services](../../analysis-services/analysis-services-developer-documentation.md)   
 [I livelli di programmazione per la compatibilità dei modelli tabulari 1050 a 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Riferimento tecnico](../../analysis-services/powershell/technical-reference-ssas.md)[aggiornare Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Livelli di compatibilità dei database e i modelli tabulari](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
