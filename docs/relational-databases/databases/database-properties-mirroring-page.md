---
title: Proprietà database (pagina Mirroring) | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
author: stevestein
ms.author: sstein
ms.openlocfilehash: a25b2b40b147cd0bd23e8c7554e548b6a577d539
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68099587"
---
# <a name="database-properties-mirroring-page"></a>Proprietà database (pagina Mirroring)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Accedere a questa pagina dal database principale e utilizzarla per configurare e modificare le proprietà del mirroring del database per un database. Utilizzare inoltre la pagina per avviare la Configurazione guidata sicurezza mirroring del database, per visualizzare lo stato di una sessione di mirroring e per sospendere o rimuovere la sessione di mirroring del database.  
  
> **IMPORTANTE** La sicurezza deve essere configurata prima dell'avvio del mirroring. Se il mirroring non è stato avviato, è necessario iniziare dalla procedura guidata. Le caselle di testo della pagina **Mirroring** sono disabilitate fino al termine della procedura guidata.  
  
 **Configurare il mirroring del database usando SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>Opzioni  
 **Configura sicurezza**  
 Fare clic sul pulsante per avviare la **Configurazione guidata sicurezza mirroring del database**  
  
 Se la procedura guidata viene completata, l'azione eseguita dipende dallo stato del mirroring come illustrato di seguito:  
  
|||  
|-|-|  
|Se il mirroring non è stato avviato.|La pagina delle proprietà memorizza nella cache le informazioni di connessione nonché un valore che indica se nel database mirror è impostata la proprietà del partner.<br /><br /> Al termine della procedura guidata, viene richiesto di avviare il mirroring del database utilizzando gli indirizzi di rete del server e la modalità operativa predefiniti. Se è necessario modificare gli indirizzi o la modalità operativa, fare clic su **Non avviare il mirroring**.|  
|Se il mirroring è stato avviato.|Se il server di controllo del mirroring è stato cambiato nella procedura guidata, viene impostato di conseguenza.|  
  
 **Indirizzi di rete del server**  
 Esiste un'opzione equivalente per ognuna delle istanze del server, ovvero **Server principale**, **Server mirror**e **Server di controllo del mirroring**.  
  
 Gli indirizzi di rete del server delle istanze del server sono specificati automaticamente al completamento della Configurazione guidata sicurezza mirroring del database. Dopo aver completato la procedura guidata, è possibile modificare gli indirizzi di rete manualmente, se necessario.  
  
 L'indirizzo di rete del server segue la sintassi di base illustrata di seguito:  
  
 TCP **://** _fully_qualified_domain_name_ **:** _port_  
  
 dove  
  
-   *fully_qualified_domain_name* è il server sul quale si trova l'istanza del server.  
  
