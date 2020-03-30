---
title: Trigger LOGON | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68058625"
---
# <a name="logon-triggers"></a>Trigger LOGON
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  I trigger LOGON consentono di attivare stored procedure in risposta a un evento LOGON generato quando viene stabilita una sessione utente a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I trigger LOGON vengono attivati dopo il completamento della fase di autenticazione della procedura di accesso, ma prima che la sessione utente venga effettivamente stabilita. Per questo motivo, tutti i messaggi generati all'interno del trigger che verrebbero normalmente visualizzati all'utente, come i messaggi di errore e i messaggi dall'istruzione PRINT, vengono invece indirizzati al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I trigger LOGON non vengono attivati in caso di esito negativo dell'autenticazione.  
  
 È possibile utilizzare i trigger LOGON per controllare e gestire le sessioni server, ad esempio tenendo traccia delle attività di accesso, limitando gli accessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o limitando il numero di sessioni per uno specifico account di accesso. Nel codice seguente, ad esempio, il trigger LOGON nega i tentativi di accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguiti dall'account di accesso *login_test* se esistono già tre sessioni utente in esecuzione create da tale account di accesso.  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 Si noti che l'evento LOGON corrisponde all'evento di Traccia SQL AUDIT_LOGIN, che può essere usato nelle [notifiche di eventi](../../relational-databases/service-broker/event-notifications.md). La principale differenza tra i trigger e le notifiche di eventi è il fatto che i trigger vengono attivati in modo sincrono rispetto agli eventi, mentre le notifiche di eventi sono asincrone. Ciò significa, ad esempio, che se si desidera arrestare l'attivazione di una sessione è necessario utilizzare un trigger LOGON. Non è possibile utilizzare una notifica di evento per un evento AUDIT_LOGIN a tale scopo.  
  
## <a name="specifying-first-and-last-trigger"></a>Impostazione del primo e ultimo trigger  
 È possibile definire più trigger per l'evento LOGON. Uno qualsiasi di questi trigger può essere designato come primo o ultimo trigger da attivare per un evento usando la stored procedure di sistema [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non garantisce l'ordine di esecuzione dei trigger rimanenti.  
  
## <a name="managing-transactions"></a>Gestione delle transazioni  
 Prima che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attivi un trigger LOGON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una transazione implicita indipendente da qualsiasi altra transazione utente. Per questo motivo, quando viene attivato il primo trigger LOGON il numero di transazioni è 1 e al termine dell'esecuzione di tutti i trigger LOGON viene eseguito il commit della transazione. Come per tutti gli altri tipi di trigger, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un errore se l'esecuzione di un trigger LOGON viene completata con un numero di transazioni pari a 0. L'istruzione ROLLBACK TRANSACTION reimposta il numero di transazioni su 0, anche se viene eseguita all'interno di una transazione nidificata. L'istruzione COMMIT TRANSACTION potrebbe ridurre il numero di transazioni a 0. È pertanto consigliabile evitare l'esecuzione di istruzioni COMMIT TRANSACTION all'interno di trigger LOGON.  
  
 Tenere presenti le considerazioni seguenti per l'utilizzo di un'istruzione ROLLBACK TRANSACTION all'interno di trigger LOGON:  
  
-   Viene eseguito il rollback di qualsiasi modifica dei dati eseguita fino al punto dell'istruzione ROLLBACK TRANSACTION. Sono incluse le modifiche apportate dal trigger corrente e quelle apportate da trigger precedenti eseguiti sullo stesso evento. Gli eventuali trigger rimanenti per l'evento specifico non vengono eseguiti.  
  
-   Il trigger corrente continua l'esecuzione delle istruzioni rimanenti successive all'istruzione ROLLBACK. Se tali istruzioni modificano i dati, non viene eseguito il rollback delle modifiche eseguite.  
  
 Non viene stabilita una sessione utente se si verifica una della condizioni seguenti durante l'esecuzione di un trigger per un evento LOGON:  
  
-   Viene eseguito il rollback della transazione implicita originale o la transazione ha esito negativo.  
  
-   Viene generato un errore con gravità maggiore di 20 all'interno del corpo del trigger.  
  
## <a name="disabling-a-logon-trigger"></a>Disabilitazione di un trigger di accesso  
 Un trigger di accesso può impedire le connessioni al [!INCLUDE[ssDE](../../includes/ssde-md.md)] per tutti gli utenti, inclusi i membri del ruolo predefinito del server **sysadmin** . Quando un trigger di accesso impedisce le connessioni, i membri del ruolo predefinito del server **sysadmin** possono connettersi tramite la connessione amministrativa dedicata o avviando il [!INCLUDE[ssDE](../../includes/ssde-md.md)] nella modalità di configurazione minima (- f). Per altre informazioni, vedere [Opzioni di avvio del servizio del motore di database](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Argomento|  
|----------|-----------|  
|Viene illustrato come creare trigger di accesso. I trigger LOGON possono essere creati da qualsiasi database, ma vengono registrati a livello del server e memorizzati nel database **master** .|[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)|  
|Viene illustrato come modificare trigger LOGON.|[ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|Viene illustrato come eliminare trigger LOGON.|[DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|Viene descritto come restituire informazioni sui trigger LOGON.|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|Viene descritto come acquisire dati degli eventi del trigger LOGON.||  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DDL](../../relational-databases/triggers/ddl-triggers.md)  
  
  
