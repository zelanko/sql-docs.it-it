---
title: Autenticazione in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c4fc4d98eb32fb07def2fd317ebb7f5a6f6332cb
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154127"
---
# <a name="authentication-in-reporting-services"></a>Autenticazione in Reporting Services
  L'autenticazione è il processo di determinazione del diritto di un utente a un'identità. Per autenticare un utente sono disponibili numerose tecniche. La più comune consiste nell'utilizzo di password. Quando si implementa l'autenticazione basata su form, ad esempio, si sceglie un'implementazione che richiede le credenziali agli utenti (generalmente tramite un'interfaccia in cui vengono richiesti un nome di accesso e una password), quindi si convalidano gli utenti in base a un archivio dati, ad esempio una tabella di database o un file di configurazione. Se non è possibile convalidare le credenziali, il processo di autenticazione non riesce e all'utente viene assegnata un'identità anonima.  
  
## <a name="custom-authentication-in-reporting-services"></a>Autenticazione personalizzata in Reporting Services  
 In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] l'autenticazione degli utenti viene gestita dal sistema operativo Windows tramite la sicurezza integrata o tramite operazioni esplicite di ricezione e convalida delle credenziali utente. L'autenticazione personalizzata può essere sviluppata in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] per supportare schemi di autenticazione aggiuntivi. Ciò è possibile tramite l'interfaccia dell'estensione di sicurezza <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension>. Tutte le estensioni ereditano dall'interfaccia di base <xref:Microsoft.ReportingServices.Interfaces.IExtension> per qualsiasi estensione distribuita e utilizzata dal server di report. <xref:Microsoft.ReportingServices.Interfaces.IExtension> e <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension> sono membri dello spazio dei nomi <xref:Microsoft.ReportingServices.Interfaces>.  
  
 La principale modalità di autenticazione in un server di report in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] è costituita dal metodo <xref:ReportService2010.ReportingService2010.LogonUser%2A>. Questo membro del servizio Web Reporting Services può essere utilizzato per passare le credenziali utente a un server di report per la convalida. L'estensione di sicurezza sottostante implementa **Iauthenticationextension** che contiene il codice di autenticazione personalizzato. Nell'esempio di autenticazione basata su form, **LogonUser**, che esegue un controllo di autenticazione in base alle credenziali fornite e a un archivio utente personalizzato in un database. Un esempio di implementazione di **LogonUser** è simile al seguente:  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 La funzione di esempio seguente viene utilizzata per verificare le credenziali fornite:  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>Flusso di autenticazione  
 Il servizio Web Reporting Services fornisce estensioni di autenticazione personalizzate per l'abilitazione dell'autenticazione basata su form da parte di Gestione report e del server di report.  
  
 Il metodo <xref:ReportService2010.ReportingService2010.LogonUser%2A> del servizio Web Reporting Services viene utilizzato per inviare le credenziali al server di report per l'autenticazione. Il servizio Web utilizza le intestazioni HTTP per passare un ticket di autenticazione (noto come "cookie") dal server al client per le richieste di accesso convalidate.  
  
 Nell'illustrazione seguente è rappresentato il metodo di autenticazione degli utenti per il servizio Web quando l'applicazione viene distribuita con un server di report configurato per l'utilizzo di un'estensione di autenticazione personalizzata.  
  
 ![Flusso di autenticazione di sicurezza per Reporting Services](../../media/rosettasecurityextensionauthenticationflow.gif "Flusso di autenticazione di sicurezza per Reporting Services")  
  
 Come illustrato nella figura 2, il processo di autenticazione è il seguente:  
  
1.  Un'applicazione client chiama il metodo <xref:ReportService2010.ReportingService2010.LogonUser%2A> del servizio Web per autenticare un utente.  
  
2.  Il servizio Web effettua una chiamata per il <xref:ReportService2010.ReportingService2010.LogonUser%2A> metodo di estensione di sicurezza, in particolare, la classe che implementa **IAuthenticationExtension**.  
  
3.  L'implementazione di <xref:ReportService2010.ReportingService2010.LogonUser%2A> convalida il nome utente e la password nell'archivio utente o nell'autorità di sicurezza.  
  
4.  Dopo la corretta esecuzione dell'autenticazione, il servizio Web crea un cookie e lo gestisce per la sessione.  
  
