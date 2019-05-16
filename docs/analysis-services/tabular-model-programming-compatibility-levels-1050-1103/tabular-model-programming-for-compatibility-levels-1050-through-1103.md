---
title: 'Analysis Services in modalità tabulare programmazione del modello per i livelli di compatibilità: 1050-1103 | Microsoft Docs'
ms.date: 05/14/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ddc25ab4d4358c8000c5a7bfe9a9de9dd5e87ed6
ms.sourcegitcommit: 4cb96c291529e9bdf0a95fb3610b350583eb36d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65709146"
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>Programmazione di modelli tabulari per i livelli di compatibilità da 1050 a 1103
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  I modelli tabulari utilizzano costrutti relazionali per modellare i dati di Analysis Services utilizzati dalle applicazioni analitiche e di report. Questi modelli vengono eseguiti in un'istanza di Analysis Services configurata per la modalità tabulare, utilizzando un motore di analisi in memoria per l'archiviazione in memoria e rapide scansioni di tabella in grado di aggregare e calcolare i dati in base alle esigenze.  
  
 Se i requisiti della soluzione BI personalizzata vengono meglio soddisfatti da un database modello tabulare, è possibile utilizzare qualsiasi libreria client di Analysis Services e interfaccia di programmazione per integrare l'applicazione con i modelli tabulari in un'istanza di Analysis Services. Per eseguire query e calcoli sui dati del modello tabulare, è possibile utilizzare il linguaggio MDX o DAX incorporato nel codice.  
  
 Per i modelli tabulari creati in versioni precedenti di Analysis Services, in particolari modelli con livelli di compatibilità 1050 a 1103, gli oggetti a cui si lavora a livello di codice in AMO, ADOMD.NET, XMLA o OLE DB sono fondamentalmente lo stesso per entrambi in formato tabulare e soluzioni multidimensionali. In particolare, i metadati degli oggetti definiti per i modelli multidimensionali viene usato anche per i livelli di compatibilità tabulare 1050-1103.  
  
 A partire da SQL Server 2016, i modelli tabulari possono essere creati o aggiornati a livello di compatibilità 1200 o superiore, che usa metadati tabulari per definire il modello. I metadati e la programmabilità sono fondamentalmente diverse a questo livello. Visualizzare [programmazione dei modelli tabulari 1200 a livello di compatibilità e versioni successive](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) e [aggiornare Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) per altre informazioni.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Annotazioni CSDL per Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
 [Comprendere il modello a oggetti tabulare alla compatibilità livelli 1050 a 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [Riferimento tecnico per le annotazioni di Business Intelligence per CSDL](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl)  
  

[Interfaccia IMDEmbeddedData](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
