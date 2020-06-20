---
title: Classe di evento QN:Dynamics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Dynamics
ms.assetid: 3c1ffa0c-c9e5-40a6-a26b-28339f60ebc3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6a55c2b2a2392cf5d9993f4bfdea8969e4f4d23f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85028889"
---
# <a name="qndynamics-event-class"></a>Classe di evento QN:Dynamics
  La classe di evento QN:Dynamics fornisce informazioni sull'attività in background eseguita dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] per supportare le notifiche delle query. All'interno di [!INCLUDE[ssDE](../../includes/ssde-md.md)], un thread in background esegue il monitoraggio dei timeout di sottoscrizione, delle sottoscrizioni in attesa di attivazione e dell'eliminazione delle tabelle di parametri.  
  
## <a name="qndynamics-event-class-data-columns"></a>Colonne dati della classe di evento QN:Dynamics  
  
|Colonna di dati|Type|Descrizione|Numero di colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Sì|  
|DatabaseID|`int`|ID del database specificato dall'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita alcuna istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] viene visualizzato il nome del database se la colonna di dati ServerName viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|DatabaseName|`nvarchar`|Nome del database in cui viene eseguita l'istruzione dell'utente.|35|Sì|  
|EventClass|`int`|Tipo di evento = 202.|27|No|  
|EventSequence|`int`|Numero di sequenza dell'evento.|51|No|  
|EventSubClass|`nvarchar`|Tipo di sottoclasse di evento in cui sono disponibili informazioni aggiuntive su ogni classe di evento. Questa colonna può contenere i valori seguenti:<br /><br /> Clock Run started: indica che il thread in background nell'oggetto [!INCLUDE[ssDE](../../includes/ssde-md.md)] che pianifica le tabelle di parametri scadute per la pulizia è stato avviato.<br /><br /> Clock Run finished: indica che il thread in background nell'oggetto [!INCLUDE[ssDE](../../includes/ssde-md.md)] che pianifica le tabelle di parametri scadute per la pulizia è terminato.<br /><br /> Master cleanup task started: Indica quando viene avviata la pulizia (Garbage Collection) per rimuovere i dati di sottoscrizione di notifica delle query scaduti.<br /><br /> Master cleanup task finished: Indica quando termina la pulizia (Garbage Collection) per rimuovere i dati di sottoscrizione di notifica delle query scaduti.<br /><br /> Master Cleanup Task ignorato: indica che l'oggetto [!INCLUDE[ssDE](../../includes/ssde-md.md)] non ha eseguito la pulizia (Garbage Collection) per rimuovere i dati di sottoscrizione di notifica delle query scaduti.|21|Sì|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Sì|  
|HostName|`nvarchar`|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente.<br /><br /> 0 = utente<br /><br /> 1 = sistema|60|No|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sicurezza di o credenziali di accesso di Windows nel formato *DOMINIO\nomeutente*).|11|No|  
|LoginSID|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|NTDomainName|`nvarchar`|Dominio di Windows a cui appartiene l'utente.|7|Sì|  
|NTUserName|`nvarchar`|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Sì|  
|RequestID|`int`|Identificatore della richiesta contenente l'istruzione.|49|Sì|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio un'applicazione si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 ed esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica "Login1" e LoginName indica "Login2". In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|TextData|`ntext`|Restituisce un documento XML contenente informazioni specifiche per questo evento. Questo documento è conforme XML Schema disponibile nella pagina [Schema di eventi di SQL Server Profiler correlati alle notifiche delle query](https://go.microsoft.com/fwlink/?LinkId=63331) .|1|Sì|  
  
  
