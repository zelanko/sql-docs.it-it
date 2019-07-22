---
title: Registrazione di un nome dell'entità servizio per le connessioni Kerberos | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 06ac9e16ccdd84020d67ce3c3a77abcb49bb4343
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938219"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Registrazione di un nome dell'entità servizio per le connessioni Kerberos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per utilizzare l'autenticazione Kerberos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario che si verifichino entrambe le seguenti condizioni:  
  
-   I computer client e server devono fare parte dello stesso dominio Windows o di domini trusted.  
  
-   Un nome dell'entità servizio (SPN, Service Principal Name) deve essere stato registrato in Active Directory, che presuppone il ruolo del centro di distribuzione chiavi (KDC) in un dominio Windows. Una volta registrato, il nome SPN esegue il mapping all'account Windows che ha avviato il servizio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se la registrazione del nome SPN non è stata eseguita o ha avuto esito negativo, il livello di sicurezza di Windows non è in grado di determinare l'account associato al nome SPN e l'autenticazione Kerberos non verrà utilizzata.  
  
    > [!NOTE]  
    >  Se il server non è in grado di eseguire la registrazione automatica del nome SPN, è necessario effettuare l'operazione manualmente. Vedere [Registrazione manuale del nome SPN](#Manual).  
  
È possibile verificare che una connessione utilizzi Kerberos eseguendo una query sulla vista a gestione dinamica sys.dm_exec_connections. Eseguire la query seguente e controllare il valore della colonna auth_scheme. Se l'autenticazione Kerberos è abilitata, tale valore corrisponderà a "KERBEROS".  
  
