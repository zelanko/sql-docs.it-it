---
title: Uso dell'autenticazione integrata | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ffaf0e89e1fdbd0a1722ad038ad9e360decf237
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305889"
---
# <a name="using-integrated-authentication"></a>Uso dell'autenticazione integrata
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS supporta le connessioni che usano l'autenticazione integrata Kerberos. Supporta il centro distribuzione chiavi di MIT Kerberos e può essere usato con GSSAPI (Generic Security Services Application Program Interface) e librerie Kerberos v5.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>Uso dell'autenticazione integrata per la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da un'applicazione ODBC  

È possibile abilitare l'autenticazione integrata di Kerberos specificando **Trusted_Connection = yes** nella stringa di connessione di **SQLDriverConnect** o **SQLConnect**. Ad esempio  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Quando ci si connette con un DSN, è anche possibile aggiungere **Trusted_Connection = yes** alla voce del DSN in `odbc.ini`.
  
Il `-E` opzione di `sqlcmd` e il `-T` opzione della `bcp` possono essere usati anche per specificare l'autenticazione integrata, vedere [ci si connette con **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) e[ La connessione con **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) per altre informazioni.

Assicurarsi che l'entità di sicurezza del client che esegue la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sia già stata autenticata con Kerberos KDC.
  
**ServerSPN** e **FailoverPartnerSPN** non sono supportati.  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Distribuzione di un Linux o macOS ODBC Driver applicazione progettata per l'esecuzione come servizio

Un amministratore di sistema può distribuire un'applicazione da eseguire come servizio che usa l'autenticazione Kerberos per connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
È necessario innanzitutto configurare Kerberos nel client e quindi verificare che l'applicazione possa usare le credenziali Kerberos dell'entità di sicurezza predefinita.

Assicurarsi di usare `kinit` o PAM (Pluggable Authentication Module) per ottenere e memorizzare nella cache il TGT per l'entità usata dalla connessione tramite uno dei metodi seguenti:  
  
-   Eseguire `kinit` specificando il nome di un'entità di sicurezza e la password.  
  
-   Eseguire `kinit` specificando il nome di un'entità di sicurezza e il percorso del file keytab contenente la chiave dell'entità creata da `ktutil`.  
  
-   Assicurarsi che l'accesso al sistema sia stato eseguito usando Kerberos PAM (Pluggable Authentication Module).

Quando un'applicazione viene eseguita come servizio, poiché le credenziali Kerberos hanno una scadenza per impostazione predefinita, rinnovare le credenziali per garantire una disponibilità continua del servizio. Il driver ODBC di non rinnovare le credenziali. Verificare che sia presente un `cron` processo o uno script che viene eseguito regolarmente per rinnovare le credenziali prima della scadenza. Per evitare di richiedere la password per ciascun rinnovo, è possibile usare un file keytab.  
  
