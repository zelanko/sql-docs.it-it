---
title: Classe di evento Plan Guide Unsuccessful | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Unsuccessful event class
ms.assetid: ef9759f8-5613-4884-9257-86b609313f69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6ce753ceaa0cc0ee16b395918390a4402cf5f39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827384"
---
# <a name="plan-guide-unsuccessful-event-class"></a>Classe di evento Plan Guide Unsuccessful
  Questa classe di evento indica che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è stato possibile creare un piano di esecuzione per una query o un batch contenente una guida di piano. Il piano è stato invece compilato senza utilizzare la guida di piano. L'evento viene generato quando vengono soddisfatte le condizioni seguenti:  
  
-   Il modulo/batch nella definizione della guida di piano corrisponde al batch in esecuzione.  
  
-   La query nella definizione della guida di piano corrisponde alla query in esecuzione.  
  
-   Gli hint nella definizione della guida di piano, incluso l'hint USE PLAN, non vengono applicati correttamente alla query o batch. Quindi, il piano di query compilato non è in grado di applicare gli hint specificati e il piano viene compilato utilizzando la guida di piano.  
  
 Una guida di piano non valida può causare la generazione di questo evento. Convalidare la guida di piano usata dalla query o batch tramite la funzione [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) e correggere l'errore riportato da questa funzione.  
  
 Questo evento è incluso nel modello Tuning di [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] .  
  
## <a name="plan-guide-unsuccessful-event-class-data-columns"></a>Colonne di dati della classe di evento Plan Guide Unsuccessful  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione anziché con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per un'istanza specificata non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|EventClass|`int`|Tipo di evento = 218.|27|no|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento si è verificato in un processo di sistema o in un processo utente: 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\\*nomeutente*).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Tali informazioni sono disponibili nelle viste del catalogo [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) o [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID oggetto del modulo in fase di compilazione quando viene applicata la guida di piano. Se la guida di piano non viene applicata a un modulo, questa colonna è impostata su NULL.|22|Yes|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Yes|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Nome della guida di piano.|1|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe di evento Plan Guide Successful](plan-guide-successful-event-class.md)   
 [Eventi estesi](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
