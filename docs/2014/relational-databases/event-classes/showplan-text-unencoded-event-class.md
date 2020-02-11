---
title: Classe di evento Showplan Text (Unencoded) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan Text (Unencoded) event class
ms.assetid: 0aad4563-8caf-4971-92af-55992bc5ff2c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd9f8c6ca62fdd9f9a856a19f3d27c2144073b52
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62650374"
---
# <a name="showplan-text-unencoded-event-class"></a>Showplan Text (Unencoded) - classe di evento
  La classe di evento Showplan Text (Unencoded) viene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generata quando esegue un'istruzione SQL. Questa classe di evento è analoga alla classe di evento Showplan Text, ma le informazioni sull'evento vengono formattate come stringa anziché come dati binari.  
  
 Le informazioni incluse sono un subset delle informazioni disponibili nelle classi di evento Showplan All, Showplan XML o Showplan XML.  
  
 Quando la classe di evento Showplan Text (Unencoded) viene inclusa in una traccia, è possibile che la quantità di overhead influisca negativamente in modo significativo sulle prestazioni. Showplan Text (Unencoded) genera una quantità di overhead inferiore rispetto alle altre classi di evento Showplan. Per ridurre al minimo la quantità di overhead generata, limitare l'utilizzo di questa classe di evento alle tracce che eseguono il monitoraggio di problemi specifici per periodi di tempo ridotti.  
  
## <a name="showplan-text-unencoded-event-class-data-columns"></a>Colonne di dati della classe di evento Showplan Text (Unencoded)  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Sì|  
|BinaryData|`image`|Valore binario che dipende dalla classe di evento acquisita nella traccia.|2|Sì|  
|ClientProcessID|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se tramite il client viene indicato l'ID del processo client.|9|Sì|  
|DatabaseID|`int`|ID del database specificato nell'istruzione USE *database* oppure il database predefinito se non è stata eseguita alcuna istruzione USE *database* per una determinata istanza. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]consente di visualizzare il nome del database se la colonna di dati ServerName viene acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Sì|  
|DatabaseName|`nvarchar`|Nome del database nel quale viene eseguita l'istruzione dell'utente.|35|Sì|  
|EventClass|`int`|Tipo di evento = 68.|27|No|  
|EventSequence|`int`|Sequenza di un determinato evento all'interno della richiesta.|51|No|  
|GroupID|`int`|ID del gruppo del carico di lavoro in cui viene generato l'evento di Traccia SQL.|66|Sì|  
|HostName|`nvarchar`|Nome del computer in cui viene eseguito il client. Questa colonna di dati viene popolata se il client fornisce il nome host. Per determinare il nome host, usare la funzione HOST_NAME.|8|Sì|  
|IntegerData|`int`|Valore integer che dipende dalla classe di evento acquisita nella traccia.|25|Sì|  
|IsSystem|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Sì|  
|LineNumber|`int`|Visualizza il numero della riga contenente l'errore.|5|Sì|  
|LoginName|`nvarchar`|Nome dell'account di accesso dell'utente (account di accesso di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows nel formato DOMINIO\nomeutente).|11|Sì|  
|LoginSid|`image`|ID di sicurezza (SID) dell'utente connesso. Queste informazioni sono disponibili nella vista del catalogo sys.server_principals. Il SID è univoco per ogni account di accesso nel server.|41|Sì|  
|NestLevel|`int`|Valore intero che rappresenta i dati restituiti da @@NESTLEVEL.|29|Sì|  
|NTDomainName|`nvarchar`|Dominio Windows di appartenenza dell'utente.|7|Sì|  
|NTUserName|`nvarchar`|Nome utente di Windows.|6|Sì|  
|ObjectID|`int`|ID dell'oggetto assegnato dal sistema.|22|Sì|  
|ObjectName|`nvarchar`|Nome dell'oggetto a cui si fa riferimento.|34|Sì|  
|ObjectType|`int`|Valore che rappresenta il tipo di oggetto coinvolto nell'evento. Questo valore corrisponde alla colonna type nella vista del catalogo sys.objects. Per i valori, vedere [Colonna ObjectType per gli eventi di traccia](objecttype-trace-event-column.md).|28|Sì|  
|RequestID|`int`|ID della richiesta contenente l'istruzione.|49|Sì|  
|ServerName|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|SessionLoginName|`nvarchar`|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, SessionLoginName indica Login1 e LoginName indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|SPID|`int`|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|StartTime|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|TextData|`ntext`|Valore di testo che dipende dalla classe di evento acquisita nella traccia.|1|Sì|  
|TransactionID|`bigint`|ID della transazione assegnato dal sistema.|4|Sì|  
|XactSequence|`bigint`|Token utilizzato per descrivere la transazione corrente.|50|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Guida di riferimento a operatori Showplan logici e fisici](../showplan-logical-and-physical-operators-reference.md)   
 [Showplan All-classe di evento](showplan-all-event-class.md)   
 [Showplan XML-classe di evento](showplan-xml-event-class.md)   
 [Classe di evento Showplan XML Statistics Profile](showplan-xml-statistics-profile-event-class.md)  
  
  
