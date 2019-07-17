---
title: Estensione di OLAP tramite personalizzazioni | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c49d2d350504daef36d0fbe861b26ccf220e7a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208887"
---
# <a name="extending-olap-through-personalizations"></a>Estensione di OLAP tramite personalizzazioni
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services fornisce diverse funzioni intrinseche da utilizzare con i linguaggi MDX (Multidimensional Expressions) e Data Mining Extensions (DMX). Queste funzioni sono progettate per consentire l'esecuzione di qualsiasi operazione, dai calcoli statistici standard all'attraversamento dei membri di una gerarchia. Come avviene per qualsiasi altro prodotto complesso e affidabile, tuttavia, si è avvertita l'esigenza di estendere ulteriormente le funzionalità di questo servizio.  
  
 A tale scopo, Analysis Services offre la possibilità di aggiungere assembly ed estensioni personalizzate a un'istanza del servizio, per soddisfare le diverse esigenze aziendali ogni volta che le funzionalità standard si rivelano insufficienti.  
  
## <a name="assemblies"></a>Assembly  
 Gli assembly consentono di estendere la funzionalità business dei linguaggi MDX e DMX. È necessario compilare la funzionalità desiderata in una libreria, ad esempio in una libreria a collegamento dinamico (DLL), quindi aggiungere tale libreria come assembly a un'istanza o a un database di Analysis Services. I metodi pubblici della libreria vengono quindi esposti come funzioni definite dall'utente in espressioni MDX e DMX, procedure, calcoli, azioni e applicazioni client.  
  
## <a name="personalized-extensions"></a>Estensioni personalizzate  
 Le estensioni della personalizzazione di SQL Server Analysis Services rappresentano la struttura di base dell'implementazione di un'architettura plug-in. Le estensioni della personalizzazione di Analysis Services rappresentano una semplice ed elegante modifica all'architettura dell'assembly gestito esistente e vengono esposte nel modello a oggetti <xref:Microsoft.AnalysisServices.AdomdServer> di Analysis Services, nella sintassi MDX e nei set di righe degli schemi.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Analysis Services Personalization Extensions](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  
