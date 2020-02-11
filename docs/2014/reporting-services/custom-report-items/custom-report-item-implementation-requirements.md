---
title: Requisiti per l'implementazione di elementi dei report personalizzati| Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0000e0c7a5933003544de22b60a8adc4d9c59c82
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74684449"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisiti per l'implementazione di elementi dei report personalizzati
  In questo argomento vengono illustrati i prerequisiti per lo sviluppo e la distribuzione di elementi dei report personalizzati.  
  
## <a name="development-and-deployment-requirements"></a>Requisiti relativi a sviluppo e distribuzione  
 Per lo sviluppo di un elemento del report personalizzato per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è necessario quanto segue:  
  
-   Accesso amministrativo a un server che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e.  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]o versione successiva con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] la Software Development Kit (SDK) installata.  
  
-   Accesso alla documentazione di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Familiarità con le attività di creazione dei componenti e gli spazi dei nomi del modello di componente in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per ulteriori informazioni, vedere gli argomenti relativi alla creazione di componenti e agli spazi dei nomi del modello di componente in Visual Studio nel sito msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Requisiti relativi a linguaggio e spazio dei nomi  
 Gli elementi dei report personalizzati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offrono supporto completo per [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. È possibile sviluppare elementi dei report personalizzati utilizzando un linguaggio di propria scelta conforme a .NET.  
  
 
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] offre allo sviluppatore numerosi strumenti e caratteristiche per semplificare e accelerare i cicli iterativi di codifica, di debug e test, nonché per semplificare la distribuzione. 
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK include i compilatori [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e C# e gli strumenti correlati.  
  
-   Gli elementi dei report personalizzati utilizzano gli spazi dei nomi `Microsoft.ReportDesigner` e <xref:Microsoft.ReportingServices.Interfaces>. Questi elementi sono archiviati negli assembly Microsoft.ReportingServices.Designer.DLL e Microsoft.ReportingServices.Interfaces.DLL, installati con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   I componenti della fase di progettazione degli elementi dei report personalizzati devono implementare le interfacce dallo spazio dei nomi <xref:System.ComponentModel> in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. La documentazione relativa a <xref:System.ComponentModel> è disponibile in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!IMPORTANT]  
>  Per impostazione predefinita, [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] viene installato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a differenza di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Se l'SDK non è installato nel computer e la documentazione associata non è inclusa nella documentazione online, non è possibile utilizzare i collegamenti al contenuto dell'SDK presenti in questa sezione. Dopo aver installato [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK, è possibile aggiungere la documentazione associata alla documentazione online e al sommario attenendosi alle istruzioni descritte in [Aggiungere o rimuovere la documentazione del prodotto per SQL Server](../../2014-toc/index.yml).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un componente runtime dell'elemento del report personalizzato](creating-a-custom-report-item-run-time-component.md)   
 [Creazione di un componente della fase di progettazione di un elemento del report personalizzato](creating-a-custom-report-item-design-time-component.md)   
 [Procedura: distribuire un elemento del report personalizzato](how-to-deploy-a-custom-report-item.md)   
 [Librerie di classi dell'elemento del report personalizzato](custom-report-item-class-libraries.md)  
  
  
