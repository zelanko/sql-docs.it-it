---
title: Configurare la sicurezza del dialogo per le notifiche degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 488b1efd533f038914f2d0186e29e28622531f02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048898"
---
# <a name="configure-dialog-security-for-event-notifications"></a>Configurazione della sicurezza del dialogo per le notifiche degli eventi
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
|[Creare una chiave master](../../t-sql/statements/create-master-key-transact-sql.md)se non ne è presente una per il database di origine. È necessaria una chiave master sia nel database di origine sia in quello di destinazione per consentire la protezione dei rispettivi certificati.|Se non è presente alcuna chiave master per il database di destinazione, crearne una.|  
|[Creare un account di accesso](../../t-sql/statements/create-login-transact-sql.md) e un [utente](../../t-sql/statements/create-user-transact-sql.md) corrispondente per il database di origine.|Creare un account di accesso e un utente corrispondente per il database di destinazione.|  
|[Creare un certificato](../../t-sql/statements/create-certificate-transact-sql.md) di proprietà dell'utente del database di origine.|Creare un certificato di proprietà dell'utente del database di destinazione.|  
|[Eseguire il backup del certificato](../../t-sql/statements/backup-certificate-transact-sql.md) in un file accessibile al server di destinazione.|Eseguire il backup del certificato in un file accessibile al server di origine.|  
|[Creare un utente](../../t-sql/statements/create-user-transact-sql.md), specificando l'utente del database di destinazione e WITHOUT LOGIN. Questo utente sarà proprietario del certificato del database di destinazione da creare dal file di backup. Non è necessario eseguire il mapping dell'utente a un account di accesso, poiché l'unico scopo di questo utente è essere proprietario del certificato del database di destinazione creato al passaggio 3 seguente.|Creare un utente, specificando l'utente del database di origine e WITHOUT LOGIN. Questo utente sarà proprietario del certificato del database di origine da creare dal file di backup. Non è necessario eseguire il mapping dell'utente a un account di accesso, poiché l'unico scopo di questo utente è essere proprietario del certificato del database di origine creato al passaggio 3 seguente.|  
  
 **Passaggio 3: condividere i certificati e concedere le autorizzazioni per l'autenticazione a livello di database.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare un certificato](../../t-sql/statements/create-certificate-transact-sql.md) dal file di backup del certificato di destinazione, specificando l'utente del database di destinazione come proprietario.|Creare un certificato dal file di backup del certificato di origine, specificando l'utente del database di origine come proprietario.|  
