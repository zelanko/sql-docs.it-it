---
title: 'Progress Report: Classe di evento online Index Operation | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a09b4c8f6f6c600ac7b14faf35966a82c0b6905
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756123"
---
# <a name="progress-report-online-index-operation-event-class"></a>Progress Report: Classe di evento Online Index Operation
  Progress Report: Classe di evento operazione sugli indici online indica lo stato di un'operazione di compilazione indice online durante il processo di compilazione è in esecuzione.  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>Progress Report: Colonne dati della classe evento operazione sugli indici online  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|BigintData1|`bigint`|Numero di righe inserite.|52|Yes|  
|BigintData2|`bigint`|0 = piano seriale; altrimenti, ID del thread durante l'esecuzione parallela.|53|Yes|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Yes|  
|DatabaseID|`int`|ID del database specificato nell'istruzione di *database* USE oppure il database predefinito se per un'istanza specifica l'istruzione di *database* USE non è stata eseguita. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati ServerName è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Yes|  
|Duration|`bigint`|Durata dell'evento in microsecondi.|13|Yes|  
|EndTime|`datetime`|Ora del completamento dell'operazione di creazione dell'indice online.|15|Yes|  
|EventClass|`int`|Tipo di evento = 190.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|EventSubClass|`int`|Tipo di sottoclasse di evento.<br /><br /> 1 = Avvio<br /><br /> 2 = Inizio esecuzione fase 1<br /><br /> 3 = Fine esecuzione fase 1<br /><br /> 4 = Inizio esecuzione fase 2<br /><br /> 5 = Fine esecuzione fase 2<br /><br /> 6 = Conteggio righe inserite<br /><br /> 7 = Fine<br /><br /> Fase 1 si riferisce all'oggetto di base (indice cluster o heap) o indica se l'operazione sull'indice include solo un indice non cluster. Fase 2 viene utilizzata quando l'operazione di compilazione di un indice include sia la ricompilazione originale che gli indici non cluster aggiuntivi.  Ad esempio, se un oggetto ha un indice cluster e molti indici non cluster, con 'Ricompila tutto' verrebbero ricompilati tutti gli indici. L'oggetto di base (l'indice cluster) viene ricompilato nella fase 1 e tutti gli indici non cluster vengono ricompilati quindi nella fase 2.|21|Yes|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Yes|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|IndexID|`int`|ID dell'indice dell'oggetto interessato dall'evento.|24|Yes|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Yes|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Yes|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Yes|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Yes|  
|ObjectID|`int`|ID dell'oggetto assegnato dal sistema.|22|Yes|  
|ObjectName|`nvarchar`|Nome dell'oggetto a cui si fa riferimento.|34|Yes|  
|PartitionId|`bigint`|ID della partizione da compilare.|65|Yes|  
|PartitionNumber|`int`|Numero ordinario della partizione da compilare.|25|Yes|  
|ssSqlProfiler|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Yes|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Yes|  
|StartTime|`datetime`|Ora di inizio dell'evento.|14|Yes|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