```sql  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** è uno strumento di diagnostica che semplifica la risoluzione dei problemi di connettività correlati a Kerberos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Microsoft Kerberos Configuration Manager per SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
##  <a name="Role"></a> Ruolo del nome SPN nell'autenticazione  
 Quando un'applicazione apre una connessione e utilizza l'autenticazione di Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client passa il nome del computer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il nome dell'istanza ed eventualmente un nome SPN. Se passato dalla connessione, il nome SPN viene utilizzato senza alcuna modifica.  
  
 Se non viene passato un nome SPN, viene costruito un nome SPN predefinito in base al protocollo utilizzato, al nome del server e al nome di istanza.  
  
 In entrambi gli scenari indicati in precedenza, il nome SPN viene inviato al centro di distribuzione chiavi per ottenere un token di sicurezza per l'autenticazione della connessione. Se non è possibile ottenere un token di sicurezza, l'autenticazione utilizza NTLM.  
  
 Un nome dell'entità servizio (SPN) è il nome con cui un client identifica in modo univoco un'istanza di un servizio. Questo nome può essere utilizzato dal servizio di autenticazione Kerberos per l'autenticazione di un servizio. Per connettersi a un servizio, un client individua un'istanza del servizio, compone un nome SPN per l'istanza, esegue la connessione al servizio e presenta il nome SPN al servizio per l'autenticazione.  
  
> [!NOTE]  
>  Le informazioni incluse in questo argomento si applicano anche a configurazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano il clustering.  
  
 L'autenticazione di Windows è il metodo preferito per l'autenticazione in SQL Server da parte degli utenti. I client che utilizzano l'autenticazione di Windows vengono autenticati tramite NTLM o Kerberos. In un ambiente Active Directory l'autenticazione Kerberos viene sempre tentata per prima. L'autenticazione Kerberos non è disponibile per client [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] che utilizzano named pipe.  
  
##  <a name="Permissions"></a> Autorizzazioni  
 Quando il servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene avviato, tenta di registrare il nome dell'entità servizio (SPN). Se l'account che avvia SQL Server non ha l'autorizzazione necessaria per registrare un nome SPN in Servizi di dominio Active Directory, questa chiamata non riesce e viene registrato un messaggio di avviso nel registro eventi applicazioni nonché nel log degli errori di SQL Server. Per registrare il nome SPN, è necessario che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] venga eseguito con un account predefinito, ad esempio Sistema locale (non consigliato) o NETWORK SERVICE, oppure con un account che dispone dell'autorizzazione necessaria per registrare un nome SPN, ad esempio un account di amministratore di dominio. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito nel sistema operativo  [!INCLUDE[win7](../../includes/win7-md.md)] o  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] , è possibile eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando un account virtuale o un account dei servizi gestiti (MSA). Entrambi gli account virtuali e MSA possono registrare un SPN. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene eseguito con nessuno di questi account, il nome SPN non viene registrato all'avvio e l'amministratore di dominio lo dovrà registrare manualmente.  
  
> [!NOTE]  
>  Quando il dominio di Windows è configurato per essere eseguito a un livello funzionale inferiore a quello di [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Windows Server 2008 R2, l'Account dei servizi gestiti non disporrà delle autorizzazioni necessarie per registrare i nomi SPN per il servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Se l'autenticazione Kerberos è richiesta, l'amministratore di dominio deve registrare manualmente i nomi SPN di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sull'Account dei servizi gestiti.  
  
 Per altre informazioni su come concedere l'autorizzazione di lettura o scrittura per un nome SPN a un account diverso da quello di amministratore di dominio, vedere l'articolo della Knowledge Base [Utilizzo dell'autenticazione Kerberos in SQL Server](https://support.microsoft.com/kb/319723).  
  
 Maggiori informazioni sono disponibili nell'articolo [How to Implement Kerberos Constrained Delegation with SQL Server 2008](https://technet.microsoft.com/library/ee191523.aspx)(Come implementare la delega vincolata Kerberos con SQL Server 2008)  
  
##  <a name="Formats"></a> Formati dei nomi SPN  
 A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], il formato dei nomi SPN è stato modificato per supportare l'autenticazione Kerberos con il protocollo TCP/IP, le named pipe e la memoria condivisa. Di seguito sono riportati i formati del nome SPN supportati per le istanze denominate e predefinite.  
  
**Istanza denominata**  
  
-   **MSSQLSvc/\<FQDN:[\<porta | \<nomeistanza>]** , dove:  
  
    -   **MSSQLSvc** è il servizio da registrare.  
  
    -   **\<FQDN>** è il nome di dominio completo del server.  
  
    -   **\<porta>** è il numero di porta TCP.  
  
    -   **\<nomeistanza>** è il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Istanza predefinita**  
  
-   **MSSQLSvc/\<FQDN>:\<porta>**  | **MSSQLSvc/\<FQDN>** , dove:  
  
    -   **MSSQLSvc** è il servizio da registrare.  
  
    -   **\<FQDN>** è il nome di dominio completo del server.  
  
    -   **\<porta>** è il numero di porta TCP.  
  
    > [!NOTE]
    > Per il nuovo formato del nome SPN non è necessario specificare un numero di porta. Di conseguenza, un server con più porte o un protocollo che non utilizza numeri di porta può utilizzare l'autenticazione Kerberos.  
   
|||  
|-|-|  
|MSSQLSvc/\<FQDN>:<port>|Nome SPN predefinito generato dal provider quando si utilizza il protocollo TCP. \<porta> è un numero di porta TCP.|  
|MSSQLSvc/\<FQDN>|Nome SPN predefinito generato dal provider per un'istanza predefinita quando si utilizza un protocollo diverso da TCP. \<FQDN> è un nome di dominio completo.|  
|MSSQLSvc/\<FQDN>:\<nomeistanza>|Nome SPN predefinito generato dal provider per un'istanza denominata quando si usa un protocollo diverso da TCP. \<nomeistanza> è il nome di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  

> [!NOTE]  
> Nel caso di una connessione TCP/IP, in cui la porta TCP è inclusa nel nome SPN, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario abilitare il protocollo TCP perché un utente sia in grado di connettersi utilizzando l'autenticazione Kerberos. 

##  <a name="Auto"></a> Registrazione automatica del nome SPN  
 Quando viene avviata un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di registrare il nome SPN per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando l'istanza viene arrestata, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di annullare la registrazione del nome SPN. Per una connessione TCP/IP, il nome SPN viene registrato nel formato *MSSQLSvc/\<FQDN>* : *\<tcpport>* . Sia le istanze denominate che quella predefinita vengono registrate come *MSSQLSvc* e differenziate in base al valore *\<tcpport>* .  
  
 Per altre connessioni che supportano l'autenticazione Kerberos, il nome SPN viene registrato nel formato *MSSQLSvc/\<FQDN>* / *\<nomeistanza>* per un'istanza denominata e nel formato *MSSQLSvc/\<FQDN>* per l'istanza predefinita.  
  
 Se l'account di servizio non dispone delle autorizzazioni richieste per eseguire queste azioni, potrebbe essere necessario intervenire manualmente per registrare o annullare la registrazione del nome SPN.  
  
##  <a name="Manual"></a> Registrazione manuale del nome SPN  
Per registrare manualmente il nome SPN, l'amministratore deve utilizzare lo strumento Setspn.exe disponibile negli strumenti di supporto Microsoft di [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] . Per altre informazioni, vedere l'articolo della Knowledge Base [Strumenti di supporto di Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777) .  
  
Setspn.exe è un'utilità della riga di comando che consente di leggere, modificare ed eliminare la proprietà della directory del nome dell'entità servizio (SPN). Questo strumento consente inoltre di visualizzare i nomi SPN correnti, reimpostare i nomi SPN predefiniti dell'account e aggiungere o eliminare nomi SPN supplementari.  
  
L'esempio seguente illustra la sintassi usata per registrare manualmente un nome SPN per una connessione TCP/IP mediante un account utente di dominio:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```  
  
