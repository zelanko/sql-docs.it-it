---
title: Classe di evento Log File Auto Shrink | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Log File Auto Shrink event class
ms.assetid: 4bf82a13-9985-4f20-9ef8-0083f104d124
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eab2902600f26abfc0f714b231fcf1bb684f513b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62662215"
---
# <a name="log-file-auto-shrink-event-class"></a>Log File Auto Shrink - classe di evento
  La classe di evento **Log File Auto Shrink** indica che il file di log è stato compattato automaticamente. Questo evento non viene generato se il file di log viene compattato a causa di un'istruzione ALTER DATABASE esplicita.  
  
 Includere la classe di evento **Log File Auto Shrink** nelle tracce che consentono di monitorare la compattazione del file di log. Quando questa classe di evento viene inclusa in una traccia, la quantità di overhead è bassa, a meno che il file non venga compattato con una certa frequenza.  
  
## <a name="log-file-auto-shrink-event-class-data-columns"></a>Colonne di dati della classe di evento Log File Auto Shrink  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**ClientProcessID**|**Int**|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|**DatabaseID**|**int**|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**DatabaseName**|**nvarchar**|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|**Durata**|**bigint**|Periodo di tempo, in millisecondi, necessario per l'estensione del file.|13|Yes|  
|**EndTime**|**datetime**|Tempo necessario per il completamento di **Auto Shrink** per il file di log.|18|Yes|  
|**EventClass**|**int**|Tipo di evento = 95.|27|no|  
|**EventSequence**|**int**|Sequenza della classe di evento **CursorClose** nel batch.|51|no|  
|**Filename**|**nvarchar**|Nome logico del file esteso.|36|Yes|  
|**HostName**|**nvarchar**|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|**Int**|Numero di pagine da 8 kilobyte (KB) aggiunte al file per aumentarne le dimensioni.|25|Yes|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|**LoginName**|**nvarchar**|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|**LoginSid**|**image**|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo **sys.server_principals** . Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|**nvarchar**|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|**ServerName**|**nvarchar**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|no|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|**SPID**|**Int**|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
