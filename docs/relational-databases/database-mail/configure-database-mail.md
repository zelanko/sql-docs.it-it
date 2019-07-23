---
title: Configurare Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlimail.profileandaccountmanagement.f1
- sql13.swb.sqlimail.newaccount.f1
- sql13.swb.dbmail. manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.manageexistingprofile.f1
- sql13.swb.sqlimail.addaccounttoprofile.f1
- sql13.swb.dbmail.manageexistingaccount.f1
- sql13.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.welcome.f1
- sql13.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql13.swb.sqlimail.newsqlimailaccount.f1
- sql13.swb.sqlimail.selectconfiguration.f1
- sql13.swb.dbmail.completewizard.f1
- sql13.swb.dbmail.sendtestemail.test.f1
- sql13.swb.sqlimail.newprofile.f1
- sql13.swb.dbmail.addaccounttoprofile.f1
- sql13.swb.dbmail.newprofile.f1
- sql13.swb.sqlimail.manageexistingaccount.f1
- sql13.swb.dbmail.welcome.f1
- sql13.swb.dbmail.newaccount.f1
- sql13.swb.dbmail.profileandaccountmanagement.f1
- sql13.swb.dbmail.selectconfiguration.f1
- sql13.swb.dbmail.sendtestemail.f1
- sql13.swb.sqlimail.completewizard.f1
- sql13.swb.dbmail.configuresystem.f1
- sql13.swb.sqlimail.configuresystem.f1
- sql13.swb.dbmail.newsqlimailaccount.f1
- sql13.swb.dbmail.manageexistingprofile.f1
- sql13.swb.dbmail.manageprofilesecurity.principalview.f1
ms.assetid: 7edc21d4-ccf3-42a9-84c0-3f70333efce6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f57825d1c4458761724c2e02c243a32a89dc018
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134582"
---
# <a name="configure-database-mail"></a>Configurare Posta elettronica database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come abilitare e configurare Posta elettronica database utilizzando la Configurazione guidata Posta elettronica database e come creare uno script di configurazione per Posta elettronica database utilizzando i modelli.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per configurare Posta elettronica database con:**  [Configurazione guidata Posta elettronica database](#DBWizard), [Modelli](#Template)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Usare l'opzione **Stored procedure estese di posta elettronica database** per abilitare Posta elettronica database nel server. Per altre informazioni, vedere l'argomento di riferimento [Opzione di configurazione del server Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) .  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 L'abilitazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker in un database richiede un blocco a livello del database. Se Service Broker è stato disabilitato nel database **msdb**, per abilitare Posta elettronica database occorre prima arrestare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per consentire a Service Broker di ottenere il blocco necessario.  
  
###  <a name="Security"></a> Sicurezza  
 Per configurare Posta elettronica database, è necessario essere un membro del ruolo predefinito del server **sysadmin** . Per inviare Posta elettronica database, è necessario essere un membro del ruolo del database **DatabaseMailUserRole** nel database **msdb** .  
  
##  <a name="DBWizard"></a> Utilizzo della Configurazione guidata Posta elettronica database  
 **Per configurare Posta elettronica database tramite una procedura guidata**  
  
1.  In Esplora oggetti espandere il nodo dell'istanza in cui si desidera configurare Posta elettronica database.  
  
2.  Espandere il nodo **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse su **Posta elettronica database**e quindi scegliere **Configura Posta elettronica database**.  
  
