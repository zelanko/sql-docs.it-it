---
title: Finestra di dialogo Crea account e profilo Posta elettronica database (Gestione configurazione Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 309cd3f67cb6fd4d41e3513aa6d3876af53bbc1b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971741"
---
# <a name="create-database-mail-profile-and-account-dialog-box-master-data-services-configuration-manager"></a>Finestra di dialogo Create account e profili di Posta elettronica database (Gestione configurazione Master Data Services)
  Usare la finestra di dialogo **Crea account e profilo di Posta elettronica database** per creare un profilo di Posta elettronica database e un account di Posta elettronica database per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Questo profilo verrà utilizzato per avvisare utenti e gruppi tramite posta elettronica quando la convalida delle regole business ha esito negativo.  
  
## <a name="database-mail-profile-and-account"></a>Account e profili di Posta elettronica database  
 Un *profilo di posta elettronica database* è una raccolta di account posta elettronica database. Un *account posta elettronica database* contiene le informazioni [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzate da per inviare messaggi di posta elettronica a un server SMTP. Quando si creano il profilo e l'account in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], l'account viene aggiunto automaticamente al profilo e le informazioni sull'account vengono utilizzate per inviare messaggi di posta elettronica.  
  
> [!NOTE]  
>  Non è possibile utilizzare [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] per aggiornare gli account e i profili di Posta elettronica database esistenti, né è possibile configurare più di un account per un profilo. Per eseguire attività più avanzate con Posta elettronica database, è possibile usare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o gli script Transact-SQL. Per altre informazioni, vedere la sezione [Oggetti di configurazione di Posta elettronica database](../relational-databases/database-mail/database-mail-configuration-objects.md) nella documentazione online di SQL Server.  
  
|Nome del controllo|Description|  
|------------------|-----------------|  
|**Nome profilo**|Digitare un nome per il nuovo profilo di Posta elettronica database. Deve essere un nome univoco nei profili di Posta elettronica database configurati per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Dopo che è stato creato, il profilo risulterà disponibile e selezionato nella pagina **Database** in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].|  
|**Nome account**|Digitare un nome per il nuovo account di Posta elettronica database da associare al profilo. Deve essere un nome univoco negli account di Posta elettronica database configurati per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . L'account non deve corrispondere a un account di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a un account utente di Windows.|  
  
## <a name="outgoing-smtp-mail-server"></a>Server della posta in uscita (SMTP)  
  
|Nome del controllo|Description|  
|------------------|-----------------|  
|**Indirizzo di posta elettronica**|Digitare il nome associato all'indirizzo di posta elettronica relativo all'account. Si tratta dell'indirizzo di posta elettronica da cui viene inviato il messaggio di posta elettronica e deve essere nel formato *email_name* @ *Domain_name*. Un esempio di indirizzo di posta elettronica è sales@contoso.com.|  
|**Nome visualizzato**|Impostazione facoltativa. Digitare il nome da visualizzare nei messaggi di posta elettronica inviati dall'account. Un esempio di nome visualizzato è Contoso Sales Group.|  
|**Indirizzo di posta elettronica risposte**|Impostazione facoltativa. Digitare l'indirizzo di posta elettronica da utilizzare per le risposte ai messaggi inviati dall'account. Un esempio di indirizzo di posta elettronica per le risposte è admin@contoso.com.|  
|**Server SMTP**|Digitare il nome o l'indirizzo IP del server SMTP utilizzato dall'account per l'invio della posta. Un esempio di formato del server SMTP è `smtp.` *<company_name>* `.com` . Per informazioni, rivolgersi all'amministratore del sistema di posta.|  
|**Numero della porta**|Digitare il numero di porta del server SMTP per l'account. Il numero di porta per SMTP predefinito è 25.|  
|**Il server necessita di una connessione sicura (SSL)**|Consente di crittografare le comunicazioni mediante SSL (Secure Sockets Layer).|  
  
## <a name="smtp-authentication"></a>Autenticazione SMTP  
 È possibile inviare Posta elettronica database usando le credenziali di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], altre credenziali specificate dall'utente oppure in modo anonimo. In base alla procedura consigliata, se il server di posta elettronica richiede l'autenticazione, è consigliabile creare un account utente specifico da utilizzare in modo specifico per Posta elettronica database. L'account utente deve disporre di autorizzazioni minime e non deve essere utilizzato per altri scopi.  
  
|Nome del controllo|Description|  
|------------------|-----------------|  
|**Autenticazione di Windows con credenziali del servizio Motore di database**|Consente di specificare che Posta elettronica database deve utilizzare le credenziali dell' [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] account del servizio Windows per l'autenticazione nel server SMTP.|  
|**Autenticazione di base**|Specificare che Posta elettronica database deve utilizzare un nome utente e una password specifici per l'autenticazione nel server SMTP. Queste informazioni vengono utilizzate solo per l'autenticazione con il server di posta elettronica e non è necessario che l'account corrisponda a un utente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a un utente nel computer che esegue [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Nome utente**|Digitare il nome dell'account utente utilizzato da Posta elettronica database per accedere al server SMTP. È necessario un nome utente quando il server SMTP richiede l'autenticazione di base.|  
|**Password**|Digitare la password utilizzata da Posta elettronica database per accedere al server SMTP. È necessaria una password quando il server SMTP richiede l'autenticazione di base.|  
|**Conferma password**|Digitare di nuovo la password per confermarla.|  
|**Autenticazione anonima**|Specificare che il server SMTP non richiede l'autenticazione. Posta elettronica database non utilizzerà credenziali per l'autenticazione nel server SMTP.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina di configurazione del database &#40;Gestione configurazione Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Configurare il database e il sito Web per Master Data Services](set-up-the-database-and-website-for-master-data-services.md)  
  
  
