---
title: La comprensione dell'analisi dello Script di distribuzione di servizi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9436d33cdc99cf979509a40f06ceea15c0cd765
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072662"
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Informazioni sullo script di distribuzione di Analysis Services
  Lo script di distribuzione XMLA generato dalla Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include due sezioni:  
  
-   La prima parte dello script di distribuzione contiene i comandi necessari per creare, modificare o eliminare gli oggetti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appropriati nel database di destinazione. Per impostazione predefinita, i file di input generati dal progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono basati su una distribuzione incrementale. Lo script di distribuzione di XMLA avrà pertanto effetto solo sugli oggetti modificati o eliminati.  
  
-   La seconda parte dello script di distribuzione contiene i comandi necessari per elaborare soltanto gli oggetti creati o modificati nel server di destinazione (opzione Elaborazione predefinita) o per elaborare completamente il database di destinazione. Si può inoltre scegliere di non includere alcun comando di elaborazione nello script di distribuzione.  
  
 L'intero script di distribuzione può essere eseguito in una singola transazione o in più transazioni. Se lo script viene eseguito in più transazioni, la prima parte dello script viene eseguita come singola transazione e ogni oggetto viene elaborato nella relativa transazione.  
  
> [!IMPORTANT]  
>  Tramite la Distribuzione guidata [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile distribuire oggetti solo in un singolo database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Non è possibile distribuire alcun oggetto o dato a livello del server.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione della Distribuzione guidata Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Informazioni sui file di input utilizzati per creare uno script di distribuzione](deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
