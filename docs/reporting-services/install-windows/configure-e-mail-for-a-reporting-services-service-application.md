---
description: Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services
title: Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 689bb92eabac3b909291845cb44bdf951f4f7977
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427103"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application"></a>Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gli avvisi dati consentono di inviare avvisi come messaggi di posta elettronica. Per inviare messaggi di posta elettronica potrebbe essere necessario configurare l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nonché modificare l'estensione per il recapito tramite posta elettronica per l'applicazione di servizio. Le impostazioni della posta elettronica sono anche richieste se si prevede di utilizzare l'estensione per il recapito tramite posta elettronica per la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
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
  
1.  Se il proprio ambiente di posta elettronica richiede l'autenticazione NTLM e non consente l'accesso anonimo, è necessario modificare la configurazione dell'estensione per il recapito tramite posta elettronica per le applicazioni di servizio di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Ad esempio, se viene visualizzato il messaggio seguente per **Ultimi risultati** nella pagina **Gestisci sottoscrizioni** page:subscriptions.  
  
    -   Errore durante l'invio della posta: Il server SMTP richiede una connessione protetta oppure il client non è stato autenticato. Risposta del server: 5.7.1 Client non autenticato. La posta non verrà inviata nuovamente.  
  
     Modificare **SMTPAuthenticate** in modo che usi il valore "2". Non è possibile modificare questo valore dall'interfaccia utente. Nell'esempio di script PowerShell seguente viene aggiornata la configurazione per l'estensione per il recapito tramite posta elettronica del server di report per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION". Alcuni dei nodi elencati nello script possono anche essere impostati dall'interfaccia utente, ad esempio l'indirizzo "Da".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  Se è necessario verificare il nome dell'applicazione di servizio, eseguire **Get-SPRSServiceApplication cmdlet**.  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  Nell'esempio seguente vengono restituiti i valori correnti dell'estensione per il recapito tramite posta elettronica per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  Nell'esempio seguente viene creato un nuovo file denominato "emailconfig.txt" con i valori correnti dell'estensione per il recapito tramite posta elettronica per l'applicazione di servizio denominata "SSRS_TESTAPPLICATION".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  
Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
