---
title: Configurare la sicurezza del dialogo per le notifiche degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d83bfe63c3a9b24c2be8d08916dd2384c59edc93
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996561"
---
# <a name="configure-dialog-security-for-event-notifications"></a>Configurazione della sicurezza del dialogo per le notifiche degli eventi
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] per le notifiche degli eventi che prevedono l'invio di messaggi a Service Broker su un server remoto. È necessario configurare manualmente la sicurezza del dialogo in base al modello di sicurezza avanzata del dialogo di [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Il modello di sicurezza avanzata attiva la crittografia e la decrittografia di messaggi inviati da e a server remoti. Sebbene le notifiche degli eventi vengano inviate in una sola direzione, gli altri messaggi, ad esempio gli errori, vengono anche restituiti nella direzione opposta.  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>Configurazione della sicurezza del dialogo per le notifiche degli eventi  
 Nella procedura seguente viene descritto il processo necessario per l'implementazione della sicurezza del dialogo per la notifica degli eventi. La procedura include azioni da eseguire sia sul server di origine sia sul server di destinazione. Nel server di origine viene creata la notifica degli eventi. Il server di destinazione riceve il messaggio di notifica degli eventi. È necessario completare le azioni di ogni passaggio sia per il server di origine sia per il server di destinazione prima di andare al passaggio successivo.  
  
> [!IMPORTANT]  
>  È necessario creare tutti i certificati con date di inizio e di scadenza valide.  
  
 **Passaggio 1: impostare un numero di porta TCP e un nome del servizio di destinazione.**  
  
 Impostare la porta TCP in cui il server di origine e il server di destinazione riceveranno i messaggi. È inoltre necessario determinare il nome del servizio di destinazione.  
  
 **Passaggio 2: configurare la crittografia e la condivisione dei certificati per l'autenticazione a livello di database.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|Scegliere o creare un database per contenere la notifica degli eventi e la chiave master.|Scegliere o creare un database per contenere la chiave master.|  
|[Creare una chiave master](/sql/t-sql/statements/create-master-key-transact-sql)se non ne è presente una per il database di origine. È necessaria una chiave master sia nel database di origine sia in quello di destinazione per consentire la protezione dei rispettivi certificati.|Se non è presente alcuna chiave master per il database di destinazione, crearne una.|  
|[Creare un account di accesso](/sql/t-sql/statements/create-login-transact-sql) e un [utente](/sql/t-sql/statements/create-user-transact-sql) corrispondente per il database di origine.|Creare un account di accesso e un utente corrispondente per il database di destinazione.|  
|[Creare un certificato](/sql/t-sql/statements/create-certificate-transact-sql) di proprietà dell'utente del database di origine.|Creare un certificato di proprietà dell'utente del database di destinazione.|  
|[Eseguire il backup del certificato](/sql/t-sql/statements/backup-certificate-transact-sql) in un file accessibile al server di destinazione.|Eseguire il backup del certificato in un file accessibile al server di origine.|  
|[Creare un utente](/sql/t-sql/statements/create-user-transact-sql), specificando l'utente del database di destinazione e WITHOUT LOGIN. Questo utente sarà proprietario del certificato del database di destinazione da creare dal file di backup. Non è necessario eseguire il mapping dell'utente a un account di accesso, poiché l'unico scopo di questo utente è essere proprietario del certificato del database di destinazione creato al passaggio 3 seguente.|Creare un utente, specificando l'utente del database di origine e WITHOUT LOGIN. Questo utente sarà proprietario del certificato del database di origine da creare dal file di backup. Non è necessario eseguire il mapping dell'utente a un account di accesso, poiché l'unico scopo di questo utente è essere proprietario del certificato del database di origine creato al passaggio 3 seguente.|  
  
 **Passaggio 3: condividere i certificati e concedere le autorizzazioni per l'autenticazione a livello di database.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare un certificato](/sql/t-sql/statements/create-certificate-transact-sql) dal file di backup del certificato di destinazione, specificando l'utente del database di destinazione come proprietario.|Creare un certificato dal file di backup del certificato di origine, specificando l'utente del database di origine come proprietario.|  
