---
title: Dimensione oggetti (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0c64f95b0c366453e1099c80d8e40b217fb7801
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702455"
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Oggetti dimensione (Analysis Services - Dati multidimensionali)
  Un oggetto <xref:Microsoft.AnalysisServices.Dimension> semplice è composto da informazioni di base, attributi e gerarchie. Le informazioni di base includono il nome e il tipo della dimensione, l'origine dati, la modalità di archiviazione e altro. Gli attributi definiscono i dati effettivi nella dimensione. Sebbene gli attributi non appartengano necessariamente a una gerarchia, le gerarchie sono compilate dagli attributi. Una gerarchia crea elenchi ordinati di livelli e definisce le modalità di esplorazione della dimensione da parte di un utente.  
  
## <a name="in-this-section"></a>In questa sezione  
 Negli argomenti seguenti vengono fornite ulteriori informazioni sulla progettazione e sull'implementazione degli oggetti dimensione.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](dimensions-analysis-services-multidimensional-data.md)|Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], le dimensioni sono un componente essenziale dei cubi. Le dimensioni consentono di organizzare i dati in relazione a un'area di interesse per gli utenti, ad esempio relativa a clienti, archivi o dipendenti.|  
|[Attributi e gerarchie di attributi](attributes-and-attribute-hierarchies.md)|Le dimensioni sono raccolte di attributi, associate a una o più colonne in una tabella o una vista della vista origine dati.|  
|[Relazioni tra attributi](attribute-relationships.md)|Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], gli attributi all'interno di una dimensione sono sempre correlati direttamente o indirettamente all'attributo chiave. Quando si definisce una dimensione in base a uno schema star, in cui tutti gli attributi della dimensione sono derivati dalla stessa tabella relazionale, viene automaticamente definita una relazione tra l'attributo chiave e ogni attributo non chiave della dimensione. Quando si definisce una dimensione in base a uno schema snowflake, in cui gli attributi della dimensione sono derivati da più tabelle correlate, viene automaticamente definita una relazione tra attributi come indicato di seguito:<br /><br /> -Tra l'attributo chiave e ogni non chiave attributi associati alle colonne nella tabella della dimensione principale.<br />-Tra l'attributo chiave e l'attributo associato alla chiave esterna della tabella secondaria che collega le tabelle delle dimensioni sottostante.<br />-Tra l'attributo associato alla chiave esterna della tabella secondaria e ogni attributo non chiave associato alle colonne della tabella secondaria.|  
  
  
