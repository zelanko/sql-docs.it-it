---
title: Documentazione per sviluppatori di Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8822a85e39efde36a04b92e8a926adca6839cf58
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578101"
---
# <a name="analysis-services-developer-documentation"></a>Guida per gli sviluppatori (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

In Analysis Services, quasi tutti gli oggetti e il carico di lavoro è programmabile, e spesso è più approcci tra cui scegliere.  Le opzioni includono scrittura di codice gestito, script o tramite standard aperti come XMLA e MSOLAP se i requisiti della soluzione precludono utilizzando .NET framework.

## <a name="what-you-can-accomplish-in-code"></a>Ciò che è possibile eseguire nel codice
Gli scenari di programmazione tipici includono server e la distribuzione del database, amministrazione, modello e la creazione del database e l'accesso ai dati dai report che utilizzano i dati di Analysis Services e applicazioni personalizzate. Comune a tutti questi scenari è una fisso architettura e l'oggetto definizione gerarchia, con operazioni ben note che si estendono su definizione dei dati, elaborazione e i carichi di lavoro di query.

Anche se gli oggetti e i carichi di lavoro sono programmabili, non sono estendibili. In particolare, è possibile creare le cartridge di dati personalizzate che recuperano dati da origini dati non supportato, personalizzano o sostituire i comportamenti di motore di formula o archiviazione, né è possibile creare nuovi tipi di metadati degli oggetti in un server, database o del modello.

Per approfondire ulteriormente l'ultimo punto sulla creazione di nuovi tipi di oggetto: mentre è possibile creare un nuovo tipo di oggetto, è possibile creare oggetti calcolati da espressioni o codice compilati in fase di esecuzione. Non tutti gli elementi nel modello deve essere predefinite ed eseguito il mapping a una struttura di dati esistente. Inoltre, è possibile estendere lo schema tramite le annotazioni in AMO per passare informazioni specifiche dell'oggetto all'applicazione client.

## <a name="choose-a-platform-or-approach-to-development"></a>Scegliere una piattaforma o un approccio allo sviluppo
Analysis Services offre molti modi per personalizzare una soluzione tramite codice, ma la maggior parte degli sviluppatori di usano l'API gestita o lo script.

- Includono le API gestite [TOM e AMO](http://msdn.microsoft.com/library/mt436122.aspx) per la definizione dei dati e le attività amministrative, e [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) per supportare le query dal codice client. In SQL Server 2016, AMO viene aggiornato per usare i nuovi metadati tabulari per i modelli creati o aggiornati a livello di compatibilità 1200 o superiore.

- Script spesso possibile ottenere gli stessi risultati di un programma eseguibile, con eventualmente meno lavoro.

  - È possibile scrivere script di PowerShell usando i componenti di PowerShell per Analysis Services che chiamano direttamente i tipi AMO. All'interno di PowerShell, è anche possibile creare ed eseguire ASSL/XMLA o script TMSL (in JSON).

  - ASSL e TMSL sono linguaggi di script che forniscono gli oggetti utilizzati nell'individuano ed eseguire operazioni. Quale tipo di script usare dipende dal server, database o del modello sottostante.

  - I modelli tabulari o database a livello di compatibilità 1200 e versioni successiva utilizzano il TMSL Tabular Model Scripting Language (), che è in formato JSON.

  - I modelli multidimensionali e modelli tabulari con livelli di compatibilità: 1050-1103 usano Analysis Services Scripting Language (ASSL), che corrisponde all'estensione di Analysis Services dello standard aperto XMLA.

  - È possibile generare uno script ASSL o TMSL in Management Studio. È anche possibile usare **Visualizza codice** in SQL Server Data Tools per visualizzare la definizione del modello in ASSL o TMSL.

- Sebbene sia possibile compilare una soluzione basata sugli standard aperto XMLA e MDX, è piuttosto raro per eseguire questa operazione. Non è prevista la documentazione diverso da XMLA e riferimento MDX consentono all'utente e la maggior parte delle community e forum di supporto disegna dalle esperienze con .NET o tecnologie (MSOLAP) native.

## <a name="programming-in-analysis-services"></a>Programmazione in Analysis Services
[Programmazione di Data Mining](../analysis-services/data-mining-programming.md) vengono descritti gli approcci la creazione di soluzioni che includono oggetti di data mining.

[Programmazione dei modelli multidimensionali](../analysis-services/multidimensional-models/multidimensional-model-programming.md) vengono descritte le attività di sviluppo e approcci per l'integrazione di oggetti del modello multidimensionale in una soluzione personalizzata.

[Programmazione dei modelli tabulari 1200 a livello di compatibilità e versioni successive](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**novità di SQL Server 2016**.  Vengono riepilogate le interfacce e i linguaggi di script utilizzati per lavorare con modelli superiore e tabulari 1200 a livello di codice.

[Programmazione dei modelli tabulari per livello di compatibilità 1050 al livello 1103](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) questa documentazione è destinata agli sviluppatori che supportano i modelli tabulari con livelli di compatibilità precedenti. Descrive le estensioni CSDL che definiscono un modello tabulare nella sintassi XML. Contiene inoltre informazioni sulla sintassi e le definizioni di modello tabulare di oggetto.

[Analysis Services Management Objects (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) documentazione di riferimento per gli sviluppatori per il provider gestito, Analysis Services Management Objects (AMO), per definizione dei dati e l'amministrazione, tra cui l'elaborazione.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) documentazione di riferimento per gli sviluppatori per il provider gestito, ADOMD.NET, usato per i dati a livello di codice i carichi di lavoro di query e l'accesso.

[Set di righe dello Schema di Analysis Services](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets) descrive i set di righe dello schema che forniscono informazioni sullo stato di server, le operazioni server e gli oggetti di database.

[XML for Analysis &#40;XMLA&#41; riferimento](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference) concetti XMLA descrive utili per comprendere il contributo di XMLA alla soluzione personalizzata. Viene inoltre descritto il livello di conformità con la specifica XMLA 1.1.

[Analysis Services Scripting Language &#40;ASSL per XMLA&#41; ](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) vengono descritte le estensioni ASSL a XMLA. ASSL fornisce i linguaggi DDL e DML per i modelli tabulari di Analysis Services che integrano la specifica XMLA.

[Tabular Model Scripting Language &#40;TMSL&#41; riferimento](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) TMSL è una rappresentazione JSON di modelli tabulari a livello di compatibilità 1200 o superiore. Le definizioni degli oggetti sono basati su costrutti di metadati tabulari come tabelle, una colonna e relazione invece i metadati multidimensionali che potrebbero essere poco note, se si ha familiarità con la modellazione di dati di Analysis Services in modalità tabulare.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) documenta i cmdlet utilizzati per le funzioni amministrative e di uso generico **Invoke-ASCmd** cmdlet che accetta qualsiasi script o una query come input.

## <a name="see-also"></a>Vedere anche
[Riferimento tecnico](../analysis-services/powershell/technical-reference-ssas.md)
[riferimenti al linguaggio di espressioni e Query &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/gg492188.aspx)
