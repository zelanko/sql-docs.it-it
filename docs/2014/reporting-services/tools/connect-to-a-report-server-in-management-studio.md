---
title: Eseguire la connessione a un server di report in Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], connections
- connections [Reporting Services], report server
- registering report servers
- report servers [Reporting Services], registering
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93cd0c424a5173539eedfa4d53ac93fa04f5962c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100435"
---
# <a name="connect-to-a-report-server-in-management-studio"></a>Eseguire la connessione a un server di report in Management Studio
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornisce Esplora oggetti, che consente di connettersi a qualsiasi server del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gruppo e di visualizzarne graficamente il contenuto. Per Reporting Services, è possibile utilizzare Esplora oggetti per effettuare le operazioni seguenti:  
  
-   Abilitare le funzionalità del server di report.  
  
-   Impostare i valori predefiniti del server e configurare le definizioni di ruolo.  
  
-   Gestire i processi in esecuzione.  
  
-   Gestire le pianificazioni dei processi.  
  
 È possibile connettersi a un server di report in modalità nativa o in modalità integrata SharePoint. La sintassi della connessione e i tipi di operazioni che è possibile eseguire varieranno a seconda della modalità del server di report e delle autorizzazioni. Se si verificano problemi durante la connessione a un server di report o l'esecuzione di attività specifiche, le autorizzazioni potrebbero non essere sufficienti o il nome del server di report non è stato specificato in modo corretto. Per ulteriori informazioni su autorizzazioni e sintassi della connessione, vedere la tabella alla fine di questo argomento.  
  
 Tenere presente che non è possibile utilizzare Esplora oggetti per visualizzare o gestire contenuto del server di report. La gestione del contenuto viene eseguita mediante Gestione report se il server di report è in esecuzione in modalità nativa o mediante un sito di SharePoint se il server di report è in esecuzione in modalità integrata SharePoint.  
  
 Esplora oggetti consente di aprire connessioni verso più istanze del server nella stessa area di lavoro, purché i server siano registrati nello stesso gruppo. Prima che sia possibile connettersi a un'istanza del server di report in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è necessario registrare il server. Se il server di report si già è registrato, ignorare questo passaggio. Le istruzioni per la registrazione di server di report sono fornite alla fine di questo argomento.  
  
### <a name="to-connect-to-a-native-mode-report-server"></a>Per connettersi a un server di report in modalità nativa  
  
1.  Se Esplora oggetti non è già aperto, selezionarlo dal menu Visualizza.  
  
2.  Fare clic **Connetti** su per visualizzare l'elenco dei tipi di server, quindi selezionare **Reporting Services**.  
  
3.  Nella finestra di dialogo **Connetti al server** immettere il nome dell'istanza del server di report. I nomi delle istanze del server di report si basano sui nomi delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per impostazione predefinita, il nome di un'istanza locale del server di report è il nome del computer. Se il server di report è stato installato come istanza denominata, utilizzare questa sintassi per specificare il server: * \<ServerName>\\ [<\>nomeistanza]*.  
  
4.  Selezionare il tipo di autenticazione. Se si utilizza l'autenticazione di Windows, connettersi utilizzando le proprie credenziali. Se è stata selezionata l'autenticazione di base o quella basata su form, digitare l'account e la password.  
  
5.  Fare clic su **Connetti**. Il server di report verrà visualizzato in Esplora oggetti.  
  
