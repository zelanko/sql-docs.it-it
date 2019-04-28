---
title: Eliminare una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deleting data source views
- data source views [Analysis Services], deleting
- removing data source views
ms.assetid: ae3f5ca0-ecbf-4b52-8386-eb457719d854
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3869a18e8b19062a0bc6eabfcf45b53d4220dab0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726321"
---
# <a name="delete-a-data-source-view-analysis-services"></a>Eliminare una vista origine dati (Analysis Services)
  Se non si usa più una vista origine dati in un progetto OLAP, è possibile eliminarla dal progetto in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 L'eliminazione di una vista origine dati è permanente. Non è possibile ripristinare una vista origine dati eliminata in un progetto o database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Non è possibile eliminare viste origine dati da cui dipendono altri oggetti da un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aperto da [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] in modalità online. Per eliminare una vista origine dati da un progetto connesso o da un database in esecuzione in un server, è necessario eliminare innanzitutto tutti gli oggetti nel database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che dipendono da tale vista prima di eliminare la vista origine dati stessa.  
  
 Se si elimina una vista origina dati, gli altri oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da cui dipendono non saranno validi pertanto, prima di eliminare la vista origine dati, si esaminerà l'elenco di oggetti che diventeranno non validi una volta rimossa tale vista. Esaminare con attenzione l'elenco per assicurarsi che non siano inclusi oggetti che si prevede di utilizzare ancora.  
  
 ![Dialogo Elimina oggetti](../media/ssas-olapdsv-deleteobjects.gif "nella finestra di dialogo Elimina oggetti")  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)   
 [Modificare le proprietà in una vista origine dati &#40;Analysis Services&#41;](change-properties-in-a-data-source-view-analysis-services.md)  
  
  
