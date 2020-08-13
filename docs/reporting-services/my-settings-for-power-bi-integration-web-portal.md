---
title: Impostazioni personali per l'integrazione di Power BI (portale Web) | Microsoft Docs
description: Informazioni sulla pagina Impostazioni personali nel portale Web di Reporting Services e sul modo in cui viene usata dai singoli utenti per gestire l'accesso con Power BI.
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f25ab8f848c642de95f1ba62eaca15bbb8b7e7d9
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248578"
---
# <a name="my-settings-for-power-bi-integration-web-portal"></a>Impostazioni personali per Integrazione di Power BI (portale Web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

La pagina **Impostazioni personali** di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] viene usata dai singoli utenti per gestire l'accesso con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Quando si eseguono i passaggi per aggiungere un elemento del report, viene richiesto automaticamente di eseguire l'accesso.  Tuttavia, è possibile usare la pagina **Impostazioni personali** per accedere manualmente o per disconnettersi.  Se l'opzione di menu **Impostazioni personali** non è visibile, il server di report non è stato integrato con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  Per altre informazioni, vedere [Integrazione del server di report e di Power BI &#40;Gestione configurazione&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>Perché eseguire l'accesso

 Quando si accede, viene stabilita una relazione tra l'account utente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e l'account [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  L'accesso crea un token di sicurezza valido per 90 giorni. Se il token scade e sono presenti elementi bloccati di Power BI, verrà visualizzata una notifica.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
I riquadri dei dashboard di [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] non verranno aggiornati fino a quando non si accede nuovamente mediante **Impostazioni personali**.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Dopo aver eseguito l'accesso, verrà creato un nuovo token di sicurezza.  Dopo l'accesso, viene iniziato l'aggiornamento dei riquadri dei dashboard sulla base delle pianificazioni configurate in precedenza.  

## <a name="next-steps"></a>Passaggi successivi

[Integrazione del server di report di Power BI](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[Aggiungere elementi di Reporting Services ai dashboard di Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Dashboard in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Portale Web](../reporting-services/web-portal-ssrs-native-mode.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