-   *port* è la porta assegnata all'endpoint di mirroring del database dell'istanza del server.  
  
     Per la partecipazione di un server al mirroring del database è necessario un endpoint di mirroring del database. Quando si utilizza la Configurazione guidata sicurezza mirroring del database per stabilire la prima sessione di mirroring per un'istanza del server, la procedura guidata crea automaticamente l'endpoint e lo configura per utilizzare l'autenticazione di Windows. Per altre informazioni sull'uso della procedura guidata con l'autenticazione basata su certificati, vedere [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md).  
  
    >**IMPORTANTE**  Per ogni istanza del server è necessario un solo endpoint di mirroring del database, indipendentemente dal numero di sessioni di mirroring da supportare.  
  
 Ad esempio, l'indirizzo di rete per un'istanza del server su un computer denominato `DBSERVER9` il cui endpoint utilizza la porta `7022`potrebbe essere:  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 Per altre informazioni, vedere [Specificare un indirizzo di rete del server &#40;Mirroring del database&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
> **NOTA:** Non è possibile cambiare le istanze del server principale né del server mirror durante una sessione di mirroring del database. È invece possibile cambiare l'istanza del server di controllo del mirroring durante una sessione. Per ulteriori informazioni, vedere la sezione "Note" più avanti in questo argomento.  
  
 **Avvia mirroring**  
 Fare clic su questo pulsante per avviare il mirroring se sussistono tutte le condizioni seguenti:  
  
-   Il database mirror deve esistere.  
  
     Prima di avviare il mirroring è necessario creare il database mirror ripristinando un backup completo recente con WITH NORECOVERY e ripristinando eventualmente i backup del log del database principale sul server mirror. Per altre informazioni, vedere [Preparazione di un database mirror per il mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Gli indirizzi TCP delle istanze dei server principale e mirror sono già specificati nella sezione **Indirizzi di rete del server** .  
  
-   Se la modalità operativa è impostata su protezione elevata con failover automatico (sincrona), viene specificato inoltre l'indirizzo TCP dell'istanza del server mirror.  
  
-   La sicurezza è stata configurata correttamente.  
  
 Fare clic su **Avvia mirroring** per iniziare la sessione. Il Motore di database tenta di connettersi automaticamente al partner per il mirroring per verificare che il server mirror sia configurato correttamente e per avviare la sessione di mirroring. Se è possibile avviare il mirroring, viene creato un processo per monitorare il database.  
  
 **Sospendi** o **Riprendi**  
 Durante una sessione di mirroring del database, fare clic su **Sospendi** per sospendere la sessione. Verrà richiesta una conferma. Se si fa clic su **Sì**la sessione viene sospesa e il pulsante diventa **Riprendi**. Per riprendere la sessione fare clic su **Riprendi**.  
  
 Per informazioni sull'impatto della sospensione di una sessione, vedere [Sospensione e ripresa del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md).  
  
> **IMPORTANTE** In un servizio forzato, quando il server principale originale esegue nuovamente la connessione il mirroring viene sospeso. Se si riprende il mirroring in questa situazione, è possibile che si verifichi una perdita di dati nel server principale originale. Per informazioni sulla gestione della potenziale perdita di dati, vedere [Cambio di ruolo durante una sessione di mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
 **Rimuovi mirroring**  
 Sull'istanza del server principale, fare clic per arrestare la sessione e rimuovere la configurazione del mirroring dai database. Verrà richiesta una conferma. Se si fa clic su **Sì**, la sessione verrà arrestata e il mirroring rimosso. Per informazioni sull'impatto della rimozione del mirroring del database, vedere [Rimozione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
> **NOTA:** se si tratta dell'unico database con mirroring sull'istanza del server, il processo di monitoraggio viene rimosso.  
  
 **Failover**  
 Fare clic per eseguire manualmente il failover del database principale sul database mirror.  
  
> **NOTA:** se la sessione di mirroring è in esecuzione in modalità a prestazioni elevate, il failover manuale non è supportato. Per eseguire il failover manualmente, è prima necessario modificare la modalità operativa in **Protezione elevata senza failover automatico (sincrona)** . Dopo il completamento del failover è possibile reimpostare la modalità su **Prestazioni elevate (asincrona)** per la nuova istanza del server principale.  
  
 Verrà richiesta una conferma. Se si fa clic su **Sì**, verrà tentato il failover. Il server principale prova a connettersi al server mirror utilizzando l'autenticazione di Windows. Se l'autenticazione di Windows non funziona, sul server principale viene visualizzata la finestra di dialogo **Connetti al server** . Se il server mirror usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare **Autenticazione di SQL Server** nella casella **Autenticazione** . Nella casella di testo **Account di accesso** specificare l'account di accesso con cui connettersi al server mirror e nella casella di testo **Password** specificare la password per tale account.  
  
 Se il failover ha esito positivo, la finestra di dialogo **Proprietà database** viene chiusa. I ruoli del server principale e mirror vengono scambiati. Il database mirror precedente diventa il database principale e viceversa. Si noti che la finestra di dialogo **Proprietà database** diventa immediatamente non disponibile nel precedente database principale perché quest'ultimo è diventato il database mirror. La finestra di dialogo risulterà disponibile nel nuovo database principale dopo il failover.  
  
 Se il failover non riesce, viene visualizzato un messaggio di errore e la finestra di dialogo rimane aperta.  
  
> **IMPORTANTE** Se si fa clic su **Failover** dopo avere modificato alcune proprietà nella finestra di dialogo **Proprietà database** , le modifiche apportate verranno perse. Per salvare le modifiche correnti fare clic su **No** alla richiesta di conferma e quindi fare clic su **OK** per salvare le modifiche. Riaprire quindi la finestra di dialogo relativa alle proprietà del database e fare clic su **Failover**.  
  
 **Modalità operativa**  
 Facoltativamente, è possibile cambiare modalità operativa. La disponibilità di determinate modalità operative dipende dal fatto che sia stato specificato un indirizzo TCP per un server di controllo del mirroring. descritte di seguito:  
  
|Opzione|Server di controllo del mirroring?|Spiegazione|  
|------------|--------------|-----------------|  
|**Prestazioni elevate (asincrona)**|Null (se presente, non usato ma la sessione richiede un quorum)|Per massimizzare le prestazioni, il database mirror rimane sempre un passo indietro rispetto al database principale. La distanza tra i database è tuttavia solitamente ridotta. La perdita di un partner produce l'effetto seguente:<br /><br /> Se l'istanza del server mirror diventa non disponibile, le attività continuano nel server principale.<br /><br /> Se l'istanza del server principale diventa non disponibile, il server mirror si arresta. Tuttavia, se la sessione è priva di server di controllo del mirroring (opzione consigliata) o se il server di controllo del mirroring è connesso al server mirror, quest'ultimo rimane accessibile come standby a caldo (warm standby). Il proprietario del database può forzare il servizio sull'istanza del server mirror (con possibile perdita di dati).|  
|**Protezione elevata senza failover automatico (sincrona)**|No|Tutte le transazioni di cui è stato eseguito il commit vengono scritte nel disco del server mirror.<br /><br /> Il failover manuale è possibile se i partner sono connessi tra loro.<br /><br /> La perdita di un partner produce l'effetto seguente:<br /><br /> Se l'istanza del server mirror diventa non disponibile, le attività continuano nel server principale.<br /><br /> Se l'istanza del server principale diventa non disponibile, il mirror si arresta ma è disponibile come standby a caldo (warm standby). Il proprietario del database può forzare il servizio sull'istanza del server mirror (con possibile perdita di dati).|  
|**Protezione elevata con failover automatico (sincrona)**|Sì (obbligatorio)|Disponibilità massimizzata mediante l'utilizzo di un'istanza del server di controllo del mirroring per supportare il failover automatico. Si noti che è possibile selezionare l'opzione **Protezione elevata con failover automatico (sincrona)** solo se è già stato specificato un indirizzo del server di controllo del mirroring.<br /><br /> Il failover manuale è sempre possibile se i partner sono connessi tra loro.<br /><br /> **&#42;&#42; Importante &#42;&#42;** Se il server di controllo del mirroring viene disconnesso, è necessario che i partner siano connessi tra loro affinché il database sia disponibile. Per altre informazioni, vedere [Quorum: Impatto di un server di controllo del mirroring sulla disponibilità del database &#40;mirroring del database&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).<br /><br /> Nelle modalità operative sincrone, per tutte le transazioni con commit è garantita la scrittura su disco sul server mirror. In presenza di un server di controllo del mirroring, la perdita di un partner produce l'effetto seguente:<br /><br /> Se l'istanza del server principale diventa non disponibile, si verifica il failover automatico. L'istanza del server mirror passa al ruolo del server principale e il database del server mirror viene considerato come database principale.<br /><br /> Se l'istanza del server mirror diventa non disponibile, le attività continuano nel server principale.<br /><br /> <br /><br /> Per altre informazioni, vedere [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).|  
  
 Dopo l'avvio del mirroring, è possibile cambiare la modalità operativa e salvare la modifica scegliendo **OK**.  
  
 Per altre informazioni, vedere [Modalità di funzionamento del mirroring del database](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **Status**  
 Dopo l'inizio del mirroring, il pannello **Stato** visualizza lo stato della sessione di mirroring del database al momento della selezione della pagina **Mirroring** . Per aggiornare il pannello **Stato** fare clic sul pulsante **Aggiorna** . Gli stati possibili sono indicati di seguito:  
  
|Stati|Spiegazione|  
|------------|-----------------|  
|**Il database non è stato configurato per il mirroring**|Non esiste alcuna sessione di mirroring del database e non ci sono attività da segnalare nella pagina **Mirroring** .|  
|**Sospeso**|Il database principale è disponibile, ma non viene inviato alcun log al server mirror.|  
|**Nessuna connessione**|L'istanza del server principale non può connettersi al proprio partner.|  
|**Sincronizzazione in corso**|Il contenuto del database mirror è in ritardo rispetto a quello del database principale. L'istanza del server principale invia record di log all'istanza del server mirror, che applica le modifiche al database mirror per eseguirne il rollforward.<br /><br /> All'avvio della sessione di mirroring del database, i database mirror e principale sono in questo stato.|  
|**Failover**|Sull'istanza del server principale, è stato avviato un failover manuale (cambio di ruolo) e il server è attualmente in fase di transizione al ruolo mirror. In questo stato, le connessioni utente al database principale vengono terminate rapidamente e il database assume il ruolo di mirror subito dopo.|  
|**Identità sincronizzate**|Quando il server mirror è sufficientemente aggiornato rispetto al server principale, lo stato del database diventa **Sincronizzato**. Il database resta in questo stato fino a quando il server principale continua a inviare modifiche al server mirror e quest'ultimo continua ad applicare le modifiche al database mirror.<br /><br /> Per la modalità a protezione elevata il failover è possibile, senza perdita di dati.<br /><br /> In modalità a prestazioni elevate è possibile che si verifichi la perdita di dati anche nello stato **Sincronizzato** .|  
  
 Per altre informazioni, vedere [Stati di mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).  
  
 **Aggiorna**  
 Fare clic su questo pulsante per aggiornare la casella **Stato** .  
  
## <a name="remarks"></a>Osservazioni  
 Se non si ha familiarità con il mirroring del database, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
### <a name="adding-a-witness-to-an-existing-session"></a>Aggiunta di un server di controllo del mirroring a una sessione esistente  
 È possibile aggiungere un server di controllo del mirroring a una sessione esistente o sostituire un server di controllo del mirroring esistente. Se si conosce l'indirizzo di rete del server di controllo del mirroring, è possibile immetterlo manualmente nel campo **Server di controllo del mirroring** . In caso contrario, utilizzare Configurazione guidata sicurezza mirroring del database per configurare il server di controllo del mirroring. Dopo aver inserito l'indirizzo nel campo, verificare che l'opzione **Protezione elevata con failover automatico (sincrona)** sia selezionata.  
  
 Dopo aver configurato un nuovo server di controllo del mirroring, è necessario fare clic su **OK** per aggiungerlo alla sessione di mirroring.  
  
 **Per aggiungere un server di controllo del mirroring utilizzando autenticazione di Windows**  
  
 [Aggiunta o sostituzione di un server di controllo del mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>Rimozione di un server di controllo del mirroring  
 Per rimuovere un server di controllo del mirroring, eliminare il relativo indirizzo di rete dal campo **Server di controllo del mirroring** . Se si passa dalla modalità a protezione elevata con failover automatico alla modalità a prestazioni elevate, il contenuto del campo **Server di controllo del mirroring** viene automaticamente cancellato.  
  
 Dopo aver rimosso il server di controllo del mirroring, è necessario fare clic su **OK** per rimuoverlo dalla sessione di mirroring.  
  
### <a name="monitoring-database-mirroring"></a>Monitoraggio del mirroring del database  
 Per monitorare i database con mirroring su un'istanza del server, è possibile usare Monitoraggio mirroring del database o la stored procedure di sistema sp_dbmmonitorresults.  
  
 **Per monitorare i database con mirroring**  
  
-   [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 Per altre informazioni, vedere [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Specificare un indirizzo di rete del server &#40;Mirroring del database&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza trasporto per il mirroring del database e i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Cambio di ruolo durante una sessione di mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Sospensione e ripresa del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [Rimozione del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Server di controllo del mirroring del database](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