|[Concedere l'autorizzazione](../../t-sql/statements/grant-transact-sql.md) per la creazione della notifica degli eventi all'utente del database di origine. Per altre informazioni su questa autorizzazione, vedere [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)se non ne è presente una per il database di origine.|Concedere l'autorizzazione REFERENCES all'utente del database di destinazione sul contratto [!INCLUDE[ssSB](../../includes/sssb-md.md)] per le notifiche degli eventi esistente: `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`.|  
|[Creare un'associazione al servizio remoto](../../t-sql/statements/create-remote-service-binding-transact-sql.md) al servizio di destinazione e specificare le credenziali dell'utente del database di destinazione. L'associazione al servizio remoto garantisce che la chiave pubblica nel certificato di proprietà dell'utente del database di origine autentichi i messaggi inviati al server di destinazione.|[Concedere](../../t-sql/statements/grant-transact-sql.md) le autorizzazioni CREATE QUEUE, CREATE SERVICE e CREATE SCHEMA all'utente del database di destinazione.|  
||Connettersi al database come utente del database di destinazione, se non è ancora stata eseguita questa operazione.|  
||[Creare una coda](../../t-sql/statements/create-queue-transact-sql.md) in cui ricevere i messaggi di notifica degli eventi e [creare un servizio](../../t-sql/statements/create-service-transact-sql.md) per il recapito dei messaggi.|  
||[Concedere l'autorizzazione SEND](../../t-sql/statements/grant-transact-sql.md) per il servizio di destinazione all'utente del database di origine.|  
|Fornire l'identificatore di Service Broker del database di origine al server di destinazione. È possibile ottenere questo identificatore eseguendo una query sulla colonna **service_broker_guid** della vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) Per una notifica degli eventi a livello di server, usare l'identificatore di Service Broker di **msdb**.|Fornire l'identificatore di Service Broker del database di destinazione al server di origine.|  
  
 **Passaggio 4: creare route e impostare l'autenticazione a livello di server.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare una route](../../t-sql/statements/create-route-transact-sql.md) al servizio di destinazione e specificare l'identificatore di Service Broker del database di destinazione e il numero di porta TCP precedentemente concordato.|Creare una route al servizio di origine e specificare l'identificatore di Service Broker del database di origine e il numero di porta TCP precedentemente definito. Per specificare il servizio di origine, utilizzare il servizio fornito seguente: `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`.|  
|Passare al database **master** per configurare l'autenticazione a livello di server.|Passare al database **master** per configurare l'autenticazione a livello di server.|  
|**Creare una chiave master** se non ne è presente una per il database [master](../../t-sql/statements/create-master-key-transact-sql.md).|Creare una chiave master se non ne è presente una per il database **master** .|  
|[Creare un certificato](../../t-sql/statements/create-certificate-transact-sql.md) per l'autenticazione del database.|Creare un certificato per l'autenticazione del database.|  
|[Eseguire il backup del certificato](../../t-sql/statements/backup-certificate-transact-sql.md) in un file accessibile al server di destinazione.|Eseguire il backup del certificato in un file accessibile al server di origine.|  
|[Creare un endpoint](../../t-sql/statements/create-endpoint-transact-sql.md)e specificare il numero di porta TCP precedentemente concordato, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nome_certificato*) e il nome del certificato di autenticazione.|Creare un endpoint e specificare il numero di porta TCP precedentemente concordato, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nome_certificato*) e il nome del certificato di autenticazione.|  
|[Creare un account di accesso](../../t-sql/statements/create-login-transact-sql.md)e specificare l'account di accesso del server di destinazione.|Creare un account di accesso e specificare l'account di accesso del server di origine.|  
|[Concedere l'autorizzazione CONNECT](../../t-sql/statements/grant-transact-sql.md) per l'endpoint all'account di accesso dell'autenticatore di destinazione.|Concedere l'autorizzazione CONNECT per l'endpoint all'account di accesso dell'autenticatore di origine.|  
|[Creare un utente](../../t-sql/statements/create-user-transact-sql.md)e specificare l'account di accesso dell'autenticatore di destinazione.|Creare un utente e specificare l'account di accesso dell'autenticatore di origine.|  
  
 **Passaggio 5: condividere i certificati per l'autenticazione a livello di server e creare la notifica degli eventi.**  
  
 Completare le azioni seguenti nel server di origine e in quello di destinazione.  
  
|Server di origine|Server di destinazione|  
|-------------------|-------------------|  
|[Creare un certificato](../../t-sql/statements/create-certificate-transact-sql.md) dal file di backup del certificato di destinazione, specificando l'utente dell'autenticatore di destinazione come proprietario.|Creare un certificato dal file di backup del certificato di origine, specificando l'utente dell'autenticatore di origine come proprietario.|  
|Passare al database di origine in cui creare la notifica degli eventi e connettersi come utente del database di origine, se non è ancora stata eseguita questa operazione.|Passare al database di destinazione per ricevere i messaggi di notifica degli eventi.|  
|[Creare la notifica degli eventi](../../t-sql/statements/create-event-notification-transact-sql.md)e specificare il servizio di Service Broker e l'identificatore del database di destinazione.||  
  
## <a name="see-also"></a>Vedere anche  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Implementazione di notifiche degli eventi](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
