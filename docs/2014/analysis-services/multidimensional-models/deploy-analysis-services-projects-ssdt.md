---
title: Distribuire progetti Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5317eea19d088a8d3f9d8bfb86da4e0429d62c3e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546853"
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Distribuire progetti di Analysis Services (SSDT)
  Durante lo sviluppo di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], si distribuisce frequentemente il progetto su un server di sviluppo per creare il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definito dal progetto. Ciò è necessario per testare il progetto, ad esempio per esplorare le celle nel cubo o i membri della dimensione oppure per verificare le formule per gli indicatori di prestazioni chiave (KPI).  
  
## <a name="deploying-a-project"></a>Distribuzione di un progetto  
 È possibile distribuire un progetto in modo indipendente oppure distribuire tutti i progetti all'interno della soluzione. Quando si distribuisce un progetto, vengono eseguite diverse operazioni in sequenza. Viene innanzitutto compilato il progetto. In questo passaggio vengono creati i file di output che definiscono il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e gli oggetti da cui è costituito. Viene quindi convalidato il server di destinazione e infine vengono creati il database di destinazione e i relativi oggetti sul server di destinazione. Durante la distribuzione, qualsiasi database preesistente viene completamente sostituito dal motore di distribuzione con il contenuto del progetto, a meno che gli oggetti non siano stati creati dal progetto durante una distribuzione precedente.  
  
 Dopo una distribuzione iniziale, nella cartella \obj viene generato un file di IncrementalSnapshot.xml \<Project Name> . Tale file consente di determinare se il database o gli oggetti sul server di destinazione sono stati modificati all'esterno del progetto. In tal caso, verrà richiesto di sovrascrivere tutti gli oggetti nel database di destinazione. Se tutte le modifiche sono state apportate all'interno del progetto e il progetto è configurato per la distribuzione incrementale, sul server di destinazione verranno distribuite soltanto le modifiche.  
  
 La configurazione di progetto e le impostazioni associate determinano le proprietà di distribuzione che verranno utilizzate per distribuire il progetto. Per un progetto condiviso, ogni sviluppatore può utilizzare la propria configurazione con specifiche opzioni di configurazione del progetto. Ogni sviluppatore può ad esempio specificare un diverso server di prova per mantenere l'isolamento rispetto agli altri sviluppatori.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un progetto di Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
  
