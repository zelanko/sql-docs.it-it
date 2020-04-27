---
title: Configurare l'autenticazione personalizzata o basata su form nel server di report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7602ce0ef0e75c3c2eb1ee5a5a47e3fe56b87f44
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102138"
---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>Configurare l'autenticazione personalizzata o basata su form nel server di report
  Reporting Services offre un'architettura estensibile che consente di inserire moduli di autenticazione basata su form o personalizzata. È possibile implementare un'estensione di autenticazione personalizzata, se i requisiti di distribuzione non includono la sicurezza integrata di Windows o l'autenticazione di base. Lo scenario più comune per l'utilizzo dell'autenticazione personalizzata consiste nel supporto dell'accesso Internet o extranet a un'applicazione Web. La sostituzione dell'estensione di autenticazione di Windows predefinita con un'estensione di autenticazione personalizzata consente un maggiore controllo sulle modalità di concessione dell'accesso al server di report agli utenti esterni.  
  
 La distribuzione di un'estensione di autenticazione personalizzata richiede sostanzialmente più passaggi, che includono la copia di un assembly e dei file dell'applicazione, la modifica dei file di configurazione e il test. In questo argomento vengono illustrate solo le impostazioni di autenticazione che l'utente specifica nei file di configurazione.  
  
> [!NOTE]  
>  La creazione di un'estensione di autenticazione personalizzata richiede codice personalizzato ed esperienza in materia di sicurezza di [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Se non si desidera creare un'estensione di autenticazione personalizzata, è possibile utilizzare gruppi e account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory, ma è necessario ridurre notevolmente l'ambito di distribuzione del server di report. Per altre informazioni sull'autenticazione personalizzata, vedere [Implementazione di un'estensione di sicurezza](../extensions/security-extension/implementing-a-security-extension.md).  
  
 Se inoltre si desidera utilizzare l'autenticazione basata su form o un'estensione di autenticazione personalizzata in un ambiente [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrato con un prodotto SharePoint, è necessario configurare il sito di SharePoint per l'utilizzo del metodo di autenticazione scelto. Per altre informazioni sulla configurazione dell'autenticazione in SharePoint, vedere [Esempi di autenticazione](https://go.microsoft.com/fwlink/?LinkId=115575) in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).  
  
### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>Per configurare un server di report per l'utilizzo dell'autenticazione personalizzata  
  
1.  Aprire RSReportServer.config in un editor di testo.  
  
2.  Trovare <`Authentication`>.  
  
3.  Copiare la struttura XML seguente:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  Incollarlo sulle voci esistenti per <`Authentication`>.  
  
     Si noti che non è possibile utilizzare `Custom` con altri tipi di autenticazione.  
  
5.  Salvare il file.  
  
6.  Aprire il file Web.config per il server di report. Per impostazione predefinita, il percorso di questo file è \Programmi\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer.  
  
7.  Trovare `authentication mode` e impostarlo su `Forms`.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
8.  Trovare `identity impersonate` e impostarlo su `False`.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
9. Aprire il file Web.config per Gestione report. Per impostazione predefinita, il percorso di questo file è \Programmi\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager.  
  
10. Trovare `authentication mode` e impostarlo su `Forms`.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. Trovare `identity impersonate` e impostarlo su `False`.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. Aggiungere la struttura dell'elemento `PassThroughCookies` al file di configurazione. Per altre informazioni, vedere [Configurare Gestione report per il passaggio di cookie di autenticazione personalizzati](configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
13. Salvare il file.  
  
14. Se è stata configurata una distribuzione con scalabilità orizzontale, ripetere tutti i passaggi precedenti per gli altri server di report presenti nella distribuzione.  
  
15. Riavviare il server di report per cancellare qualsiasi sessione attualmente aperta.  
  
## <a name="see-also"></a>Vedi anche  
 [Implementazione di un'estensione di sicurezza](../extensions/security-extension/implementing-a-security-extension.md)   
 [Autenticazione con il server di report](authentication-with-the-report-server.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Configurare l'autenticazione di base nel server di report](configure-basic-authentication-on-the-report-server.md)   
 [Configurare l'autenticazione di Windows nel server di report](configure-windows-authentication-on-the-report-server.md)  
  
  
