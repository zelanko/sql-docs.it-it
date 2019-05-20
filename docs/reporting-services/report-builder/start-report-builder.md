---
title: Avviare Generatore report | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8170a46bdcb0d6249b59965e190ff3eb6d14b4d0
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571743"
---
# <a name="start-report-builder"></a>Avviare Generatore report

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] è un ambiente di creazione di report autonomo. Permette di creare report impaginati e di pubblicarli in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato in modalità nativa o nella modalità integrata SharePoint.  
  
 La prima volta che si avvia [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dal portale Web [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità integrata SharePoint, viene richiesto di scaricarlo dall'Area download Microsoft. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 L'utente o un amministratore può anche [installare Generatore report nel computer dall'Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=219138). Per altri dettagli, vedere "Installare Generatore report con Systems Manager Server" in [Installare Generatore Report](../../reporting-services/install-windows/install-report-builder.md) .
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] non viene installato quando si installa SQL Server Reporting Services; è necessario scaricarlo e installarlo separatamente.  
  
 Quando si avvia [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dal portale Web o dal sito di SharePoint, se si apre una versione precedente di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] , contattare l'amministratore, che può aggiornare la versione sul portale Web o sul sito di SharePoint.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversionmd-from-the-includessrsnoversionincludesssrsnoversion-mdmd-web-portal"></a>Per avviare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] dal portale Web [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  Digitare l'URL per il server di report nella barra degli indirizzi del browser. L'URL predefinito è https://\<*nomeserver*>/reports.  
  
2.  Nella barra superiore del portale Web, selezionare **Nuovo** > **Report impaginato**.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     La prima volta viene richiesto di [installare Generatore Report](../../reporting-services/install-windows/install-report-builder.md). 
  
     In seguito, viene aperto [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ed è possibile creare un report impaginato o aprire un report dal server di report.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversionmd-in-sharepoint-integrated-mode"></a>Per avviare [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] in modalità integrata SharePoint  
  
1.  Accedere al sito di SharePoint che contiene la raccolta desiderata.  
  
2.  Aprire la raccolta.  
  
3.  Fare clic su **Documenti**.  
  
4.  Scegliere **Report di Generatore report** dal menu **Nuovo documento**.  
  
     La prima volta viene avviata la Configurazione guidata di [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] per SQL Server. Per ulteriori informazioni, vedere [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md) .  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] ed è possibile creare un report impaginato o aprire un report nel server di report.  
  
     **Nota** Se nel menu **Nuovo documento** non sono elencati **Report di Generatore report**, **Modello di Generatore report**e **Origine dati report**, i relativi tipi di contenuto devono essere aggiunti alla raccolta di SharePoint. Per altre informazioni, vedere [Aggiungere i tipi di contenuto di Reporting Services a una raccolta di SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

## <a name="next-steps"></a>Passaggi successivi

[Generatore report in SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[Impostare le opzioni predefinite per Generatore Report](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
