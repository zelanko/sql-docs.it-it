---
title: Calcoli | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 871d248eec557033c181bbd3d162cd17875dd30c
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158308"
---
# <a name="calculations"></a>Calcoli
  Un calcolo è un'espressione MDX (Multidimensional Expressions) o uno script che viene usato per definire un membro calcolato, un set denominato o un'assegnazione di ambito in un cubo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. I calcoli consentono di aggiungere oggetti definiti non dai dati del cubo, ma da espressioni che possono fare riferimento ad altre parti del cubo, ad altri cubi o persino a informazioni esterne al database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. I calcoli consentono di estendere le funzionalità di un cubo, aggiungendo flessibilità e potenza alle applicazioni di Business Intelligence. Per altre informazioni sui calcoli di scripting, vedere [Introduzione alla creazione di script MDX in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892). Per altre informazioni sui problemi di prestazioni correlati a query e calcoli MDX, vedere la [SQL Server 2005 Analysis Services Performance Guide](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="calculated-members"></a>Membri calcolati  
 Un membro calcolato è un membro il cui valore viene calcolato in fase di esecuzione utilizzando un'espressione MDX (Multidimensional Expressions) specificata dall'utente durante la definizione del membro stesso. Un membro calcolato è disponibile per le applicazioni di Business Intelligence come qualsiasi altro membro. I membri calcolati non aumentano le dimensioni del cubo dato che solo le definizioni vengono archiviate nel cubo, mentre il calcolo dei valori, necessario per rispondere alle query, viene eseguito in memoria.  
  
 È possibile definire membri calcolati per qualsiasi dimensione, inclusa la dimensione delle misure. I membri calcolati creati per la dimensione Measures vengono denominati "misure calcolate".  
  
 Sebbene i membri calcolati siano generalmente basati su dati già esistenti nel cubo, è possibile creare espressioni complesse combinando questi dati con operatori aritmetici, numeri e funzioni. È possibile utilizzare anche funzioni MDX, ad esempio LookupCube per accedere in altri cubi nel database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include librerie di funzione Visual Studio standardizzate ed è possibile utilizzare stored procedure per recuperare dati da origini diverse dal database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] corrente. Per altre informazioni sulle stored procedure, vedere [definizione di Stored procedure](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md).  
  
 Si supponga, ad esempio, che i dirigenti di una società di spedizioni desiderino determinare i tipi di merci più vantaggiosi da trasportare in base al profitto per unità di volume. A tale scopo, utilizzano un cubo Shipments contenente le dimensioni Cargo, Fleet e Time e le misure Price_to_Ship, Cost_to_Ship e Volume_in_Cubic_Meters. Il cubo, tuttavia, non contiene una misura per la redditività. In tal caso, è possibile creare nel cubo un membro calcolato come misura denominata Profit_per_Cubic_Meter combinando le misure esistenti nell'espressione seguente:  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 Dopo aver creato il membro calcolato, la misura Profit_per_Cubic_Meter verrà visualizzata insieme alle altre alla successiva esplorazione del cubo Shipments.  
  
 Per creare membri calcolati, usare il **calcolo**scheda in Progettazione cubi. Per altre informazioni, vedere [creare membri calcolati](../multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>Set denominati  
 Un set denominato è un'istruzione CREATE SET MDX che restituisce un set. L'espressione MDX viene salvata come parte della definizione di un cubo in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Un set denominato viene creato per il riutilizzo in query MDX e consente agli utenti aziendali di semplificare le query e utilizzare un nome di set anziché un'espressione set per le espressioni set complesse utilizzate di frequente. **Argomento correlato:** [Creare set denominati](../multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>Comandi script  
 Un comando script è uno script MDX incluso nella definizione del cubo. I comandi script consentono di eseguire quasi tutte le operazioni supportate da MDX in un cubo, ad esempio la definizione dell'ambito di un calcolo da applicare solo a parte del cubo. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], gli script MDX possono essere applicato all'intero cubo o a sezioni specifiche del cubo, in punti specifici durante l'esecuzione dello script. L'istruzione CALCULATE, che è il comando script predefinito, popola le celle del cubo con dati aggregati in base all'ambito predefinito.  
  
 L'ambito predefinito è l'intero cubo, ma è possibile definire un ambito più limitato, noto come sottocubo, e quindi applicare uno script MDX solo a tale area del cubo. L'istruzione SCOPE definisce l'ambito di tutte le successive espressioni e istruzioni MDX nello script di calcolo fino a quando l'ambito non viene terminato o ridefinito. Viene quindi utilizzata l'istruzione THIS per applicare un'espressione MDX all'ambito corrente. È possibile utilizzare l'istruzione BACK_COLOR per applicare alle celle nell'ambito corrente un colore di sfondo che agevoli le operazioni di debug.  
  
 È ad esempio possibile utilizzare un comando script per allocare obiettivi di vendita ai dipendenti, suddivisi per periodo di tempo e territorio di vendita, in base ai valori ponderati delle vendite in un periodo di tempo precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli nei modelli multidimensionali](../multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
