---
title: Distribuire soluzioni di modelli tramite XMLA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68700aaba6c335bf7fe9686961933eac5c52f8f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075365"
---
# <a name="deploy-model-solutions-using-xmla"></a>Distribuire soluzioni di modelli utilizzando XMLA
  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]l'opzione **Genera codice per istruzione CREATE in** del comando **Crea script per database** consente di creare uno script XML per un intero database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o uno dei relativi oggetti che lo costituiscono. Lo script risultante può quindi essere eseguito in un altro computer per ricreare lo schema (metadati) del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Lo script genera l'intero database e non è disponibile alcun meccanismo per eseguire l'aggiornamento incrementale di oggetti già distribuiti durante l'utilizzo dello script. In seguito all'esecuzione dello script e alla distribuzione del database, il nuovo database creato deve essere elaborato prima che gli utenti possano visualizzarlo.  
  
 Per altre informazioni sul comando **Crea script per database** , vedere [Documentazione e script per un database di Analysis Services](document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Modifica delle proprietà degli oggetti nello script XML  
 Quando si usa il comando **Crea script per database** , non è possibile modificare proprietà specifiche, ad esempio il nome del database, le stringhe di connessione dell'origine dei dati e le impostazioni di sicurezza, degli oggetti del database. Tali proprietà devono essere modificate manualmente nello script in seguito alla generazione dello script oppure nel database distribuito in seguito all'esecuzione dello script.  
  
> [!IMPORTANT]  
>  La password eventualmente specificata nella stringa di connessione per un'origine dati o ai fini della rappresentazione non è contenuta nello script XML. Poiché in tale scenario la password è necessaria per l'elaborazione, è necessario aggiungerla manualmente allo script XML prima che questo venga eseguito oppure aggiungerla dopo l'esecuzione dello script XML.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire soluzioni di modelli tramite la distribuzione guidata](deploy-model-solutions-using-the-deployment-wizard.md)   
 [Sincronizzare database di Analysis Services](synchronize-analysis-services-databases.md)  
  
  