La pagina relativa a[configurazione e uso di Kerberos](https://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) fornisce informazioni dettagliate sull'uso di Kerberos per i servizi in Linux.
  
## <a name="tracking-access-to-a-database"></a>Rilevamento dell'accesso a un database

Un amministratore di database può creare un itinerario di controllo di accesso a un database quando vengono usati account di sistema per accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con l'autenticazione integrata.  
  
L'accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa l'account di sistema e non vi è alcuna funzionalità in Linux per rappresentare il contesto di sicurezza. Sono pertanto necessari più dati per determinare l'utente.
  
Per controllare le attività in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per conto di utenti diversi dagli account di sistema, è necessario che l'applicazione usi [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE AS**.  
  
Per migliorare le prestazioni, l'applicazione può usare pool di connessioni con autenticazione integrata e controllo. Tuttavia, la combinazione di pool di connessioni, autenticazione integrata e controllo crea un rischio per la sicurezza perché il programma di gestione dei driver unixODBC consente a utenti diversi di riutilizzare le connessioni in pool. Per altre informazioni, vedere la pagina relativa ai [pool di connessioni ODBC](http://www.unixodbc.org/doc/conn_pool.html).  

Prima del riutilizzo, è necessario che l'applicazione reimposti le connessioni in pool eseguendo `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Uso di Active Directory per la gestione delle identità utente

Non è necessario che l'amministratore di sistema dell'applicazione gestisca più set di credenziali di accesso per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È possibile configurare Active Directory come centro distribuzione chiavi (KDC) per l'autenticazione integrata. Visualizzare [Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos) per altre informazioni.

## <a name="using-linked-server-and-distributed-queries"></a>Uso di un server collegato e di query distribuite

Gli sviluppatori possono distribuire un'applicazione che usa un server collegato o query distribuite senza che l'amministratore di database gestisca più set di credenziali SQL. In questo caso, è necessario che lo sviluppatore configuri l'applicazione per l'uso dell'autenticazione integrata:  
  
-   L'utente accede a un computer client ed esegue l'autenticazione nel server applicazioni.  
  
-   Il server applicazioni esegue l'autenticazione come database diverso e si connette a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue l'autenticazione come utente di database in un altro database ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
Dopo aver configurato l'autenticazione integrata, le credenziali vengono passate al server collegato.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Autenticazione integrata e sqlcmd
Per accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con l'autenticazione integrata, usare l'opzione `-E` di `sqlcmd`. Verificare che l'account che esegue `sqlcmd` è associato all'entità client Kerberos predefinita.

## <a name="integrated-authentication-and-bcp"></a>Autenticazione integrata e bcp
Per accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con l'autenticazione integrata, usare l'opzione `-T` di `bcp`. Verificare che l'account che esegue `bcp` è associato all'entità client Kerberos predefinita. 
  
È possibile usare `-T` con il `-U` o `-P` opzione.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>Sintassi supportata per un nome SPN registrato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

Di seguito è indicata la sintassi usata per i nomi SPN nella stringa di connessione o negli attributi di connessione:  

|Sintassi|Descrizione|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|Nome SPN predefinito generato dal provider quando si usa il protocollo TCP. *port* è un numero di porta TCP. *fqdn* è un nome di dominio completo.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Autenticazione di un computer Linux o macOS con Active Directory

Per configurare Kerberos, l'immissione di dati di `krb5.conf` file. `krb5.conf` le novità `/etc/` ma è possibile fare riferimento a un altro file usando la sintassi, ad esempio `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. Di seguito è riportato un file `krb5.conf` di esempio:  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
Se il computer Linux o macOS è configurato per l'utilizzo di Dynamic Host Configuration Protocol (DHCP) con un server DHCP di Windows che fornisce i server DNS da usare, è possibile usare **dns_lookup_kdc = true**. A questo punto, è possibile usare Kerberos per accedere al dominio eseguendo il comando `kinit alias@YYYY.CORP.CONTOSO.COM`. I parametri passati a `kinit` fanno distinzione tra maiuscole e le [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] computer configurato come nel dominio deve disporre di tale utente `alias@YYYY.CORP.CONTOSO.COM` aggiunti per account di accesso. È ora possibile usare connessioni trusted (**Trusted_Connection=YES** in una stringa di connessione, **bcp -T** o **sqlcmd -E**).  
  
L'ora nel computer Linux o macOS e l'ora nel centro di distribuzione chiavi (KDC) Kerberos, devono essere simili. Verificare che l'ora di sistema sia impostata correttamente, ad esempio usando il protocollo NTP (Network Time Protocol).  

Se l'autenticazione Kerberos non riesce, il driver ODBC in Linux o macOS non usa l'autenticazione NTLM.  

Per altre informazioni sull'autenticazione computer Linux o macOS con Active Directory, vedere [autenticare client Linux con Active Directory](https://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) e [le procedure consigliate per l'integrazione di OS X con Active Directory](https://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Per altre informazioni sulla configurazione di Kerberos, vedere la [documentazione relativa a Kerberos MIT](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Vedere anche  
[Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes.md)

[Uso di Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)
