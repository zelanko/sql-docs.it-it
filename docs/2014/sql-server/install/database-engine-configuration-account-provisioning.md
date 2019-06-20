---
title: Configurazione del motore di database - Provisioning Account | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 300e3dd81ae7a3de2361c79864130c1361c19588
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095868"
---
# <a name="database-engine-configuration---account-provisioning"></a>Configurazione Motore di database - Provisioning account
  Utilizzare questa pagina per impostare la modalità di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiungere utenti o gruppi di Windows come amministratori del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Considerazioni sull'esecuzione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]viene eseguito il provisioning del gruppo **BUILTIN\Administrators** come account di accesso nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] e i membri del gruppo Administrators locale possono accedere usando le credenziali di amministratore. L'utilizzo di autorizzazioni elevate non è una procedura consigliata. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non viene eseguito il provisioning del gruppo **BUILTIN\Administrators** come account di accesso. Di conseguenza, è consigliabile creare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni utente amministrativo e aggiungere tale account al ruolo predefinito del server sysadmin durate l'installazione di una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. È consigliabile eseguire questa operazione anche per gli account di Windows utilizzati per eseguire i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, inclusi i processi dell'agente di replica.  
  
## <a name="options"></a>Opzioni  
 **Modalità di sicurezza** : selezionare l'autenticazione di Windows o l'autenticazione mista per l'istallazione.  
  
 **Provisioning entità Windows** : nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]il gruppo locale Builtin\Administrator di Windows era incluso nel ruolo del server sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e consentiva agli amministratori di Windows di accedere in modo efficace all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]il gruppo Builtin\Administrator non è disponibile nel ruolo del server sysadmin. Al contrario, è necessario eseguire in modo esplicito il provisioning degli amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le nuove installazioni durante l'esecuzione del programma di installazione.  
  
> [!IMPORTANT]  
>  È necessario eseguire il provisioning esplicito degli amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le nuove installazioni durante l'esecuzione del programma di installazione. Se non si completa questo passaggio, non sarà possibile procedere con l'installazione.  
  
 **Specifica amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: è necessario specificare almeno un'entità di Windows per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiungere l'account usato per l'esecuzione del programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic sul pulsante **Utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Dopo avere modificato l'elenco, scegliere **OK**, quindi verificare l'elenco di amministratori nella finestra di dialogo di configurazione. Quando l'elenco è completo, scegliere **Avanti**.  
  
 Se si seleziona l'autenticazione Modalità mista, è necessario fornire credenziali di accesso per l'account amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modalità di autenticazione di Windows**  
 Quando un utente si connette utilizzando un account utente di Windows, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il nome di account e la password vengono convalidati tramite il token dell'entità di Windows nel sistema operativo. Si tratta della modalità di autenticazione predefinita e garantisce maggiore protezione rispetto alla modalità mista. L'autenticazione di Windows, per la quale viene utilizzato il protocollo di sicurezza Kerberos, garantisce l'applicazione dei criteri password mediante convalida della complessità delle password, fornisce supporto per il blocco dell'account e supporta la scadenza delle password.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Non impostare mai password vuote o vulnerabili.  
  
 **Modalità mista (autenticazione di Windows o autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
 Consente agli utenti di connettersi tramite l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Gli utenti che utilizzano un account utente di Windows per la connessione possono utilizzare connessioni trusted convalidate da Windows.  
  
 Se è necessario selezionare l'autenticazione Modalità mista e utilizzare account di accesso SQL per le applicazioni legacy, sarà necessario impostare password complesse per tutti gli account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  L'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile solo per la compatibilità con le versioni precedenti. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Immettere la password**  
 Immettere e confermare l'account di accesso dell'amministratore di sistema (sa). Le password rappresentano la prima forma di difesa contro eventuali intrusi, pertanto l'impostazione di password complesse costituisce una misura di sicurezza fondamentale per la sicurezza del sistema. Non impostare mai password dell'account "sa" vuote o vulnerabili.  
  
> [!NOTE]  
>  Le password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono contenere da 1 a 128 caratteri, inclusa qualsiasi combinazione di lettere, simboli e numeri. Se si seleziona l'autenticazione Modalità mista, sarà necessario immettere una password dell'account sa complessa prima di passare alla pagina successiva dell'Installazione guidata.  
  
 **Linee guida per la creazione di password complesse**  
 Le password complesse non vengono decifrate facilmente, né da parte degli utenti né mediante l'utilizzo di programmi specifici. Le password complesse non prevedono l'utilizzo di termini o condizioni non consentite, quali:  
  
-   Condizione di spazio vuoto o NULL  
  
-   'Password'  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   'sysadmin'  
  
 Una password complessa non può essere costituita dagli elementi seguenti associati al computer di installazione:  
  
-   Nome dell'utente attualmente connesso al computer.  
  
-   Nome del computer.  
  
 Una password complessa deve essere formata da più di otto caratteri e soddisfare almeno tre dei quattro criteri seguenti:  
  
-   Deve contenere lettere maiuscole.  
  
-   Deve contenere lettere minuscole.  
  
-   Deve contenere numeri.  
  
-   Deve contenere caratteri non alfanumerici, ad esempio #, % o ^.  
  
 Le password immesse in questa pagina devono soddisfare i requisiti relativi ai criteri password complessi. In presenza di qualsiasi componente di automazione in cui viene utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , assicurarsi che la password soddisfi i requisiti relativi ai criteri password complessi.  
  
## <a name="related-content"></a>Contenuto correlato  
 Per ulteriori informazioni sulla scelta tra l'autenticazione di Windows e l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere l'argomento **Scegliere una modalità di autenticazione** nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per altre informazioni sulla scelta di un account per l'esecuzione del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], vedere l'argomento **Configurare account di servizio e autorizzazioni di Windows** nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
