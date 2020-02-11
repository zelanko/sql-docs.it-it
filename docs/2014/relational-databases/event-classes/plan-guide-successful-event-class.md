---
title: Classe di evento Plan Guide Successful | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Successful event class
ms.assetid: fecfbb6c-56c9-4db4-84d3-00d6e338355a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56157ce2c29a95d35198ab44835b50e45d7831a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62827204"
---
# <a name="plan-guide-successful-event-class"></a>Classe di evento Plan Guide Successful
  Questa classe di evento indica che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato correttamente creato un piano di esecuzione per una query o un batch contenente una guida di piano. L'evento viene generato quando vengono soddisfatte le condizioni seguenti:  
  
-   Il modulo o batch nella definizione della guida di piano corrisponde al batch o modulo in esecuzione.  
  
-   La query nella definizione della guida di piano corrisponde alla query in esecuzione.  
  
-   Gli hint nella definizione della guida di piano, incluso l'hint USE PLAN, vengono applicati correttamente alla query. Ovvero, il piano di query compilato soddisfa gli hint specificati.  
  
## <a name="plan-guide-successful-event-class-data-columns"></a>Colonne di dati della classe di evento Plan Guide Successful  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione anziché con il nome visualizzato del programma.|10|Sì|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Sì|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per un'istanza specificata non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]consente di visualizzare il nome del database se la colonna di dati ServerName viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Sì|  
|EventClass|`int`|Tipo di evento = 214.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|IsSystem|`int`|Indica se l'evento si è verificato in un processo di sistema o in un processo utente: 1 = sistema, 0 = utente.|60|Sì|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accesso di sicurezza [!INCLUDE[msCoName](../../includes/msconame-md.md)] di o credenziali di accesso di Windows nel\\formato dominio*nomeutente*).|11|Sì|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Tali informazioni sono disponibili nelle viste del catalogo [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) o [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) . Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Sì|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Sì|  
|ObjectID|`int`|ID oggetto del modulo in fase di compilazione quando viene applicata la guida di piano. Se la guida di piano non viene applicata a un modulo, questa colonna è impostata su NULL.|22|Sì|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Sì|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|TextData|`ntext`|Nome della guida di piano.|1|Sì|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Sì|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe di evento Plan Guide Unsuccessful](plan-guide-unsuccessful-event-class.md)   
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
