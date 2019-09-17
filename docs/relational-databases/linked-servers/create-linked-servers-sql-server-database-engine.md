---
title: Creare server collegati (motore di database di SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2015
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdbf53aae89ee6beb8e06fef9c51e1b72e34ab0e
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211334"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>Creazione di server collegati (Motore di database di SQL Server)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  In questo argomento viene illustrato come creare un server collegato e come accedere ai dati da un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La creazione di server collegati consente di utilizzare dati di più origini. Il server collegato non deve essere un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia si tratta di uno scenario comune.  
  
##  <a name="Background"></a> Background  
 il quale consente l'accesso a query distribuite ed eterogenee in origini dati OLE DB. Dopo aver creato un server collegato, le query distribuite possono essere eseguite in questo server e consentono di creare un join di tabelle provenienti da più origini dati. Se il server collegato viene definito come un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile eseguire stored procedure remote.  
  
 Le funzionalità e gli argomenti obbligatori del server collegato possono variare in modo significativo. Tra gli esempi contenuti in questo argomento ne viene fornito uno tipico nel quale però non sono descritte tutte le opzioni. Per altre informazioni, vedere [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
##  <a name="Security"></a> Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
 Quando si utilizzano istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] è richiesta l'autorizzazione **ALTER ANY LINKED SERVER** per il server o l'appartenenza nel ruolo predefinito del server **setupadmin** . Quando si utilizza [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] è richiesta l'autorizzazione **CONTROL SERVER** o l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
##  <a name="Procedures"></a> Come creare un server collegato  
 È possibile utilizzare uno degli elementi seguenti:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>Per creare un server collegato a un'altra istanza di SQL Server tramite SQL Server Management Studio  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti, espandere **Oggetti server**, fare clic con il pulsante destro del mouse su **Server collegati**, quindi **Nuovo server collegato**.  
  
2.  Nella casella **Server collegato** della pagina **Generale** digitare il nome dell'istanza di **SQL Server** a cui si sta eseguendo il collegamento.  
  
     **SQL Server**  
     Consente di identificare il server collegato come istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se per definire un server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] collegato si utilizza questo metodo, il nome specificato in **Server collegato** deve essere quello di rete del server. Inoltre, le eventuali tabelle recuperate dal server provengono dal database predefinito impostato per l'account di accesso del server collegato.  
  
     **Altra origine dati**  
     Specificare un tipo di server OLE DB diverso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La selezione di questa opzione determina l'attivazione delle opzioni sottostanti.  
  
     **Provider**  
     Consente di selezionare un'origine dati OLE DB nella casella di riepilogo. Il provider OLE DB viene registrato nel Registro di sistema con il valore PROGID specificato.  
  
     **Nome prodotto**  
     Consente di specificare il nome del prodotto dell'origine dati OLE DB da aggiungere come server collegato.  
  
     **Origine dati**  
     Consente di digitare il nome dell'origine dati in base alla modalità di interpretazione del provider OLE DB. Se ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], specificare il nome dell'istanza.  
  
     **Stringa provider**  
     Digitare il ProgID univoco del provider OLE DB che corrisponde all'origine dati. Per esempi di stringhe provider valide, vedere [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
     **Percorso**  
     Digitare la posizione del database secondo la modalità di interpretazione del provider OLE DB.  
  
     **Catalogo**  
     Digitare il nome del catalogo da utilizzare durante la connessione al provider OLE DB.  
  
     Per verificare la possibilità di eseguire una connessione a un server collegato, in Esplora oggetti fare clic con il pulsante destro del mouse sul server collegato, quindi scegliere **Test connessione**.  
  
    > [!NOTE]  
    >  Se l'istanza di **SQL Server** è quella predefinita, immettere il nome del computer che ospita l'istanza di **SQL Server**. Se l'istanza di **SQL Server** è un'istanza denominata, immettere il nome del computer e il nome dell'istanza, ad esempio **Contabilità\SQLExpress**.  
  
3.  Nell'area **Tipo di server** selezionare **SQL Server** per indicare che il server collegato è un'altra istanza di **SQL Server**.  
  
