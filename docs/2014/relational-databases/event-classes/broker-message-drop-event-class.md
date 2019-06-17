---
title: Classe di evento Broker:Message Undeliverable | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Message Drop event class
- Broker:Message Undeliverable event class
ms.assetid: f532b7c9-ca34-4bac-8dc3-53f9895fd6af
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1aadd84d42f797026323023b0cf5be27d01d693
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663968"
---
# <a name="brokermessage-undeliverable-event-class"></a>Classe di evento Broker:Message Undeliverable
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Message Undeliverable** quando Service Broker non è in grado di trattenere un messaggio ricevuto che avrebbe dovuto essere recapitato a un servizio dell'istanza. Per i messaggi che avrebbero dovuto essere inoltrati, vedere [Classe di evento Broker:Forwarded Message Dropped](broker-forwarded-message-dropped-event-class.md).  
  
## <a name="brokermessage-undeliverable-event-class-data-columns"></a>Colonne di dati della classe di evento Broker:Message Undeliverable  
  
|Colonna di dati|Type|Descrizione|Numero colonna|Filtrabile|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**Application Name**|`nvarchar`|Nome dell'applicazione client in cui è stata creata la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa colonna viene popolata con i valori passati dall'applicazione e non con il nome visualizzato del programma.|10|Yes|  
|**BigintData1**|`bigint`|Numero di sequenza del messaggio non recapitabile.|52|No|  
|**BigintData2**|`bigint`|Numero di sequenza dell'ultimo messaggio riconosciuto correttamente.|53|No|  
|**ClientProcessID**|`int`|ID assegnato dal computer host al processo in cui è in esecuzione l'applicazione client. Questa colonna di dati viene popolata se l'ID del processo client viene fornito dal client.|9|Yes|  
|**DatabaseID**|`int`|ID del database specificato nell'istruzione USE *database* oppure ID del database predefinito, se per una determinata istanza non viene eseguita un'istruzione USE *database* . [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] visualizza il nome del database se la colonna di dati **ServerName** è acquisita nella traccia e il server è disponibile. Determinare il valore per un database utilizzando la funzione DB_ID.|3|Yes|  
|**Errore**|`int`|Numero di ID del messaggio in **sys.messages** relativo al testo dell'evento.|31|No|  
|**EventClass**|`int`|Tipo di classe di evento acquisita. Sempre **160** per **Broker:MessageUndeliverable**.|27|No|  
|**EventSequence**|`int`|Numero di sequenza dell'evento.|51|no|  
|**EventSubClass**|`nvarchar`|Indica se il messaggio non recapitabile è un messaggio in sequenza. È possibile specificare uno dei due valori seguenti:<br /><br /> **Messaggio in sequenza**. Il messaggio non recapitabile è un messaggio in sequenza.<br /><br /> **Messaggio non in sequenza**. Il messaggio non recapitabile non è un messaggio in sequenza.|21|Yes|  
|**GUID**|`uniqueidentifier`|ID della conversazione a cui appartiene il messaggio non recapitabile. Questo identificatore viene trasmesso come parte del messaggio e viene condiviso da entrambi i lati della conversazione.|54|No|  
|**HostName**|`nvarchar`|Nome del computer in cui è in esecuzione il client. Questa colonna di dati viene popolata se il nome host viene fornito dal client. Per determinare il nome host, usare la funzione HOST_NAME.|8|Yes|  
|**IntegerData**|`int`|Numero di frammento del messaggio non recapitabile.|25|No|  
|**IntegerData2**|`int`|Numero di frammento riconosciuto dal messaggio non recapitabile.|55|no|  
|**IsSystem**|`int`|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|no|  
|**LoginName**|`nvarchar`|Nome dell'account di accesso dell'utente (account di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenziali di accesso di Windows nel formato DOMINIO\nomeutente).|11|no|  
|**LoginSid**|`image`|ID di sicurezza (SID) dell'utente connesso. Il SID è univoco per ogni account di accesso nel server.|41|Yes|  
|**NTDomainName**|`nvarchar`|Dominio di Windows a cui appartiene l'utente.|7|Yes|  
|**NTUserName**|`nvarchar`|Nome dell'utente proprietario della connessione che ha generato questo evento.|6|Yes|  
|**ObjectName**|`nvarchar`|Handle di conversazione del dialogo.|34|No|  
|**RoleName**|`nvarchar`|Ruolo dell'handle di conversazione. I valori possibili sono **initiator** o **target**.|38|No|  
|**ServerName**|`nvarchar`|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tracciata.|26|No|  
|**Severity**|`int`|Numero di gravità per il testo dell'evento.|29|no|  
|**SPID**|`int`|ID del processo server assegnato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al processo associato al client.|12|Yes|  
|**StartTime**|`datetime`|Ora di inizio dell'evento, se disponibile.|14|Yes|  
|**Stato**|`int`|Indica la posizione che ha generato l'evento all'interno del codice sorgente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni punto che può generare questo evento è contraddistinto da un codice di stato diverso. Questo codice di stato consente al supporto tecnico Microsoft di individuare la posizione in cui è stato generato l'evento.|30|No|  
|**TextData**|`ntext`|Motivo per cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è riuscito a recapitare il messaggio.|1|Yes|  
|**TransactionID**|`bigint`|ID della transazione assegnato dal sistema.|4|No|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
