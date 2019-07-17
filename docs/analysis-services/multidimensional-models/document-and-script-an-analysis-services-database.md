---
title: Documentazione e Script per un Database di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2fa4d5df2af04402ae8dc40c81ec75a72f7d8671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208910"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentazione e script per un database di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dopo la distribuzione di un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per generare l'output dei metadati del database o di un oggetto contenuto nel database in formato di script XMLA (XML for Analysis). È possibile salvare l'output di questo script in una nuova finestra dell'**Editor di query XMLA**, in un file o negli Appunti. Per altre informazioni su XMLA, vedere [Guida di riferimento ad Analysis Services Scripting Language &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
 Lo script XMLA generato utilizza gli elementi ASSL ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) per definire gli oggetti contenuti nello script. Se è stato generato uno script CREATE, lo script XMLA risultante contiene un comando XMLA **Create** e gli elementi ASSL che consentono di creare l'intera struttura del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un'istanza. Se è stato generato uno script ALTER, lo script XMLA risultante contiene un comando XMLA **Alter** e gli elementi ASSL che consentono di ripristinare lo stato in cui si trovava la struttura di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente al momento della creazione dello script.  
  
 È possibile utilizzare in vari modi lo script XMLA generato da un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ad esempio per gli scopi seguenti:  
  
-   Per mantenere uno script di backup che consente di ricreare tutti gli oggetti e le autorizzazioni di database.  
  
-   Per creare o aggiornare il codice di sviluppo del database.  
  
-   Per creare un ambiente di prova o di sviluppo da uno schema esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare o eliminare un database di Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Elemento Alter &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