4.  Nella pagina **Sicurezza** specificare il contesto di sicurezza che verrà utilizzato quando la connessione al server collegato viene eseguita dall'istanza originale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In un ambiente di dominio in cui gli utenti eseguono la connessione tramite account di dominio personalizzati, la selezione di **Verranno effettuate con il contesto di sicurezza corrente dell'account di accesso** è spesso la soluzione migliore. Quando gli utenti eseguono la connessione all'istanza originale di **SQL Server** utilizzando un account di accesso di **SQL Server** , la scelta ottimale spesso consiste nel selezionare **Verranno effettuate con il contesto di sicurezza seguente**, quindi fornendo le credenziali necessarie per l'autenticazione nel server collegato.  
  
     **Account di accesso locale**  
     Consente di specificare l'ID di accesso locale con cui è possibile connettersi al server collegato. L'account di accesso locale può essere un account basato sull'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un account basato sull'autenticazione di Windows. Utilizzare questo elenco per limitare la connessione a determinati account di accesso o per consentire ad alcuni account di connettersi con un account di accesso diverso.  
  
     **Impersonate**  
     Consente di passare il nome utente e la password dall'account di accesso locale al server collegato. Nel caso dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che nel server remoto esista un account di accesso con un nome e una password identici. Nel caso degli account di accesso Windows, è necessario che l'account di accesso sia valido nel server collegato.  
  
     Per utilizzare la funzionalità di rappresentazione, è indispensabile che la configurazione risponda ai requisiti per la delega.  
  
     **Utente remoto**  
     Usare l'utente remoto per eseguire il mapping di utenti non definiti in **Account di accesso locale**. L' **Utente remoto** deve essere un account di accesso basato sull'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel server remoto.  
  
     **Password remota**  
     Consente di specificare la password dell'Utente remoto.  
  
     **Aggiungi**  
     Consente di aggiungere un nuovo account di accesso locale.  
  
     **Rimuovi**  
     Consente di rimuovere un account di accesso locale esistente.  
  
     **Non verranno effettuate**  
     Consente di specificare che non verrà effettuata una connessione per gli account di accesso non definiti nell'elenco.  
  
     **Verranno effettuate senza un contesto di sicurezza**  
     Consente di specificare che verrà effettuata una connessione senza un contesto di sicurezza per gli account di accesso non definiti nell'elenco.  
  
     **Verranno effettuate con il contesto di sicurezza corrente dell'account di accesso**  
     Consente di specificare che verrà effettuata una connessione con il contesto di sicurezza corrente dell'account di accesso per gli account di accesso non definiti nell'elenco. Se la connessione al server locale è stata effettuata utilizzando l'autenticazione di Windows, per la connessione al server remoto verranno utilizzate le credenziali di Windows. Se la connessione al server locale è stata effettuata utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , per la connessione al server remoto verranno utilizzati il nome e la password dell'account di accesso. In tal caso, è necessario che nel server remoto esista un account di accesso con un nome e una password identici.  
  
     **Verranno effettuate con il contesto di sicurezza seguente**  
     Consente di specificare che verrà effettuata una connessione utilizzando l'account di accesso e la password specificati in **Account di accesso remoto** e **Password** per gli account di accesso non definiti nell'elenco. L'account di accesso remoto deve essere un account di accesso basato sull'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel server remoto.  
  
5.  Facoltativamente, visualizzare o specificare opzioni server, fare clic sulla pagina **Opzioni server**  .  
  
     **Regole di confronto compatibili**  
     Influisce sull'esecuzione delle query distribuite in server collegati. Se questa opzione è impostata su true, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera tutti i caratteri del server collegato compatibili con il server locale, relativamente al set di caratteri e alla sequenza delle regole di confronto oppure al tipo di ordinamento. Ciò consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di inviare al provider i confronti per colonne di tipo carattere. Se questa opzione non è impostata, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valuta sempre i confronti per le colonne di tipo carattere localmente.  
  
     Impostare questa opzione solo se nell'origine dei dati corrispondente al server collegato il set di caratteri e il tipo di ordinamento corrispondono a quelli del server locale.  
  
     **Accesso ai dati**  
     Consente di attivare e disabilitare un server collegato per l'accesso a query distribuite.  
  
     **RPC**  
     Attiva l'esecuzione di chiamate RPC dal server specificato.  
  
     **Chiamate RPC in uscita**  
     Viene abilitata l'esecuzione di chiamate RPC al server specificato.  
  
     **Usa regole di confronto remote**  
     Determina se vengono utilizzate le regole di confronto di una colonna remota o di un server locale.  
  
     Se è true, per le origini dei dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono adottate le regole di confronto delle colonne remote, mentre le regole di confronto specificate nel nome delle regole di confronto vengono utilizzate per origini dei dati diverse da[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Se è false, per le query distribuite vengono sempre utilizzate le regole di confronto predefinite del server locale, mentre il nome delle regole di confronto e le regole di confronto delle colonne remote vengono ignorati. Il valore predefinito è false.  
  
     **Nome regole di confronto**  
     Consente di specificare il nome delle regole di confronto utilizzate dall'origine dei dati remota quando l'opzione Usa regole di confronto remote è true e l'origine dei dati non è un'origine dei dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È necessario specificare il nome di uno dei set di regole di confronto supportate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Utilizzare questa opzione per accedere a un'origine dei dati OLE DB diversa da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]che utilizza regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Il server collegato deve supportare regole di confronto singole da utilizzare per tutte le colonne del server. Non impostare questa opzione quando il server collegato supporta più regole di confronto nella stessa origine dei dati oppure non è possibile stabilire se le regole di confronto del server collegato corrispondono a una delle regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Connection Timeout**  
     Valore di timeout espresso in secondi per la connessione al server collegato.  
  
     Se il valore è 0, usare il valore predefinito **sp_configure** dell'opzione [remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) .  
  
     **Timeout query**  
     Valore di timeout espresso in secondi per le query eseguite nel server collegato.  
  
     Se 0, usare il valore predefinito **sp_configure** dell'opzione [remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) .  
  
     **Abilita promozione delle transazioni distribuite**  
     Questa opzione consente di proteggere le azioni di una procedura da server a server tramite una transazione MS DTC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator). Quando questa opzione è impostata su TRUE, la chiamata di una stored procedure remota comporta l'avvio di una transazione distribuita e l'integrazione della transazione in MS DTC. Per altre informazioni, vedere [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).  
  