> [!NOTE]
> Se un nome SPN esiste già, è necessario eliminarlo prima che sia possibile registrarlo nuovamente. Per eseguire questa operazione, utilizzare il comando `setspn` con l'opzione `-D` . Negli esempi seguenti viene illustrato come registrare manualmente un nuovo nome SPN basato su un'istanza. Per un'istanza predefinita con un account utente di dominio, usare:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
Per un'istanza denominata, utilizzare il formato seguente:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com/instancename redmond\accountname  
```  
  
##  <a name="Client"></a> Connessioni client  
 I nomi SPN specificati dall'utente sono supportati nei driver client. Se non viene specificato, tuttavia, il nome SPN verrà generato automaticamente in base al tipo di una connessione client. Per una connessione TCP, il formato del nome SPN è *MSSQLSvc*/*FQDN*:[*porta*] sia per le istanze denominate che per quella predefinita.  
  
Per le connessioni con named pipe e con memoria condivisa, il formato del nome SPN è *MSSQLSvc/\<FQDN>:\<nomeistanza* per un'istanza denominata e *MSSQLSvc/\<FQDN* per l'istanza predefinita.  
  
 **Utilizzo di un account di servizio come nome SPN**  
  
Come nome SPN è possibile utilizzare gli account di servizio, specificati mediante l'attributo di connessione per l'autenticazione Kerberos nei formati seguenti:  
  
-   **username@domain** o **dominio\nomeutente** per un account utente di dominio  
  
-   **computer$@domain** o **host\FQDN** per un account di dominio di computer, ad esempio Sistema locale o NETWORK SERVICES.  
  
Per determinare il metodo di autenticazione di una connessione, eseguire la query seguente.  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> Impostazioni di autenticazione predefinite  
 Nella tabella seguente vengono descritte le impostazioni di autenticazione predefinite utilizzate in base agli scenari di registrazione del nome SPN.  
  
|Scenario|Metodo di autenticazione|  
|--------------|---------------------------|  
|Viene eseguito il mapping del nome SPN all'account di dominio, all'account virtuale, all'account dei servizi gestiti (MSA) o all'account predefinito corretto. ad esempio sistema locale o NETWORK SERVICE.|Le connessioni locali utilizzano l'autenticazione NTLM, mentre quelle remote utilizzano l'autenticazione Kerberos.|  
|Il nome SPN è l'account di dominio, l'account virtuale, l'account dei servizi gestiti (MSA) o l'account predefinito corretto.|Le connessioni locali utilizzano l'autenticazione NTLM, mentre quelle remote utilizzano l'autenticazione Kerberos.|  
|Viene eseguito il mapping del nome SPN a un account di dominio, a un account virtuale, a un account dei servizi gestiti (MSA) o a un account predefinito non corretto.|Errore di autenticazione|  
|La ricerca del nome SPN ha esito negativo o non viene eseguito il mapping a un account di dominio, a un account virtuale, a un account dei servizi gestiti (MSA) o a un account predefinito non corretto, oppure non è un account di dominio, un account virtuale, un account dei servizi gestiti o un account predefinito corretto.|Le connessioni locali e remote utilizzano l'autenticazione NTLM.|  
  
> [!NOTE]  
> Con il termine corretto si intende che l'account per il quale è stato eseguito il mapping dal nome SPN registrato è quello usato per eseguire il servizio SQL Server.  
  
##  <a name="Comments"></a> Commenti  
 La connessione amministrativa dedicata (DAC) utilizza un nome di istanza basato sul nome SPN. Se tale nome è stato registrato in modo corretto, è possibile utilizzare l'autenticazione Kerberos con una connessione DAC. In alternativa, un utente può specificare il nome dell'account come nome SPN.  
  
 Se la registrazione del nome SPN ha esito negativo in fase di avvio, l'errore viene registrato nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la procedura di avvio continua.  
  
 Se l'annullamento del nome SPN non riesce in fase di arresto, l'errore viene registrato nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la procedura di arresto continua.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto per nomi SPN nelle connessioni client](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [Nomi SPN &#40;Service Principal Name&#41; nelle connessioni client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [Nomi SPN &#40;Service Principal Name&#41; nelle connessioni client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [Funzionalità di SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Gestire problemi di autenticazione Kerberos in un ambiente Reporting Services](https://technet.microsoft.com/library/ff679930.aspx)  
  
  
