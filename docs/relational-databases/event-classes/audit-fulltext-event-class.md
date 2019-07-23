---
title: Classe di evento Audit Fulltext | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 95e4c5fd-e16f-446e-b42b-105495a8f39a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d77321058cbe0a45bfa9ab168cf92ed9b1c3e8ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897597"
---
# <a name="audit-fulltext-event-class"></a>Classe di evento Audit Fulltext
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La classe di evento **Audit Fulltext** si verifica quando ci si connette con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e si comunica con il processo daemon di filtri full-text.  
  
## <a name="audit-fulltext-event-class-data-columns"></a>Colonne di dati della classe di evento Audit Fulltext  
  
|Nome colonna di dati|Tipo di dati|Descrizione|ID colonna|Filtrabile|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**Errore**|**int**|Numero di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se l'evento indica un errore.|31|Sì|  
|**EventSequence**|**int**|Sequenza di un determinato evento all'interno della richiesta.|51|no|  
|**EventSubClass**|**int**|Tipo di connessione utilizzato dall'account di accesso. 1 = Non in pool, 2 = In pool.|21|Sì|  
|**IsSystem**|**int**|Indica se l'evento è stato generato per un processo di sistema o un processo utente. 1 = sistema, 0 = utente.|60|Sì|  
|**SessionLoginName**|**nvarchar**|Nome dell'account di accesso dell'utente che ha avviato la sessione. Se ad esempio si stabilisce la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'account di accesso Login1 e si esegue un'istruzione con l'account di accesso Login2, **SessionLoginName** indica Login1 e **LoginName** indica Login2. In questa colonna sono visualizzati sia gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che quelli di Windows.|64|Sì|  
|**SPID**|**int**|ID della sessione in cui si è verificato l'evento.|12|Sì|  
|**StartTime**|**datetime**|Ora di inizio dell'evento, se disponibile.|14|Sì|  
|**Esito positivo**|**int**|1 = esito positivo. 0 = esito negativo. Ad esempio, il valore 1 indica che il controllo delle autorizzazioni ha avuto esito positivo e il valore 0 che il controllo ha avuto esito negativo.|23|Sì|  
|**TargetLoginName**|**int**|Per le azioni relative a un account di accesso (ad esempio l'aggiunta di un nuovo account di accesso), il nome dell'account di accesso specifico.|42|Sì|  
|**TargetLoginSid**|**int**|Per le azioni relative a un account di accesso (ad esempio l'aggiunta di un nuovo account di accesso), l'ID di sicurezza (SID) dell'account di accesso specifico.|43|Sì|  
|**TextData**|**ntext**|Informazioni in formato testo sull'evento full-text. In genere questo campo fornisce informazioni sulla connessione tra il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il processo daemon di filtri full-text|1|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