6.  Fare clic su **OK**.  
  
##### <a name="to-view-the-provider-options"></a>Per visualizzare le opzioni del provider  
  
-   Per visualizzare le opzioni rese disponibili dal provider, fare clic sulla pagina **Opzioni provider** .  
  
     Non tutti i provider dispongono delle stesse opzioni. Ad esempio, alcuni tipi di dati, a differenza di altri, dispongono di indici. Utilizzare questa finestra di dialogo per consentire a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di capire le funzionalità del provider. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installa alcuni provider di dati comuni; tuttavia, quando il prodotto che fornisce i dati cambia, il provider installato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe non supportare tutte le funzionalità nuove. La migliore fonte di informazioni sulle funzionalità del prodotto che fornisce i dati è la documentazione di quel prodotto.  
  
     **Parametro dinamico**  
     Indica che il provider consente l'utilizzo della sintassi con il marcatore di parametro "?" nel caso di query con parametri. Impostare questa opzione solo se il provider supporta l'interfaccia **ICommandWithParameters** e "?" come marcatore di parametro. L'impostazione di questa opzione consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di eseguire query con parametri sul provider. In determinati casi, la possibilità di eseguire query con parametri sul provider può determinare un miglioramento delle prestazioni.  
  
     **Query nidificate**  
     Indica che il provider supporta le istruzioni `SELECT` nidificate nella clausola FROM. L'impostazione di questa opzione consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di delegare al provider le query che richiedono la nidificazione di istruzioni SELECT nella clausola FROM.  
  
     **Solo livello zero**  
     Indica che sul provider vengono richiamate solo le interfacce OLE DB di livello 0.  
  
     **Consenti in-process**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la creazione di un'istanza del provider come server in-process. Se questa opzione non viene impostata, per impostazione predefinita viene creata un'istanza del provider al di fuori del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La creazione di un'istanza del provider al di fuori del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di proteggere il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dagli errori che si verificano nel provider. Quando l'istanza del provider viene creata al di fuori del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , gli aggiornamenti o gli inserimenti che fanno riferimento a colonne per valori di grandi dimensioni (**text**, **ntext**o **image**) non sono consentiti.  
  
     **Aggiornamenti non in transazioni**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente gli aggiornamenti anche se **ITransactionLocal** non è disponibile. Se questa opzione è abilitata, gli aggiornamenti sul provider non sono recuperabili poiché il provider non supporta le transazioni.  
  
     **Indici come percorso di accesso**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di usare gli indici del provider per recuperare i dati. Per impostazione predefinita, gli indici vengono utilizzati solo per i metadati e non vengono mai aperti  
  
     **Accesso ad hoc non consentito**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente l'accesso ad hoc tramite le funzioni OPENROWSET e OPENDATASOURCE sul provider OLE DB. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente l'accesso ad hoc anche se questa opzione non è impostata.  
  
     **Supporta l'operatore 'Like'**  
     Indica che il provider supporta le query che utilizzano la parola chiave LIKE.  
  
###  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Per creare un server collegato con [!INCLUDE[tsql](../../includes/tsql-md.md)], usare le istruzioni [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) e [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Per creare un server collegato a un'altra istanza di SQL Server tramite Transact-SQL  
  
1.  Nell'Editor query immettere il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente per il collegamento a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominata `SRVR002\ACCTG`:  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  Eseguire il codice riportato di seguito per configurare il server collegato in modo da utilizzare le credenziali di dominio dell'account di accesso utilizzate dal server collegato.  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> Completamento: Passaggi da effettuare dopo aver creato un server collegato  
  
#### <a name="to-test-the-linked-server"></a>Per testare il server collegato  
  
-   Eseguire il codice riportato di seguito per testare la connessione al server collegato. In questo esempio vengono restituiti i nomi dei database nel server collegato.  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>Scrittura di una query che consente creare un join di tabelle di un server collegato  
  
-   Utilizzare nomi in quattro parti per fare riferimento a un oggetto in un server collegato. Eseguire il codice riportato di seguito per restituire un elenco di tutti gli account di accesso nel server locale e i relativi account di accesso corrispondenti nel server collegato.  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     Quando viene restituito NULL per l'account di accesso del server collegato, tale account di accesso non è presente nel server collegato. Questi account di accesso non potranno essere utilizzati dal server collegato a meno tale server non sia configurato per passare un contesto di sicurezza differente oppure il server collegato accetta connessioni anonime.  
  
## <a name="see-also"></a>Vedere anche  
 [Server collegati &#40;Motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
