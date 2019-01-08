---
title: Classe di evento QN:Parameter Table | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Parameter Table
ms.assetid: 292da1ed-4c7e-4bd2-9b84-b9ee09917724
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 395df605926f0ff4ddc30970cdcebce0f1d0c8fc
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349642"
---
# <a name="qnparameter-table-event-class"></a>Classe di evento QN:Parameter Table
  L'evento QN:Parameter table fornisce informazioni sulle operazioni necessarie per creare ed eliminare le tabelle interne in cui sono archiviate le informazioni sui parametri, nonché per mantenere i conteggi dei riferimenti corrispondenti. Questo evento indica inoltre l'attività interna per reimpostare il conteggio di utilizzi relativo a una tabella di parametri.  
  
## <a name="qnparameter-table-event-class-data-columns"></a>Colonne di dati della classe di evento QN:Parameter table  
  
|Colonna di dati|Tipo|Descrizione|Numero colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato dall'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita alcuna istruzione USE *database*. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] viene visualizzato il nome del database se la colonna di dati ServerName viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database in cui viene eseguita l'istruzione dell'utente.|35|Yes|  
|EventClass|`Int`|Tipo di evento = 200.|27|No|  
|EventSequence|`int`|Numero di sequenza dell'evento.|51|No|  
|EventSubClass|`nvarchar`|Tipo di sottoclasse di evento in cui sono disponibili informazioni aggiuntive su ogni classe di evento. Questa colonna può contenere i valori seguenti:<br /><br /> Tabella creata: Indica che nel database è stata creata una tabella di parametri.<br /><br /> Tentativo di eliminazione tabella: Indica che il database ha tentato di eliminare automaticamente una tabella di parametri inutilizzata per liberare risorse.<br /><br /> Tentativo di eliminazione tabella non riuscito: Indica che il database ha tentato di eliminare una tabella di parametri inutilizzata e che l'operazione ha avuto esito negativo. In [!INCLUDE[ssDE](../../includes/ssde-md.md)] verrà automaticamente ripianificata l'eliminazione della tabella di parametri per liberare risorse.<br /><br /> Tabella eliminata: Indica che il database ha eliminato correttamente una tabella di parametri.<br /><br /> Tabella aggiunta: Indica che per la tabella di parametri è stato attivato il pinning per l'utilizzo corrente mediante elaborazione interna.<br /><br /> Tabella unpinned: Indica che per la tabella di parametri è stato annullato il pinning. L'elaborazione interna non richiede più l'utilizzo della tabella.<br /><br /> Numero di utenti incrementato: Indica che il numero di sottoscrizioni di notifica delle query che fanno riferimento a una tabella di parametri è aumentato.<br /><br /> Numero di utenti ridotto: Indica che il numero di sottoscrizioni di notifica delle query che fanno riferimento a una tabella di parametri è diminuito.<br /><br /> Reimposta contatore LRU: Indica che il conteggio di utilizzi per la tabella di parametri è stato reimpostato.<br /><br /> Attività di pulizia avviata: Indica quando ha avuto inizio la pulizia per tutte le sottoscrizioni in questa tabella di parametri. In genere, questa operazione ha inizio all'avvio del database o all'eliminazione di una tabella sottostante le sottoscrizioni di questa tabella di parametri.<br /><br /> Fine attività di pulizia: Indica quando termina la pulizia per tutte le sottoscrizioni in questa tabella di parametri.|21|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente.<br /><br /> 0 = utente<br /><br /> 1 = sistema|60|No|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di Windows nel formato *DOMAIN*\\*Username*).|11|No|  
|LoginSID|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio di Windows a cui appartiene l'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Yes|  
|RequestID|`int`|Identificatore della richiesta contenente l'istruzione.|49|Yes|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio un'applicazione si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 ed esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica "Login1" e LoginName indica "Login2". In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|TextData|`ntext`|Restituisce un documento XML contenente informazioni specifiche per questo evento. Questo documento è conforme XML Schema disponibile nella pagina [Schema di eventi di SQL Server Profiler correlati alle notifiche delle query](https://go.microsoft.com/fwlink/?LinkId=63331) .|1|Yes|  
  
  
