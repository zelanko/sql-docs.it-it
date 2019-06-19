---
title: Protezione delle applicazioni di servizi desktop remoto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b2afe6074f115c1d9770251c51e6288e9d92ee3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699341"
---
# <a name="securing-rds-applications"></a>Sicurezza delle applicazioni RDS
Questo argomento vengono fornite informazioni sulla sicurezza per Servizi Desktop remoto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Problemi di sicurezza di Microsoft Internet Explorer  
 Con nuovi miglioramenti della sicurezza aggiunti per Microsoft Internet Explorer, alcuni oggetti ADO e servizi desktop remoto sono limitate a in esecuzione solo in un ambiente in modalità "sicuro". Ciò richiede che si è a conoscenza di questi problemi, tra cui diverse zone, i livelli di sicurezza, comportamento restrittivo, operazioni non sicure e le impostazioni di sicurezza personalizzate.  
  
## <a name="security-and-your-web-server"></a>Sicurezza e il Server Web  
 Se si usa la [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) dell'oggetto nel server Web Internet, è necessario ricordare che tale condizione crea un potenziale rischio di sicurezza. Gli utenti esterni che ottengono il nome di origine dati valido (DSN), ID utente e le informazioni sulla password è stato possibile scrivere le pagine per l'invio di tutte le query all'origine dati. Se si desidera un accesso più limitato a un'origine dati, è un'opzione per annullare la registrazione ed eliminare le **RDSServer** (msadcf) dell'oggetto e utilizzare invece oggetti business personalizzati con le query a livello di codice.  
  
 Per altre informazioni sulle implicazioni di sicurezza di utilizzo dell'oggetto RDSServer, vedere il bollettino sulla sicurezza di Microsoft MS99-025 nel sito Web Microsoft Security.  
  
## <a name="client-impersonation-and-security"></a>Sicurezza e la rappresentazione del client  
 Se il **l'autenticazione della Password** per il server Web IIS viene impostata per l'autenticazione di Windows NT Challenge/Response (per Windows NT 4.0) o per l'autenticazione integrata Windows (per Windows 2000), quindi sono oggetti business viene richiamato nel contesto di sicurezza del client. Si tratta di una nuova funzionalità di 1.5 di servizi desktop remoto che consente la rappresentazione del Client su HTTP. Quando si utilizza questa modalità, l'accesso al server Web (IIS) non è anonimo, ma usa l'ID utente e password di cui è in esecuzione nel computer client. Se il DSN ODBC sono configurati per utilizzare la connessione Trusted, quindi accedere ai database, ad esempio SQL Server, avviene anche nel contesto di sicurezza del client. Ma funziona solo se il database si trova nello stesso computer IIS; le credenziali del client non possono essere trasferite a un altro computer.  
  
 Ad esempio, un client, John Doe, con ID = "LucaD" e la password = "segreto" è connesso a un computer client. Peter esegue un'applicazione basata su browser che richiede l'accesso di **RDSServer** oggetto per creare un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) eseguendo una query SQL sul computer "MyServer" che esegue IIS. MyServer, un sistema che esegue Windows NT Server 4.0, è configurato per usare l'autenticazione di Windows NT Challenge/Response, il DSN di ODBC è "Usa connessione Trusted" selezionato e il server contiene anche l'origine dati SQL Server. Quando viene ricevuta una richiesta sul server Web, chiede client per l'ID utente e password. Di conseguenza, la richiesta viene registrata nel server MyServer come provenienti da "LucaD" o "Segreto" anziché da IUSER_MyServer (ovvero l'impostazione predefinita al termine dell'autenticazione di Password anonimi su). Analogamente, quando si accede a SQL Server, "LucaD" / "Segreto" viene utilizzato.  
  
 Di conseguenza, la modalità di autenticazione IIS Windows NT Challenge/Response consente pagine HTML da creare senza che venga richiesta in modo esplicito per le informazioni di ID e la password utente necessarie per accedere al database utente. Se fosse utilizzata l'autenticazione di base di IIS, quindi questa anche potrebbe essere necessaria.  
  
## <a name="password-authentication"></a>Autenticazione della password  
 Servizi Desktop remoto può comunicare con un server Web IIS in esecuzione in una delle tre modalità di autenticazione della Password: NT Challenge/Response, Basic o Anonymous authentication (nota come autenticazione di Windows integrata in Windows 2000). Queste impostazioni definiscono come un server Web controlla l'accesso attraverso di esso, ad esempio richiedere che un computer client dispone di privilegi di accesso esplicite nel server Web NT.