4.  Completare le finestre di dialogo della procedura guidata  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    -   [Pagina introduttiva](#Welcome)  
  
    -   [Pagina Selezione attività di configurazione](#ConfigTask)  
  
    -   [Pagina Nuovo account](#NewAccount)  
  
    -   [Pagina Gestione account esistente](#ExistingAccount)  
  
    -   [Pagina Nuovo profilo](#NewProfile)  
  
    -   [Pagina Gestione profilo esistente](#ExistingProfile)  
  
    -   [Pagina Aggiungi account al profilo](#AddAccount)  
  
    -   [Pagina Gestisci account e profili](#AccountsProfiles)  
  
    -   [Gestione sicurezza profilo, scheda Pubblico](#ProfileSecurityPublic)  
  
    -   [Gestione sicurezza profilo, scheda Privato](#ProfileSecurityPrivate)  
  
    -   [Pagina Configurazione parametri di sistema](#SystemParameters)  
  
    -   [Pagina Completamento procedura guidata](#CompleteWizard)  
  
    -   [Pagina Invia messaggio di prova](#TestEmail)  
  
###  <a name="Welcome"></a> Pagina introduttiva  
 In questa pagina vengono illustrati i passaggi necessari per configurare Posta elettronica database.  
  
 **Non visualizzare più questa pagina**: selezionare questa opzione per non visualizzare più la pagina introduttiva.  
  
 **Avanti** : consente di passare alla pagina **Selezionare un'attività di configurazione** .  
  
 **Annulla**: consente di terminare la procedura guidata senza configurare Posta elettronica database  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="ConfigTask"></a> Selezione attività di configurazione  
 Usare la pagina **Selezione attività di configurazione** per indicare quali attività verranno eseguite ogni volta che si usa la procedura guidata. Se si vuole cambiare tali attività prima del completamento della procedura guidata, fare clic sul pulsante **Indietro** per tornare in questa pagina e selezionare un'attività diversa.  
  
> [!NOTE]  
>  Se la caratteristica Posta elettronica database non è stata abilitata, verrà visualizzato il messaggio: **La caratteristica Posta elettronica database non è disponibile.  Abilitarla?** L'opzione **Sì**equivale ad abilitare la funzionalità Posta elettronica database usando l'opzione [Stored procedure estese di posta elettronica database](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) della stored procedure di sistema **sp_configure** .  
  
 **Installa Posta elettronica database eseguendo le attività seguenti**  
 Consente di eseguire tutte le attività necessarie per installare Posta elettronica database per la prima volta. Questa opzione include tutte le altre tre.  
  
 **Gestisci account e profili di Posta elettronica database**  
 Utilizzare questa opzione per creare nuovi profili e account di Posta elettronica database oppure per visualizzare, modificare o eliminare quelli esistenti  
  
 **Gestisci sicurezza profilo**  
 Consente di configurare gli utenti che dispongono dell'accesso ai profili di Posta elettronica database.  
  
 **Visualizza o modifica i parametri di sistema**  
 Consente di configurare i parametri di sistema di Posta elettronica database, ad esempio le dimensioni massime di file consentite per gli allegati.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="NewAccount"></a> Pagina Nuovo account  
 Utilizzare questa pagina per creare un nuovo account di Posta elettronica database. In un account di Posta elettronica database sono contenute le informazioni per l'invio di messaggi di posta elettronica a un server SMTP.  
  
 In un account di Posta elettronica database sono presenti le informazioni utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per inviare messaggi di posta elettronica a un server SMTP. In ogni account sono incluse le informazioni per un singolo server di posta elettronica.  
  
 Un account di Posta elettronica database viene utilizzato solo per Posta elettronica database Un account di Posta elettronica database non corrisponde a un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a un account di Microsoft Windows. È possibile inviare Posta elettronica database mediante le credenziali del servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], altre credenziali fornite dall'utente oppure in modo anonimo. Se si utilizza l'autenticazione di base, il nome utente e la password di un account di Posta elettronica database vengono utilizzati solo per l'autenticazione al server di posta elettronica. Non è necessario che l'account corrisponda a un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a un utente del computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome account**  
 Digitare il nome del nuovo account.  
  
 **Descrizione**  
 Digitare una descrizione dell'account. La descrizione è facoltativa.  
  
 **Indirizzo posta elettronica**  
 Digitare il nome associato all'indirizzo di posta elettronica relativo all'account. Si tratta dell'indirizzo di posta elettronica da cui vengono inviati i messaggi. Un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ad esempio, può inviare posta elettronica dall'indirizzo SqlAgent@Adventure-Works.com.  
  
 **Nome visualizzato**  
 Digitare il nome che deve essere visualizzato nei messaggi di posta elettronica inviati dall'account. Il nome visualizzato è facoltativo. Si tratta del nome visualizzato nei messaggi inviati da questo account. È ad esempio possibile che un account per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent visualizzi il nome "SQL Server Agent Automated Mailer" nei messaggi di posta elettronica.  
  
 **Indirizzo risposte**  
 Consente di digitare l'indirizzo di posta elettronica che verrà utilizzato per le risposte ai messaggi di posta elettronica inviati da questo account. L'indirizzo risposte è facoltativo. Le risposte a un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ad esempio, possono essere indirizzate all'amministratore del database danw@Adventure-Works.com.  
  
 **Nome server**  
 Digitare il nome o l'indirizzo IP del server SMTP utilizzato dall'account per l'invio della posta. In genere, presenta un formato simile a **smtp.** _<nome_società>_ **.com**. Per informazioni, rivolgersi all'amministratore del sistema di posta.  
  
 **Numero di porta**  
 Digitare il numero di porta del server SMTP per l'account. La maggior parte dei server SMTP utilizza la porta 25.  
  
 **Il server necessita di una connessione sicura (SSL)**  
 Consente di crittografare le comunicazioni mediante SSL (Secure Sockets Layer).  
  
 **Autenticazione di Windows con credenziali del servizio Motore di database**  
 Viene eseguita la connessione al server SMTP mediante le credenziali configurate per il servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticazione di base**  
 Consente di specificare il nome utente e la password necessari per il server SMTP.  
  
 **Nome utente**  
 Consente di digitare il nome utente utilizzato da Posta elettronica database per accedere al server SMTP. Il nome utente è necessario se il server SMTP richiede l'autenticazione di base.  
  
 **Password**  
 Consente di digitare la password utilizzata da Posta elettronica database per accedere al server SMTP. La password è necessaria se il server SMTP richiede l'autenticazione di base.  
  
 **Conferma password**  
 Digitare di nuovo la password per confermarla. La password è necessaria se il server SMTP richiede l'autenticazione di base.  
  
 **Autenticazione anonima**  
 La posta elettronica viene inviata al server SMTP senza credenziali di accesso. Utilizzare questa opzione se il server SMTP non richiede l'autenticazione.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="ExistingAccount"></a> Pagina Gestione account esistente  
 Utilizzare questa pagina per gestire un account di Posta elettronica database esistente.  
  
 **Nome account**  
 Consente di selezionare l'account da visualizzare, aggiornare o eliminare.  
  
 **Elimina**  
 Consente di eliminare l'account selezionato. È necessario rimuovere l'account dai profili associati, o eliminare tali profili, prima di poter eliminare l'account selezionato.  
  
 **Descrizione**  
 Consente di visualizzare o aggiornare la descrizione dell'account. La descrizione è facoltativa.  
  
 **Indirizzo posta elettronica**  
 Consente di visualizzare o aggiornare il nome dell'indirizzo di posta elettronica dell'account. Si tratta dell'indirizzo di posta elettronica da cui vengono inviati i messaggi. Un account di Microsoft SQL Server Agent, ad esempio, può inviare posta elettronica dall'indirizzo **SqlAgent@Adventure-Works.com** .  
  
 **Nome visualizzato**  
 Consente di visualizzare o aggiornare il nome da visualizzare nei messaggi di posta elettronica inviati da questo account. Il nome visualizzato è facoltativo. Si tratta del nome visualizzato nei messaggi inviati da questo account. Un account di SQL Server Agent, ad esempio, può visualizzare il nome **SQL Server Agent Automated Mailer** nei messaggi di posta elettronica.  
  
 **Indirizzo risposte**  
 Consente di visualizzare o aggiornare l'indirizzo di posta elettronica da utilizzare per le risposte ai messaggi inviati da questo account. L'indirizzo risposte è facoltativo. Le risposte a un account di SQL Server Agent, ad esempio, possono essere indirizzate all'amministratore del database **danw@Adventure-Works.com** .  
  
 **Nome server**  
 Consente di visualizzare o aggiornare il nome del server SMTP utilizzato dall'account per l'invio della posta. In genere, presenta un formato simile a **smtp.<nome_società>.com**. Per informazioni, rivolgersi all'amministratore del sistema di posta.  
  
 **Numero di porta**  
 Consente di visualizzare o aggiornare il numero di porta del server SMTP di questo account. La maggior parte dei server SMTP utilizza la porta 25.  
  
 **Il server necessita di una connessione sicura (SSL)**  
 Consente di crittografare le comunicazioni mediante SSL (Secure Sockets Layer).  
  
 **Autenticazione di Windows con credenziali del servizio Motore di database**  
 Viene eseguita la connessione al server SMTP mediante le credenziali configurate per il servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticazione di base**  
 Consente di specificare il nome utente e la password necessari per il server SMTP.  
  
 **User name**  
 Consente di visualizzare o aggiornare il nome utente utilizzato da Posta elettronica database per accedere al server SMTP. Il nome utente è necessario se il server SMTP richiede l'autenticazione di base.  
  
 **Password**  
 Consente di modificare la password utilizzata da Posta elettronica database per accedere al server SMTP. La password è necessaria se il server SMTP richiede l'autenticazione di base.  
  
 **Conferma password**  
 Digitare di nuovo la password per confermarla. La password è necessaria se il server SMTP richiede l'autenticazione di base.  
  
 **Autenticazione anonima**  
 La posta elettronica viene inviata al server SMTP senza credenziali di accesso. Utilizzare questa opzione se il server SMTP non richiede l'autenticazione.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="NewProfile"></a> Pagina Nuovo profilo  
 Utilizzare questa pagina per creare un profilo di Posta elettronica database, Un profilo di Posta elettronica database è una raccolta di account di Posta elettronica database. I profili consentono di migliorare l'affidabilità nei casi in cui non sia possibile raggiungere un server di posta elettronica, offrendo account di Posta elettronica database alternativi. È necessario almeno un account di Posta elettronica database. Per altre informazioni sull'impostazione della priorità degli account di Posta elettronica database, vedere [Creare un profilo di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-profile.md).  
  
 Usare i pulsanti **Sposta su** e **Sposta giù** per modificare l'ordine di uso degli account di Posta elettronica database. L'ordine viene stabilito in base a un valore definito come numero di sequenza. Il pulsante**Sposta su** consente di ridurre il numero di sequenza, mentre il pulsante **Sposta giù** consente di aumentarlo. Il numero di sequenza determina l'ordine in cui Posta elettronica database utilizza gli account nel profilo. Per un nuovo messaggio di posta elettronica, Posta elettronica database inizia con l'account che ha il numero di sequenza più basso. Se l'invio del messaggio con tale account ha esito negativo, Posta elettronica database prova con l'account con il numero di sequenza successivo e così via, finché il messaggio non viene inviato o finché anche l'invio con l'account con il numero di sequenza più alto non ha esito negativo. Se l'invio con l'account con il numero di sequenza più alto ha esito negativo, il tentativo di inviare il messaggio viene sospeso per il periodo di tempo specificato nel parametro **AccountRetryDelay** . Trascorso questo periodo di tempo, Posta elettronica database prova di nuovo a inviare il messaggio, iniziando con l'account con il numero di sequenza più basso. Usare il parametro **AccountRetryDelay** per specificare quante volte il processo di posta elettronica esterno deve provare a inviare il messaggio di posta elettronica usando ogni account del profilo specificato. È possibile configurare i parametri **AccountRetryDelay** e **AccountRetryAttempts** nella pagina **Configurazione parametri di sistema** di Configurazione guidata Posta elettronica database.  
  
 **Nome profilo**  
 Consente di digitare il nome del nuovo profilo. Il profilo verrà creato con il nome specificato. Non utilizzare il nome di un profilo esistente.  
  
 **Descrizione**  
 Consente di digitare una descrizione per il profilo. La descrizione è facoltativa.  
  
 **Account SMTP**  
 Consente di selezionare uno o più account per il profilo. L'ordine in cui Posta elettronica utilizza gli account è determinato dal livello di priorità. Se non è elencato alcun account, è necessario fare clic su **Aggiungi** per continuare e aggiungere un nuovo account SMTP.  
  
 **Aggiungi**  
 Consente di aggiungere un account al profilo.  
  
 **Rimuovi**  
 Consente di rimuovere l'account selezionato dal profilo.  
  
 **Sposta su**  
 Consente di aumentare la priorità dell'account selezionato.  
  
 **Sposta giù**  
 Consente di ridurre la priorità dell'account selezionato.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="ExistingProfile"></a> Pagina Gestione profilo esistente  
 Utilizzare questa pagina per gestire un profilo di Posta elettronica database esistente. Un profilo di Posta elettronica database è una raccolta di account di Posta elettronica database. I profili consentono di migliorare l'affidabilità nei casi in cui non sia possibile raggiungere un server di posta elettronica, offrendo account di Posta elettronica database alternativi. È necessario almeno un account di Posta elettronica database. Per altre informazioni sull'impostazione della priorità degli account di Posta elettronica database, vedere [Creare un profilo di Posta elettronica database](../../relational-databases/database-mail/create-a-database-mail-profile.md).  
  
 Usare i pulsanti **Sposta su** e **Sposta giù** per modificare l'ordine di uso degli account di Posta elettronica database. L'ordine viene stabilito in base a un valore definito come numero di sequenza. Il pulsante**Sposta su** consente di ridurre il numero di sequenza, mentre il pulsante **Sposta giù** consente di aumentarlo. Il numero di sequenza determina l'ordine in cui Posta elettronica database utilizza gli account nel profilo. Per un nuovo messaggio di posta elettronica, Posta elettronica database inizia con l'account che ha il numero di sequenza più basso. Se l'invio del messaggio con tale account ha esito negativo, Posta elettronica database prova con l'account con il numero di sequenza successivo e così via, finché il messaggio non viene inviato o finché anche l'invio con l'account con il numero di sequenza più alto non ha esito negativo. Se l'invio con l'account con il numero di sequenza più alto ha esito negativo, il tentativo di inviare il messaggio viene sospeso per il periodo di tempo specificato nel parametro **AccountRetryDelay** . Trascorso questo periodo di tempo, Posta elettronica database prova di nuovo a inviare il messaggio, iniziando con l'account con il numero di sequenza più basso. Usare il parametro **AccountRetryDelay** per specificare quante volte il processo di posta elettronica esterno deve provare a inviare il messaggio di posta elettronica usando ogni account del profilo specificato. È possibile configurare i parametri **AccountRetryDelay** e **AccountRetryAttempts** nella pagina **Configurazione parametri di sistema** di Configurazione guidata Posta elettronica database.  
  
 **Nome profilo**  
 Consente di selezionare il nome del profilo da gestire.  
  
 **Elimina**  
 Consente di eliminare il profilo selezionato. Verrà richiesto di scegliere **Sì** per eliminare il profilo selezionato e impostare un errore per gli eventuali messaggi non inviati oppure di scegliere **No** per eliminare il profilo selezionato solo se non sono presenti messaggi non inviati.  
  
 **Descrizione**  
 Consente di visualizzare o modificare la descrizione del profilo selezionato. La descrizione è facoltativa.  
  
 **Account SMTP**  
 Consente di selezionare uno o più account per il profilo. La proprietà di failover imposta l'ordine in cui Posta elettronica database utilizza l'account in caso si verifichi un failover.  
  
 **Aggiungi**  
 Consente di aggiungere un account al profilo.  
  
 **Rimuovi**  
 Consente di rimuovere l'account selezionato dal profilo.  
  
 **Sposta su**  
 Consente di aumentare il valore della proprietà di failover per l'account selezionato.  
  
 **Sposta giù**  
 Consente di diminuire la priorità di failover per l'account selezionato.  
  
 **Priorità**  
 Consente di visualizzare la priorità di failover attualmente associata all'account.  
  
 **Nome account**  
 Consente di visualizzare il nome dell'account.  
  
 **E-mail Address**  
 Consente di visualizzare l'indirizzo di posta elettronica dell'account.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="AddAccount"></a> Add Account to Profile Page  
 Utilizzare questa pagina per specificare l'account da aggiungere al profilo. Selezionare un account esistente dalla casella **Nome account** o fare clic su **Nuovo account**.  
  
 **Nome account**  
 Consente di selezionare il nome dell'account da aggiungere al profilo.  
  
 **Indirizzo posta elettronica**  
 Consente di visualizzare l'indirizzo di posta elettronica per l'account selezionato. Non è possibile modificare l'indirizzo di posta elettronica da questa pagina. A questo scopo, tornare alla pagina principale della procedura guidata e selezionare l'opzione **Gestisci account e profili di Posta elettronica database** .  
  
 **Nome server**  
 Consente di visualizzare il nome del server di posta elettronica per l'account selezionato. Non è possibile modificare il nome del server di posta elettronica da questa pagina. A questo scopo, tornare alla pagina principale della procedura guidata e selezionare l'opzione **Gestisci account e profili di Posta elettronica database** .  
  
 **Nuovo account**  
 Consente di creare un nuovo account.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="AccountsProfiles"></a> Pagina Gestisci account e profili  
 Utilizzare questa pagina per selezionare un'attività per la gestione di un profilo o di un account.  
  
 **Crea nuovo account**  
 Consente di creare un nuovo account.  
  
 **Visualizza, modifica o elimina un account esistente**  
 Consente di gestire o eliminare un account esistente.  
  
 **Crea nuovo profilo**  
 Consente di creare un nuovo profilo.  
  
 **Visualizza, modifica o elimina un profilo esistente. È inoltre possibile gestire gli account associati al profilo.**  
 Consente di aggiornare o di eliminare un profilo esistente, nonché di gestire gli account associati al profilo.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="ProfileSecurityPublic"></a> Gestione sicurezza profilo, scheda Pubblico  
 Utilizzare questa pagina per configurare un profilo pubblico.  
  
 I profili sono pubblici o privati. Un profilo privato è accessibile solo a ruoli o utenti specifici, mentre un profilo pubblico può essere usato per l'invio di messaggi di posta elettronica da tutti gli utenti o ruoli che dispongono dell'accesso al database host della posta elettronica (**msdb**).  
  
 Un profilo può essere predefinito. In questo caso, gli utenti o i ruoli possono inviare messaggi di posta elettronica utilizzando il profilo senza specificarlo esplicitamente. Se l'utente o il ruolo che invia il messaggio di posta elettronica dispone di un profilo privato predefinito, Posta elettronica database utilizzerà tale profilo. Se all'utente o ruolo non è associato alcun profilo privato predefinito, **sp_send_dbmail** usa il profilo pubblico predefinito per il database **msdb** . Se non è disponibile un profilo privato predefinito per l'utente o il ruolo oppure un profilo pubblico predefinito per il database, **sp_send_dbmail** restituisce un errore. È possibile contrassegnare come predefinito un unico profilo.  
  
 **Pubblico**  
 Selezionare questa opzione per rendere pubblico il profilo specificato.  
  
 **Profile Name**  
 Consente di visualizzare il nome del profilo.  
  
 **Profilo predefinito**  
 Selezionare questa opzione affinché il profilo specificato sia quello predefinito.  
  
 **Mostra solo profili pubblici esistenti**  
 Selezionare questa opzione per visualizzare solo i profili pubblici disponibili nel database specificato.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="ProfileSecurityPrivate"></a> Gestione sicurezza profilo, scheda Privato  
 Utilizzare questa pagina per configurare un profilo privato.  
  
 I profili sono pubblici o privati. Un profilo privato è accessibile solo a ruoli o utenti specifici, mentre un profilo pubblico può essere usato per l'invio di messaggi di posta elettronica da tutti gli utenti o ruoli che dispongono dell'accesso al database host della posta elettronica (**msdb**).  
  
 Un profilo può essere predefinito. In questo caso, gli utenti o i ruoli possono inviare messaggi di posta elettronica utilizzando il profilo senza specificarlo esplicitamente. Se l'utente o il ruolo che invia il messaggio di posta elettronica dispone di un profilo privato predefinito, Posta elettronica database utilizzerà tale profilo. Se all'utente o ruolo non è associato alcun profilo privato predefinito, **sp_send_dbmail** usa il profilo pubblico predefinito per il database **msdb** . Se non è disponibile un profilo privato predefinito per l'utente o il ruolo oppure un profilo pubblico predefinito per il database, **sp_send_dbmail** restituisce un errore.  
  
 **User name**  
 Consente di selezionare il nome di un utente o di un ruolo nel database **msdb** .  
  
 **Accesso**  
 Consente di specificare se l'utente o il ruolo dispone dell'accesso al profilo specificato.  
  
 **Nome profilo**  
 Consente di visualizzare il nome del profilo.  
  
 **È il profilo predefinito**  
 Consente di specificare se il profilo è il profilo predefinito per l'utente o il ruolo. Ogni utente o ruolo può disporre di un unico profilo predefinito.  
  
 **Mostra solo profili privati esistenti per l'utente**  
 Selezionare questa opzione per visualizzare solo i profili a cui l'utente o il ruolo specificato ha già accesso.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="SystemParameters"></a> Configurazione parametri di sistema  
 Utilizzare questa pagina per specificare i parametri di sistema di Posta elettronica database. Visualizzare i parametri di sistema e i valori correnti di ognuno di essi. Selezionare un parametro per visualizzarne una breve descrizione nel riquadro informazioni.  
  
 **Tentativi account**  
 Numero di tentativi di invio del messaggio di posta elettronica da parte del processo di posta elettronica esterno, utilizzando ogni account nel profilo specificato.  
  
 **Ritardo tentativi account (secondi)**  
 Periodo di tempo, in secondi, per cui il processo di posta elettronica esterno rimane in attesa dopo un tentativo di recapito di un messaggio tramite tutti gli account nel profilo prima di eseguire un altro tentativo utilizzando di nuovo ogni account.  
  
 **Dimensioni massime file (byte)**  
 Dimensioni massime di un allegato, in byte.  
  
 **Estensioni file allegati non consentite**  
 Elenco delimitato da virgole delle estensioni che non possono essere inviate come allegato a un messaggio di posta elettronica. Fare clic sul pulsante Sfoglia ( **...** ) per aggiungere altre estensioni.  
  
 **Durata minima eseguibile Posta elettronica database (secondi)**  
 Periodo minimo di tempo, in secondi, durante il quale il processo di posta elettronica esterno resta attivo. Il processo rimane attivo finché sono presenti messaggi di posta elettronica nella coda di Posta elettronica database. Questo parametro indica il periodo di tempo per cui il processo rimane attivo se non esiste alcun messaggio da elaborare.  
  
 **Livello di registrazione**  
 Consente di specificare i messaggi registrati nel log di Posta elettronica database. I valori possibili sono:  
  
-   Normale - Vengono registrati solo gli errori.  
  
-   Esteso - Vengono registrati gli errori, gli avvisi e i messaggi informativi.  
  
-   Dettagliato - Vengono registrati errori, avvisi, messaggi informativi, messaggi che indicano l'esito positivo delle operazioni e altri messaggi interni. Utilizzare la registrazione dettagliata per la risoluzione dei problemi.  
  
 Il valore predefinito è Esteso.  
  
 **Reimposta tutto**  
 Selezionare questa opzione per reimpostare i valori nella pagina sui valori predefiniti.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="CompleteWizard"></a> Pagina Completamento procedura guidata  
 Usare questa pagina per controllare le azioni che verranno eseguite dalla **Configurazione guidata posta elettronica database** . Non verrà apportata alcuna modifica finché la procedura guidata non verrà completata.  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
###  <a name="TestEmail"></a> Send Test E-Mail Page  
 Usare la finestra di dialogo **Invia messaggio di prova da** _<nome_istanza>_ per inviare un messaggio di posta elettronica usando il profilo di Posta elettronica database specificato. Solo i membri del ruolo predefinito del server **sysadmin** possono inviare messaggi di posta elettronica di prova usando questa pagina.  
  
 **Profilo di Posta elettronica database**  
 Selezionare un profilo di Posta elettronica database nell'elenco. Questo campo è obbligatorio. Se non viene visualizzato alcun profilo, non esiste alcun profilo oppure non si dispone dell'autorizzazione per esso. Per creare e configurare profili, usare la **Configurazione guidata posta elettronica database** . Se non è elencato alcun profilo, utilizzare la Configurazione guidata posta elettronica database per crearne uno.  
  
 **Per**  
 Indirizzo di posta elettronica dei destinatari del messaggio. È necessario specificare almeno un destinatario.  
  
 **Oggetto**  
 Riga dell'oggetto del messaggio di posta elettronica di prova. Modificare l'oggetto predefinito per identificare con più accuratezza il messaggio di posta elettronica per la risoluzione dei problemi.  
  
 **Corpo**  
 Corpo del messaggio di posta elettronica di prova. Modificare l'oggetto predefinito per identificare con più accuratezza il messaggio di posta elettronica per la risoluzione dei problemi.  
  
 La finestra di dialogo **Messaggio di prova di Posta elettronica database** conferma che Posta elettronica database ha provato a inviare il messaggio e viene specificato il valore **mailitem_id** relativo al messaggio di posta elettronica di prova. Verificare con il destinatario se il messaggio di posta elettronica è stato recapitato. In genere, un messaggio di posta elettronica viene ricevuto entro alcuni minuti, ma è possibile che si verifichi un ritardo a causa di prestazioni di rete ridotte, per effetto di un backlog di messaggi in corrispondenza del server di posta elettronica o a seguito di un'indisponibilità temporanea del server. Usare il valore **mailitem_id** per la risoluzione dei problemi.  
  
 **Messaggio inviato**  
 Valore **mailitem_id** del messaggio di posta elettronica di prova.  
  
 **Risoluzione dei problemi**  
 Fare clic su questo pulsante per aprire la documentazione online relativa all'argomento [Risoluzione dei problemi relativi a Posta elettronica database](https://msdn.microsoft.com/library/ms188663.aspx).  
  
 [Configurazione guidata Posta elettronica database](#DBWizard)  
  
##  <a name="Template"></a> Utilizzo di modelli  
 **Per creare uno script di configurazione di Posta elettronica database**  
  
1.  Scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Nella finestra **Esplora modelli** espandere la cartella **Posta elettronica database** .  
  
3.  Fare doppio clic su **Simple Database Mail Configuration**(Configurazione di Posta elettronica database semplice). Il modello verrà visualizzato in una nuova finestra Query.  
  
4.  Scegliere **Imposta valori per parametri modello** dal menu **Query**. Viene visualizzata la finestra **Sostituisci parametri modello** .  
  
5.  Digitare i valori per i parametri **profile_name**, **account_name**, **SMTP_nomeserver**, **email_address**e **display_name**. SQL Server Management Studio compilerà il modello con i valori immessi.  
  
6.  Eseguire lo script per creare la configurazione.  
  
7.  Lo script non concede l'accesso al profilo ad alcun utente del database. Per impostazione predefinita, quindi, il profilo può essere usato solo dai membri del ruolo di sicurezza predefinito **sysadmin**. Per altre informazioni sulla concessione dell'accesso ai profili, vedere [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)  
  
  