5.  Il servizio Web restituisce il ticket di autenticazione all'applicazione chiamante nell'intestazione HTTP.  
  
 Quando un utente viene correttamente autenticato dal servizio Web tramite l'estensione di sicurezza, viene generato un cookie utilizzato per le richieste successive. Il cookie non può essere reso persistente nell'autorità di sicurezza personalizzata perché il server di report non possiede l'autorità di sicurezza. Il cookie viene restituito dal metodo del servizio Web <xref:ReportService2010.ReportingService2010.LogonUser%2A> e viene utilizzato nelle successive chiamate al metodo del servizio Web e nell'accesso con URL.  
  
> [!NOTE]  
>  Per evitare di compromettere il cookie durante la trasmissione, i cookie di autenticazione restituiti da <xref:ReportService2010.ReportingService2010.LogonUser%2A> devono essere trasmessi in modo protetto utilizzando la crittografia SSL (Secure Sockets Layer).  
  
 Se si accede al server di report tramite accesso con URL quando un'estensione di sicurezza personalizzata è installata, Internet Information Services (IIS) e [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] gestiscono automaticamente la trasmissione del ticket di autenticazione. Se si accede al server di report tramite l'API SOAP, l'implementazione della classe proxy deve includere supporto aggiuntivo per la gestione del ticket di autenticazione. Per ulteriori informazioni sull'utilizzo dell'API SOAP e sulla gestione del ticket di autenticazione, vedere "Utilizzo del servizio Web con la sicurezza personalizzata".  
  
## <a name="forms-authentication"></a>Autenticazione basata su form  
 L'autenticazione basata su form è un tipo di autenticazione di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] con la quale un utente non autenticato viene indirizzato a un form HTML. Dopo che l'utente ha fornito le credenziali, il sistema produce un cookie contenente un ticket di autenticazione. In occasione delle richieste successive, il sistema controlla innanzitutto il cookie per verificare se l'utente è già stato autenticato dal server di report.  
  
 È possibile estendere [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] per supportare l'autenticazione basata su form utilizzando le interfacce di estendibilità della sicurezza disponibili tramite l'API di Reporting Services. Se si estende [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] per l'utilizzo dell'autenticazione basata su form, utilizzare SSL (Secure Sockets Layer) per tutte le comunicazioni con il server di report per impedire a utenti malintenzionati di accedere al cookie di un altro utente. SSL consente ai client e a un server di report di autenticarsi a vicenda per garantire che il contenuto delle comunicazioni tra i due computer non possa essere letto da nessun altro computer. Tutti i dati inviati da un client tramite una connessione SSL vengono crittografati in modo che gli utenti malintenzionati non possano intercettare le password o i dati inviati a un server di report.  
  
 L'autenticazione basata su form viene in genere implementata per supportare account e autenticazione per piattaforme diverse da Windows. Quando un utente richiede l'accesso a un server di report, viene visualizzata un'interfaccia grafica e le credenziali fornite vengono inviate a un'autorità di sicurezza per l'autenticazione.  
  
 L'autenticazione basata su form richiede la presenza di una persona per l'immissione delle credenziali. Per le applicazioni automatiche che comunicano direttamente con il servizio Web Reporting Services, l'autenticazione basata su form deve essere utilizzata in combinazione con uno schema di autenticazione personalizzato.  
  
 L'autenticazione basata su form è adatta per [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nei casi seguenti:  
  
-   Quando è necessario archiviare e autenticare utenti che non dispongono di account di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
-   Quando è necessario fornire un modulo di interfaccia utente personalizzato come pagina di accesso tra pagine diverse in un sito Web.  
  
 Quando si scrive un'estensione di sicurezza personalizzata che supporta l'autenticazione basata su form, prendere in considerazione gli aspetti seguenti:  
  
-   Se si utilizza l'autenticazione basata su form, l'accesso anonimo deve essere abilitato nella directory virtuale del server di report in Internet Information Services (IIS).  
  
-   L'autenticazione di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] deve essere impostata su Forms. È possibile configurare l'autenticazione di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] nel file Web.config per il server di report.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] consente di autenticare e autorizzare gli utenti con l'autenticazione di Windows o con l'autenticazione personalizzata, ma non con entrambe. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] non supporta l'utilizzo simultaneo di più estensioni di sicurezza.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione di sicurezza](../security-extension/implementing-a-security-extension.md)  
  
  