6.  Fare clic con il pulsante destro del mouse sul nodo del server per impostare le proprietà di sistema e valori predefiniti per il server. Per altre informazioni, vedere [Impostare le proprietà di un server di report &#40;Management Studio&#41;](set-report-server-properties-management-studio.md).  
  
### <a name="to-connect-to-a-sharepoint-integrated-mode-report-server"></a>Per connettersi a un server di report in modalità integrata SharePoint  
  
1.  Se Esplora oggetti non è già aperto, selezionarlo dal menu Visualizza.  
  
2.  Fare clic Connetti su per visualizzare l'elenco dei tipi di server, quindi selezionare **Reporting Services**.  
  
3.  Nella finestra di dialogo **Connetti al server** , immettere un URL a un sito di SharePoint. Nell'esempio seguente viene illustrata la sintassi:\<http://web server>\</sites/sito>.  
  
4.  Selezionare il tipo di autenticazione. Se si utilizza l'autenticazione di Windows, connettersi utilizzando le proprie credenziali. Se è stata selezionata l'autenticazione di base o quella basata su form, digitare l'account e la password.  
  
5.  Fare clic su **Connetti**. Il server di report verrà visualizzato in Esplora oggetti.  
  
6.  Fare clic con il pulsante destro del mouse sul nodo del server per impostare le proprietà di sistema e valori predefiniti per il server. Per altre informazioni, vedere [Impostare le proprietà di un server di report &#40;Management Studio&#41;](set-report-server-properties-management-studio.md).  
  
### <a name="to-register-a-report-server"></a>Per registrare un server di report  
  
1.  Se non è possibile connettersi a un server di report, non si dispone delle autorizzazioni di accesso oppure è necessario registrare il server. Per registrare il server, scegliere **Server registrati** dal menu Visualizza.  
  
2.  Fare clic sull'icona di Reporting Services.  
  
3.  Fare clic con il pulsante destro del mouse su **Reporting Services**, scegliere **Nuovo**e quindi fare clic su **Registrazione server**. Verrà visualizzata la finestra di dialogo **Nuova registrazione server** .  
  
4.  In **Nome server**immettere un valore. Il valore da specificare varierà in base alla modalità del server:  
  
    -   Per un server di report in modalità nativa, digitare il nome dell'istanza relativa. I nomi delle istanze del server di report si basano sui nomi delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per impostazione predefinita, il nome di un'istanza locale del server di report è il nome del computer. Se il server di report è stato installato come istanza denominata, utilizzare questa sintassi per specificare il server: * \<ServerName>\\ [<\>nomeistanza]*.  
  
    -   Per un server di report eseguito in modalità integrata SharePoint, il server cui connettersi è il sito di SharePoint cui il server di report è connesso. La connessione al sito di SharePoint è necessaria perché in questo modo è possibile visualizzare i livelli di autorizzazione che controllano l'accesso al contenuto e alle operazioni del server di report. È possibile specificare qualsiasi sito nella raccolta siti. Nell'esempio seguente viene illustrata la sintassi: http://mysharepointsite.  
  
5.  In **Autenticazione**selezionare la modalità di autenticazione da usare per l'accesso al server Web. È necessario selezionare la modalità di autenticazione già in uso nel server di report.  
  
    -   Con le impostazioni di sicurezza predefinite, scegliere **Autenticazione di Windows**.  
  
    -   Se è stata installata e distribuita un'estensione di sicurezza personalizzata, scegliere **Autenticazione basata su form**.  
  
    -   Se il server di report è stato configurato per usare l'autenticazione di base, selezionare **Autenticazione di base**.  
  
    -   Se il server di report è configurato per la modalità integrata SharePoint, scegliere **Autenticazione di Windows**.  
  
6.  Fare clic su **Test** per verificare la connessione.  
  
7.  Quando richiesto, fare clic su **OK**e quindi su **Salva**.  
  
## <a name="connection-syntax-and-permissions"></a>Sintassi della connessione e autorizzazioni  
 Nella tabella seguente vengono riepilogate la sintassi della connessione, le operazioni e le autorizzazioni necessarie per eseguire operazioni specifiche.  
  
 Quando si specifica [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] come tipo di server nella finestra di dialogo **Connetti al server** , è possibile specificare un nome del server di report o un endpoint al servizio Web.  
  
|Server di report di connessione|Attività|Autorizzazioni|  
|----------------|-----------|-----------------|  
|Server di report in modalità nativa, connesso come l'istanza predefinita o denominata:<br /><br /> 
  \<nome server>\<_istanza><br /><br /> La connessione al server di report viene eseguita mediante il provider WMI del server di report.|Visualizzazione e impostazione delle proprietà e dei valori predefiniti del server.<br /><br /> Visualizzazione e annullamento di processi.<br /><br /> Creazione e gestione di pianificazioni condivise.<br /><br /> Creazione, modifica o eliminazione di definizioni di ruolo.|Assegnato al ruolo di Amministratore sistema.|  
|Server di report in modalità nativa, connesso come l'istanza predefinita o denominata tramite l'endpoint al servizio Web ReportServer:<br /><br /> http://\<nomeserver>/ReportServer<br /><br /> La specifica di un URL per server di report fornisce una modalità alternativa per connettersi al server di report.|Visualizzazione e impostazione delle proprietà e dei valori predefiniti del server.<br /><br /> Visualizzazione e annullamento di processi.<br /><br /> Creazione e gestione di pianificazioni condivise.<br /><br /> Creazione, modifica o eliminazione di definizioni di ruolo.|Assegnato al ruolo di Amministratore sistema.|  
|Server di report in modalità integrata SharePoint, connesso mediante il sito di SharePoint:<br /><br /> http://\<webserver>/\<SitoSharePoint>|Visualizzazione e impostazione delle proprietà e dei valori predefiniti del server.<br /><br /> Visualizzazione e annullamento di processi.<br /><br /> Creazione e gestione di pianificazioni condivise definite per il sito cui si è connessi.<br /><br /> Visualizzazione dei livelli di autorizzazione definiti per il sito cui si è connessi.|Livello di autorizzazione Controllo completo sul sito di SharePoint cui si è connessi.|  
|Server di report in modalità integrata SharePoint, connesso mediante il nome dell'istanza del server di report:<br /><br /> 
  \<nome server>\<_istanza>|Visualizzazione e impostazione delle proprietà e dei valori predefiniti del server.<br /><br /> Visualizzazione e annullamento di processi.|Livello di autorizzazione Controllo completo sul sito di SharePoint integrato con il server di report.<br /><br /> Si noti che quando si esegue la connessione al server di report anziché al sito di SharePoint, il numero di attività che è possibile eseguire si riduce in modo significativo. Questa situazione si verifica perché il server di report può restituire solo dati dell'applicazione archiviati o gestiti nel database del server di report e non nella configurazione di SharePoint e in database del contenuto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare una connessione al database del server di report &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services in SQL Server Management Studio &#40;SSRS&#41;](reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
