---
title: Classe di evento Audit Broker Login | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Broker Login event class
ms.assetid: af9b1153-2791-40ef-a95c-50923cd0cc97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de23ecd1201d7ce0e24638cf9e64c63cb782face
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912106"
---
# <a name="audit-broker-login-event-class"></a>Audit Broker Login - classe di evento
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un evento **Audit Broker Login** per indicare i messaggi di controllo correlati alla sicurezza del trasporto di Service Broker.  
  
## <a name="audit-broker-login-event-class-data-columns"></a>Colonne di dati della classe di evento Audit Broker Login  
  
|Colonna di dati|Type|Descrizione|Numero colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Non utilizzata per questa classe di evento.|10|Yes|  
|**ClientProcessID**|**int**|Non utilizzata per questa classe di evento.|9|Yes|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**EventClass**|**int**|Tipo di classe di evento acquisita. Per **Audit Broker Login** corrisponde sempre a **159**.|27|No|  
|**EventSequence**|**int**|Numero di sequenza dell'evento.|51|No|  
|**EventSubClass**|**int**|Tipo di sottoclasse di evento in cui sono disponibili informazioni aggiuntive su ogni classe di evento. Nella tabella seguente sono elencati i valori di sottoclasse per questo evento.|21|Yes|  
|**FileName**|**nvarchar**|Livello di autenticazione dell'istanza remota di Service Broker. Metodo di autenticazione supportato configurato nell'endpoint dell'istanza remota di Service Broker. Se è disponibile più di un metodo, l'endpoint di accettazione (destinazione) determina quale metodo viene utilizzato per primo. I valori possibili sono:<br /><br /> **None**. Non è configurato alcun metodo di autenticazione.<br /><br /> **NTLM**. Richiede un'autenticazione NTLM.<br /><br /> **KERBEROS**. Richiede un'autenticazione Kerberos.<br /><br /> **NEGOTIATE**. Il metodo di autenticazione viene negoziato da Windows.<br /><br /> **CERTIFICATE**. Richiede il certificato configurato per l'endpoint, archiviato nel database **master** .<br /><br /> **NTLM, CERTIFICATE**. Accetta l'autenticazione NTLM o basata sul certificato SSL.<br /><br /> **KERBEROS, CERTIFICATE**. Accetta l'autenticazione Kerberos o basata sul certificato dell'endpoint.<br /><br /> **NEGOTIATE, CERTIFICATE**. Il metodo di autenticazione viene negoziato da Windows oppure per l'autenticazione può essere utilizzato un certificato dell'endpoint.<br /><br /> **CERTIFICATE, NTLM**. Accetta un certificato dell'endpoint o un'autenticazione NTLM.<br /><br /> **CERTIFICATE, KERBEROS**. Accetta il certificato di un endpoint o l'autenticazione Kerberos.<br /><br /> **CERTIFICATE, NEGOTIATE**. Accetta il certificato di un endpoint, oppure il metodo di autenticazione è negoziato da Windows.|36|no|  
|**HostName**|**nvarchar**|Non utilizzata per questa classe di evento.|8|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|No|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio di Windows a cui appartiene l'utente.|7|Yes|  
|**NTUserName**|**nvarchar**|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Yes|  
|**ObjectName**|**nvarchar**|La stringa di connessione utilizzata per questa connessione.|34|no|  
|**OwnerName**|**nvarchar**|Metodo di autenticazione supportato configurato nell'endpoint dell'istanza locale di Service Broker. Se è disponibile più di un metodo, l'endpoint di accettazione (destinazione) determina quale metodo viene utilizzato per primo. I valori possibili sono:<br /><br /> **None**. Non è configurato alcun metodo di autenticazione.<br /><br /> **NTLM**. Richiede un'autenticazione NTLM.<br /><br /> **KERBEROS**. Richiede un'autenticazione Kerberos.<br /><br /> **NEGOTIATE**. Il metodo di autenticazione viene negoziato da Windows.<br /><br /> **CERTIFICATE**. Richiede il certificato configurato per l'endpoint, archiviato nel database **master** .<br /><br /> **NTLM, CERTIFICATE**. Accetta l'autenticazione NTLM o basata sul certificato SSL.<br /><br /> **KERBEROS, CERTIFICATE**. Accetta l'autenticazione Kerberos o basata sul certificato dell'endpoint.<br /><br /> **NEGOTIATE, CERTIFICATE**. Il metodo di autenticazione viene negoziato da Windows oppure per l'autenticazione può essere utilizzato un certificato dell'endpoint.<br /><br /> **CERTIFICATE, NTLM**. Accetta il certificato di un endpoint o l'autenticazione NTLM.<br /><br /> **CERTIFICATE, KERBEROS**. Accetta il certificato di un endpoint o l'autenticazione Kerberos.<br /><br /> **CERTIFICATE, NEGOTIATE**. Accetta il certificato di un endpoint, oppure il metodo di autenticazione è negoziato da Windows.|37|No|  
|**ProviderName**|**nvarchar**|Metodo di autenticazione utilizzato per la connessione.|46|No|  
|**RoleName**|**nvarchar**|Ruolo della connessione. I valori possibili sono **initiator** o **target**.|38|No|  
|**ServerName**|**nvarchar**|Nome dell'istanza di SQL Server tracciata.|26|No|  
|**SPID**|**int**|ID del processo server assegnato da SQL Server al processo associato al client.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**State**|**int**|Indica il punto del codice sorgente di SQL Server che ha generato l'evento. Ogni punto che può generare questo evento è contraddistinto da un codice di stato diverso. Questo codice di stato consente al supporto tecnico Microsoft di individuare la posizione in cui è stato generato l'evento.|30|no|  
|**TargetUserName**|**nvarchar**|Stato di accesso. I possibili valori sono i seguenti:<br /><br /> INITIAL<br /><br /> WAIT LOGIN NEGOTIATE<br /><br /> ONE ISC<br /><br /> ONE ASC<br /><br /> TWO ISC<br /><br /> TWO ASC<br /><br /> WAIT ISC Confirm<br /><br /> WAIT ASC Confirm<br /><br /> WAIT REJECT<br /><br /> WAIT PRE-MASTER SECRET<br /><br /> WAIT VALIDATION<br /><br /> WAIT ARBITRATION<br /><br /> ONLINE<br /><br /> error<br /><br /> **Nota** ISC = Initiate Security Context. ASC = Accept Security Context.|39|no|  
|**TransactionID**|**bigint**|ID della transazione assegnato dal sistema.|4|no|  
  
 Nella tabella seguente sono elencati i valori di sottoclasse per questa classe di evento.  
  
