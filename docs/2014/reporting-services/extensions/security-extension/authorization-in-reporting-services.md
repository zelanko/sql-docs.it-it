---
title: Autorizzazione in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- authorization [Reporting Services]
ms.assetid: 15fc1c7b-560c-4737-b126-e0d428a1b530
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ac9f9882724e9ba0341bf11af948c948070e6774
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60153526"
---
# <a name="authorization-in-reporting-services"></a>Autorizzazione in Reporting Services
  L'autorizzazione è il processo tramite cui viene determinato se a un'identità deve essere concesso il tipo di accesso richiesto a una determinata risorsa nel database del server di report. In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] viene utilizzata un'architettura di autorizzazione basata sui ruoli che consente di concedere a un utente l'accesso a una determinata risorsa in base all'assegnazione di ruolo dell'utente per l'applicazione. Le estensioni di sicurezza per [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] contengono un'implementazione di un componente di autorizzazione utilizzata per concedere l'accesso agli utenti dopo l'autenticazione nel server di report. L'autorizzazione viene richiamata quando un utente tenta di eseguire un'operazione nel sistema o in un elemento del server di report tramite l'API SOAP e l'accesso con URL. Questo è reso possibile tramite l'interfaccia di estensione di sicurezza **IAuthorizationExtension**. Come dichiarato in precedenza, tutte le estensioni ereditano da **IExtension** l'interfaccia di base per qualsiasi estensione distribuita. **IExtension** e **IAuthorizationExtension** appartengono le **ReportingServices** dello spazio dei nomi.  
  
## <a name="checking-access"></a>Controllo dell'accesso  
 Nell'ambito dell'autorizzazione, la chiave per qualsiasi implementazione della sicurezza personalizzata è il controllo dell'accesso, implementato nel metodo <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> viene chiamato ogni volta che un utente tenta un'operazione sul server di report. Il metodo <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> è sottoposto a overload per ogni tipo di operazione. Per le operazioni sulle cartelle, un esempio di controllo dell'accesso potrebbe essere simile al seguente:  
  
```  
// Overload for Folder operations  
public bool CheckAccess(  
   string userName,   
   IntPtr userToken,   
   byte[] secDesc,   
   FolderOperation requiredOperation)  
{  
   // If the user is the administrator, allow unrestricted access.  
   if (userName == m_adminUserName)   
      return true;  
  
   AceCollection acl = DeserializeAcl(secDesc);  
   foreach(AceStruct ace in acl)  
   {  
         if (userName == ace.PrincipalName)  
         {  
            foreach(FolderOperation aclOperation in   
               ace.FolderOperations)  
            {  
               if (aclOperation == requiredOperation)  
                     return true;  
            }  
         }  
   }  
   return false;  
}  
```  
  
 Il server di report chiama il metodo <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> passando il nome dell'utente connesso, un token utente, il descrittore di sicurezza per l'elemento e l'operazione richiesta. A questo punto il descrittore di sicurezza viene controllato per verificare se il nome utente e l'autorizzazione sono appropriati per il completamento della richiesta, quindi viene restituito `true` per indicare che l'accesso è concesso o `false` per indicare che l'accesso è negato.  
  
## <a name="security-descriptors"></a>Descrittori di sicurezza  
 Quando si impostano i criteri di autorizzazione per gli elementi nel database del server di report, un'applicazione client (ad esempio Gestione report) invia le informazioni utente all'estensione di sicurezza insieme ai criteri di sicurezza per l'elemento. I criteri di sicurezza e le informazioni utente sono collettivamente denominati descrittore di sicurezza. Un descrittore di sicurezza contiene le informazioni seguenti per un elemento nel database del server di report:  
  
-   Gruppo o utente che dispone di un tipo di autorizzazione per l'esecuzione di operazioni sull'elemento.  
  
-   Tipo di elemento.  
  
-   Elenco di controllo di accesso discrezionale che controlla l'accesso all'elemento.  
  
 I descrittori di sicurezza vengono creati utilizzando i metodi <xref:ReportService2010.ReportingService2010.SetPolicies%2A> e <xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A> del servizio Web.  
  
### <a name="authorization-flow"></a>Flusso di autorizzazione  
 L'autorizzazione in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] viene controllata dall'estensione di sicurezza attualmente configurata per l'esecuzione nel server. L'autorizzazione è basata sul ruolo ed è limitata alle autorizzazioni e alle operazioni fornite dall'architettura di sicurezza di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Nel diagramma seguente è illustrato il processo di autorizzazione degli utenti per l'utilizzo degli elementi nel database del server di report:  
  
 ![Flusso dell'autorizzazione di sicurezza di Reporting Services](../../media/rosettasecurityextensionauthorizationflow.gif "Flusso dell'autorizzazione di sicurezza di Reporting Services")  
  
 Come illustrato in questo diagramma, per l'autorizzazione viene applicata la sequenza seguente:  
  
1.  Dopo l'autenticazione, le applicazioni client inviano le richieste al server di report tramite i metodi del servizio Web Reporting Services. Un ticket di autenticazione viene passato al server di report sotto forma di cookie nell'intestazione HTTP di ogni richiesta Web.  
  
2.  Il cookie viene convalidato prima di qualsiasi controllo dell'accesso.  
  
3.  Dopo la convalida del cookie, il server di report chiama <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> e all'utente viene fornita un'identità.  
  
4.  L'utente tenta di eseguire un'operazione tramite il servizio Web Reporting Services.  
  
5.  Il server di report chiama il metodo <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>.  
  
6.  Il descrittore di sicurezza viene recuperato e passato a un'implementazione dell'estensione di sicurezza personalizzata di <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. A questo punto, l'utente, il gruppo o il computer viene confrontato con il descrittore di sicurezza dell'elemento a cui viene eseguito l'accesso e viene autorizzato a eseguire l'operazione richiesta.  
  
7.  Se l'utente è autorizzato, il servizio Web esegue l'operazione e restituisce una risposta all'applicazione chiamante.  
  
  
