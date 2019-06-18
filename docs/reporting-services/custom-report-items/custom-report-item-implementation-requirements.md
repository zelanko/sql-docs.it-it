---
title: Requisiti per l'implementazione di elementi dei report personalizzati| Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3e90b19178bc62d0c6ef51a740ab86244709a948
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194319"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisiti per l'implementazione di elementi dei report personalizzati
  In questo argomento vengono illustrati i prerequisiti per lo sviluppo e la distribuzione di elementi dei report personalizzati.  
  
## <a name="development-and-deployment-requirements"></a>Requisiti relativi a sviluppo e distribuzione  
 Per lo sviluppo di un elemento del report personalizzato per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è necessario quanto segue:  
  
-   Accesso amministrativo a un server che esegue [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)] o versioni successive in cui sia installato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Accesso alla documentazione di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Familiarità con le attività di creazione dei componenti e gli spazi dei nomi del modello di componente in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per ulteriori informazioni, vedere gli argomenti relativi alla creazione di componenti e agli spazi dei nomi del modello di componente in Visual Studio nel sito msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Requisiti relativi a linguaggio e spazio dei nomi  
 Gli elementi dei report personalizzati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offrono supporto completo per [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. È possibile sviluppare elementi dei report personalizzati utilizzando un linguaggio di propria scelta conforme a .NET.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] offre allo sviluppatore numerosi strumenti e caratteristiche per semplificare e accelerare i cicli iterativi di codifica, di debug e test, nonché per semplificare la distribuzione. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK include i compilatori [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e C# e gli strumenti correlati.  
  
-   Gli elementi del report personalizzati usano gli spazi dei nomi **Microsoft.ReportDesigner** e <xref:Microsoft.ReportingServices.Interfaces>. Questi elementi sono archiviati negli assembly Microsoft.ReportingServices.Designer.DLL e Microsoft.ReportingServices.Interfaces.DLL, installati con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   I componenti della fase di progettazione degli elementi dei report personalizzati devono implementare le interfacce dallo spazio dei nomi <xref:System.ComponentModel> in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. La documentazione relativa a <xref:System.ComponentModel> è disponibile in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!IMPORTANT]  
>  Per impostazione predefinita, [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] viene installato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a differenza di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Se l'SDK non è installato nel computer e la documentazione associata non è inclusa nella documentazione online, non è possibile utilizzare i collegamenti al contenuto dell'SDK presenti in questa sezione. Dopo aver installato [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK, è possibile aggiungere la documentazione associata alla documentazione online e al sommario attenendosi alle istruzioni descritte in [Aggiungere o rimuovere la documentazione del prodotto per SQL Server](https://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un componente runtime dell'elemento del report personalizzato](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Creazione di un componente dell'elemento del report personalizzato per la fase di progettazione](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Procedura: Distribuire un elemento del report personalizzato](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Librerie di classi dell'elemento del report personalizzato](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
