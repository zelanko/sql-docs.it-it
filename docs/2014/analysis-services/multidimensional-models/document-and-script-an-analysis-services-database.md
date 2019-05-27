---
title: Documentazione e Script per un Database di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9284073781a91b21d588684b9071e6179a815613
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075121"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentazione e script per un database di Analysis Services
  Dopo la distribuzione di un database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per generare l'output dei metadati del database o di un oggetto contenuto nel database in formato di script XMLA (XML for Analysis). È possibile salvare l'output di questo script in una nuova finestra dell' **Editor di query XMLA** , in un file o negli Appunti. Per altre informazioni su XMLA, vedere [Analysis Services Scripting Language &#40;ASSL&#41; riferimento](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
 Lo script XMLA generato utilizza gli elementi ASSL ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language) per definire gli oggetti contenuti nello script. Se è stato generato uno script CREATE, lo script XMLA risultante contiene un comando XMLA **Create** e gli elementi ASSL che consentono di creare l'intera struttura del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un'istanza. Se è stato generato uno script ALTER, lo script XMLA risultante contiene un comando XMLA **Alter** e gli elementi ASSL che consentono di ripristinare lo stato in cui si trovava la struttura di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente al momento della creazione dello script.  
  
 È possibile utilizzare in vari modi lo script XMLA generato da un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ad esempio per gli scopi seguenti:  
  
-   Per mantenere uno script di backup che consente di ricreare tutti gli oggetti e le autorizzazioni di database.  
  
-   Per creare o aggiornare il codice di sviluppo del database.  
  
-   Per creare un ambiente di prova o di sviluppo da uno schema esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare o eliminare un database di Analysis Services](modify-or-delete-an-analysis-services-database.md)   
 [Elemento Alter &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