|ID|Sottoclasse|Descrizione|  
|--------|--------------|-----------------|  
|1|Login Success|L'evento Login Success indica che la procedura di accesso dell'istanza di Service Broker adiacente ha avuto esito positivo.|  
|2|Login Protocol Error|L'evento Login Protocol Error indica che Service Broker riceve un messaggio in formato corretto, ma non valido per lo stato attuale della procedura di accesso. Questo messaggio potrebbe essere andato perduto o potrebbe essere stato inviato fuori sequenza.|  
|3|Message Format Error|L'evento Message Format Error indica che Service Broker ha ricevuto un messaggio in un formato non previsto. È possibile che il messaggio sia danneggiato oppure che un programma diverso da SQL Server stia inviando messaggi alla porta utilizzata da Service Broker.|  
|4|Negotiate Failure|L'evento Negotiate Failure indica che l'istanza locale e l'istanza remota di Service Broker supportano livelli di autenticazione che si escludono a vicenda.|  
|5|Authentication Failure|L'evento Authentication Failure indica che Service Broker non può eseguire l'autenticazione della connessione a causa di un errore. Per l'autenticazione di Windows, questo evento indica che Service Broker non può utilizzare l'autenticazione di Windows. Per l'autenticazione basata sui certificati, questo evento indica che Service Broker non può accedere al certificato.|  
|6|Authorization Failure|L'evento Authorization Failure indica che Service Broker ha negato l'autorizzazione per la connessione. Per l'autenticazione di Windows, questo evento segnala che l'ID di sicurezza per la connessione non corrisponde a un utente del database. Per l'autenticazione basata sui certificati, questo evento indica che la chiave pubblica recapitata nel messaggio non corrisponde a un certificato nel database.|  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
