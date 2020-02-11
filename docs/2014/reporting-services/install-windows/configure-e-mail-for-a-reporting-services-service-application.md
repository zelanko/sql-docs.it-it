---
title: Configurare la posta elettronica per un'applicazione di servizio Reporting Services (SharePoint 2010 e SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6caa06af68eddfd85cb4f19ab2cfb8dd41bbdd95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798106"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services (SharePoint 2010 e SharePoint 2013)
  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gli avvisi dati consentono di inviare avvisi come messaggi di posta elettronica. Per inviare messaggi di posta elettronica potrebbe essere necessario configurare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nonché modificare l'estensione per il recapito tramite posta elettronica per l'applicazione di servizio. Le impostazioni della posta elettronica sono anche richieste se si prevede di utilizzare l'estensione per il recapito tramite posta elettronica per la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] La modalità sharepoint di &#124; SharePoint 2010 e SharePoint 2013.|  
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>Per configurare le impostazioni di posta elettronica per il servizio condiviso  
  
1.  In Amministrazione centrale SharePoint, fare clic su **Gestione dell'applicazione**.  
  
2.  Nel gruppo **Applicazioni di servizio** fare clic su **Gestisci applicazioni di servizio**.  
  
3.  Nell'elenco **Nome** fare clic sul nome dell'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Fare clic su **Impostazioni posta elettronica** nella pagina **Gestione applicazione di Reporting Services** .  
  
5.  Selezionare **Utilizza server SMTP**.  
  
6.  Nella casella **Server SMTP in uscita** digitare il nome di un server SMTP.  
  
7.  Nella casella **Indirizzo mittente** digitare un indirizzo di posta elettronica.  
  
     Questo indirizzo è il mittente di tutti i messaggi di posta elettronica di avviso.  
  
     L'account dell'utente specificato in **Indirizzo mittente** deve essere un account gestito specificato quando il pool di applicazioni è stato configurato per l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se si dispone delle autorizzazioni, è possibile visualizzare un elenco di account gestiti esistenti nella pagina Account di servizio in Amministrazione centrale SharePoint.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>Autenticazione NTLM  
  
1.  Se il proprio ambiente di posta elettronica richiede l'autenticazione NTLM e non consente l'accesso anonimo, è necessario modificare la configurazione dell'estensione per il recapito tramite posta elettronica per le applicazioni di servizio di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Modificare **SMTPAuthenticate** in modo che usi il valore "2". Non è possibile modificare questo valore dall'interfaccia utente. Nell'esempio di script PowerShell seguente viene aggiornata la configurazione per l'estensione per il recapito tramite posta elettronica del server di report per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION". Alcuni dei nodi elencati nello script possono anche essere impostati dall'interfaccia utente, ad esempio l'indirizzo "Da".  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
    $emailXml = [xml]$emailCfg
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  Se è necessario verificare il nome dell'applicazione di servizio, eseguire il cmdlet **Get-SPRSServiceApplication** .  
  
    ```powershell
    Get-SPRSServiceApplication  
    ```  
  
3.  Nell'esempio seguente vengono restituiti i valori correnti dell'estensione per il recapito tramite posta elettronica per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION".  
  
    ```powershell
    $app = get-sprsserviceapplication | Where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
    ```  
  
4.  Nell'esempio seguente viene creato un nuovo file denominato "emailconfig.txt" con i valori correnti dell'estensione per il recapito tramite posta elettronica per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION".  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | Select -ExpandProperty ConfigurationXml | Out-File c:\emailconfig.txt  
    ```