|[Concedere l'autorizzazione](/sql/t-sql/statements/grant-transact-sql) per la creazione della notifica degli eventi all'utente del database di origine. Per altre informazioni su questa autorizzazione, vedere [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)se non ne è presente una per il database di origine.|Concedere l'autorizzazione REFERENCES all'utente del database di destinazione sul contratto [!INCLUDE[ssSB](../../includes/sssb-md.md)] per le notifiche degli eventi esistente: `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`.|  
|[Creare un'associazione al servizio remoto](/sql/t-sql/statements/create-remote-service-binding-transact-sql) al servizio di destinazione e specificare le credenziali dell'utente del database di destinazione. L'associazione al servizio remoto garantisce che la chiave pubblica nel certificato di proprietà dell'utente del database di origine autentichi i messaggi inviati al server di destinazione.|[Concedere](/sql/t-sql/statements/grant-transact-sql) le autorizzazioni CREATE QUEUE, CREATE SERVICE e CREATE SCHEMA all'utente del database di destinazione.|  
||Connettersi al database come utente del database di destinazione, se non è ancora stata eseguita questa operazione.|  
||[Creare una coda](/sql/t-sql/statements/create-queue-transact-sql) in cui ricevere i messaggi di notifica degli eventi e [creare un servizio](/sql/t-sql/statements/create-service-transact-sql) per il recapito dei messaggi.|  
||[Concedere l'autorizzazione SEND](/sql/t-sql/statements/grant-transact-sql) per il servizio di destinazione all'utente del database di origine.|  
|Fornire l'identificatore di Service Broker del database di origine al server di destinazione. È possibile ottenere questo identificatore eseguendo una query sulla colonna **service_broker_guid** della vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) Per una notifica degli eventi a livello di server, usare l'identificatore di Service Broker di **msdb**.|Fornire l'identificatore di Service Broker del database di destinazione al server di origine.|  
  
 **Passaggio 4: creare route e impostare l'autenticazione a livello di server.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare una route](/sql/t-sql/statements/create-route-transact-sql) al servizio di destinazione e specificare l'identificatore di Service Broker del database di destinazione e il numero di porta TCP precedentemente concordato.|Creare una route al servizio di origine e specificare l'identificatore di Service Broker del database di origine e il numero di porta TCP precedentemente definito. Per specificare il servizio di origine, utilizzare il servizio fornito seguente: `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`.|  
|Passare al database **master** per configurare l'autenticazione a livello di server.|Passare al database **master** per configurare l'autenticazione a livello di server.|  
|**Creare una chiave master** se non ne è presente una per il database [master](/sql/t-sql/statements/create-master-key-transact-sql).|Creare una chiave master se non ne è presente una per il database **master** .|  
|[Creare un certificato](/sql/t-sql/statements/create-certificate-transact-sql) per l'autenticazione del database.|Creare un certificato per l'autenticazione del database.|  
|[Eseguire il backup del certificato](/sql/t-sql/statements/backup-certificate-transact-sql) in un file accessibile al server di destinazione.|Eseguire il backup del certificato in un file accessibile al server di origine.|  
|[Creare un endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)e specificare il numero di porta TCP precedentemente concordato, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nome_certificato*) e il nome del certificato di autenticazione.|Creare un endpoint e specificare il numero di porta TCP precedentemente concordato, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nome_certificato*) e il nome del certificato di autenticazione.|  
|[Creare un account di accesso](/sql/t-sql/statements/create-login-transact-sql)e specificare l'account di accesso del server di destinazione.|Creare un account di accesso e specificare l'account di accesso del server di origine.|  
|[Concedere l'autorizzazione CONNECT](/sql/t-sql/statements/grant-transact-sql) per l'endpoint all'account di accesso dell'autenticatore di destinazione.|Concedere l'autorizzazione CONNECT per l'endpoint all'account di accesso dell'autenticatore di origine.|  
|[Creare un utente](/sql/t-sql/statements/create-user-transact-sql)e specificare l'account di accesso dell'autenticatore di destinazione.|Creare un utente e specificare l'account di accesso dell'autenticatore di origine.|  
  
 **Passaggio 5: condividere i certificati per l'autenticazione a livello di server e creare la notifica degli eventi.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare un certificato](/sql/t-sql/statements/create-certificate-transact-sql) dal file di backup del certificato di destinazione, specificando l'utente dell'autenticatore di destinazione come proprietario.|Creare un certificato dal file di backup del certificato di origine, specificando l'utente dell'autenticatore di origine come proprietario.|  
|Passare al database di origine in cui creare la notifica degli eventi e connettersi come utente del database di origine, se non è ancora stata eseguita questa operazione.|Passare al database di destinazione per ricevere i messaggi di notifica degli eventi.|  
|[Creare la notifica degli eventi](/sql/t-sql/statements/create-event-notification-transact-sql)e specificare il servizio di Service Broker e l'identificatore del database di destinazione.||  
  
## <a name="see-also"></a>Vedere anche  
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Gerarchia di crittografia](../security/encryption/encryption-hierarchy.md)   
 [Implementazione di notifiche degli eventi](event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-remote-service-binding-transact-sql)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-queue-transact-sql)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-service-transact-sql)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
  
