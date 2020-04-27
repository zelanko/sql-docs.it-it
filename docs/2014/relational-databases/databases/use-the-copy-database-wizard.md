---
title: Usare Copia guidata database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.cdw.transfermethod.f1
- sql12.swb.cdw.welcome.f1
- sql12.swb.cdw.packageconfiguration.f1
- sql12.swb.cdw.schedule.f1
- sql12.swb.cdw.destination.f1
- sql12.swb.cdw.complete.f1
- sql12.swb.cdw.destinationconfiguration.f1
- sql12.swb.cdw.selectdatabaseobjects.f1
- sql12.swb.cdw.databases.f1
- sql12.swb.cdw.source.f1
- sql12.swb.cdw.locationofsourcedbfiles.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e72b960db0fd5b733119cafeca98f124eaa15f38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871138"
---
# <a name="use-the-copy-database-wizard"></a>Utilizzo di Copia guidata database
  Tramite Copia guidata database è possibile spostare o copiare con semplicità i database e i relativi oggetti da un server a un altro, senza alcun tempo di inattività del server. È inoltre possibile aggiornare i database da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Mediante questa procedura guidata è possibile effettuare le operazioni seguenti:  
  
-   Selezionare un server di origine e uno di destinazione.  
  
-   Selezionare i database da spostare, copiare o aggiornare.  
  
-   Specificare il percorso di file per il database.  
  
-   Creare account di accesso nel server di destinazione.  
  
-   Copiare ulteriori oggetti di supporto, processi, stored procedure definite dall'utente e messaggi di errore.  
  
-   Pianificare lo spostamento o la copia dei database.  
  
 Oltre a copiare i database, è possibile effettuare la stessa operazione con i metadati associati, ad esempio gli account di accesso e gli oggetti del database **master** necessari per un database copiato.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Utilizzo di Copia guidata database per:**  
  
     [Copiare, spostare o aggiornare i database](#Copy_Move)  
  
-   **Completamento dopo l'aggiornamento:**  
  
     [Dopo l'aggiornamento di un database di SQL Server](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   La Copia guidata database non è disponibile nell'edizione Express.  
  
-   Non è possibile utilizzare Copia guidata database per copiare o spostare i database riportati di seguito.  
  
    -   Database di sistema  
  
    -   Database contrassegnati per la replica.  
  
    -   Database contrassegnati come inaccessibili, offline o sospetti, database in modalità di emergenza o in cui sono in corso operazioni di caricamento o recupero.  
  
-   Dopo aver aggiornato un database, non è possibile effettuarne il downgrade a una versione precedente.  
  
-   Se si seleziona l'opzione **Sposta** , il database di origine verrà automaticamente eliminato dopo lo spostamento del database. Se si seleziona l'opzione **Copia** , il database di origine non verrà eliminato.  
  
-   Se si usa il metodo SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) per spostare il catalogo full-text, è necessario ripopolare l'indice dopo lo spostamento.  
  
-   Il metodo di collegamento e scollegamento consente di scollegare il database, spostare o copiare i file con estensione mdf, ndf e ldf del database e ricollegare quest'ultimo nella nuova posizione. Nel caso di questo metodo, non è possibile collegare sessioni attive al database da spostare o copiare, al fine di evitare la perdita o l'inconsistenza dei dati. Se sono presenti sessioni attive, l'operazione di copia o spostamento non verrà eseguita. Nel caso del metodo SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object), l'utilizzo delle sessioni attive è consentito, poiché il database non viene mai portato offline.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Assicurarsi che SQL Server Agent sia stato avviato nel server di destinazione.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Per garantire prestazioni ottimali del database aggiornato, aggiornare le statistiche eseguendo sp_updatestats (aggiornamento delle statistiche) sul database aggiornato.  
  
-   Quando si copia un database in un'altra istanza del server, per garantire un utilizzo coerente a utenti e applicazioni, potrebbe essere necessario ricreare nell'altra istanza del server alcuni o tutti i metadati per il database, ad esempio account di accesso e processi. Per ulteriori informazioni, vedere [gestire i metadati quando si rende disponibile un database in un'altra istanza del Server &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario essere membri del ruolo predefinito del server **sysadmin** sia nel server di origine sia in quello di destinazione.  
  
##  <a name="copy-move-or-upgrade-databases"></a><a name="Copy_Move"></a>Copiare, spostare o aggiornare i database  
  
1.  In Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere il nodo **Database**, fare clic con il pulsante destro del mouse su un database, scegliere **Attività**, quindi **Copia database**.  
  
2.  Nella pagina **Selezione server di origine** specificare il server in cui si trova il database da spostare o copiare e immettere le informazioni relative all'account di accesso. Dopo aver selezionato il metodo di autenticazione e immesso le informazioni per l'accesso, fare clic su **Avanti** per stabilire la connessione al server di origine. La connessione rimane aperta durante tutta la sessione.  
  
     **Server di origine**  
     Selezionare il nome del server in cui risiedono i database che si desidera spostare o copiare oppure fare clic sul pulsante Sfoglia (**...**) per individuare il server desiderato. La versione del server deve essere almeno [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
     **Usa autenticazione di Windows**  
     Consente a un utente di connettersi tramite un account utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usa autenticazione SQL Server**  
     Consente all'utente di specificare una password e un nome utente dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Nome utente**  
     Immettere il nome utente da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Password**  
     Immettere la password per l'account di accesso. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Avanti**  
     Consente di connettersi al server e di convalidare l'utente. Questo processo consente di controllare se l'utente è un membro del ruolo predefinito del server **sysadmin** nel computer selezionato.  
  
3.  Nella pagina **Selezione server di destinazione** specificare il server in cui verrà spostato o copiato il database. Se si impostano il server di origine e quello di destinazione sulla stessa istanza del server, verrà effettuata una copia di un database. In questo caso, è necessario rinominare il database in un punto successivo della procedura guidata. È possibile utilizzare il nome del database di origine per il database copiato o spostato solo se non si verificano conflitti di nome nel server di destinazione. Se sono presenti conflitti di nome, è necessario risolverli manualmente nel server di destinazione per potervi utilizzare il nome del database di origine.  
  
     **Server di destinazione**  
     Selezionare il nome del server in cui verranno copiati o spostati i database oppure fare clic sul pulsante Sfoglia (**...**) per individuare un server di destinazione.  
  
    > [!NOTE]  
    >  È possibile utilizzare una destinazione costituita da un server cluster. Nella Copia guidata database sarà possibile selezionare solo unità condivise in un server di destinazione cluster.  
  
     **Usa autenticazione di Windows**  
     Consente a un utente di connettersi tramite un account utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usa autenticazione SQL Server**  
     Consente all'utente di specificare una password e un nome utente dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione.  
  
     **Nome utente**  
     Immettere il nome utente da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Password**  
     Immettere la password per l'account di accesso. Questa opzione è disponibile solo se si è scelto di utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Avanti**  
     Consente di connettersi al server e di convalidare l'utente. Questo processo consente di controllare se l'utente dispone delle autorizzazioni elencate in precedenza per i computer selezionati.  
  
4.  Nella pagina **Selezione metodo di trasferimento** selezionare il metodo di trasferimento.  
  
     **Usa metodo di collegamento e scollegamento**  
     Consente di scollegare il database dal server di origine, copiare i file di database (con estensione mdf, ndf e ldf) nel server di destinazione e collegare il database nel server di destinazione. Questo è in genere il metodo più rapido poiché il lavoro principale è rappresentato dalla lettura del disco di origine e dalla scrittura del disco di destinazione. Per creare oggetti strutture di archiviazione dei dati o oggetti all'interno del database non è necessaria alcuna logica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se il database contiene molto spazio allocato ma inutilizzato, questo metodo può risultare più lento. Ad esempio, nel caso di un database nuovo e quasi vuoto creato allocando 100 MB, vengono copiati tutti i 100 MB anche se nel database sono effettivamente utilizzati solo 5 MB.  
  
    > [!NOTE]  
    >  L'utilizzo di questo metodo rende il database non disponibile per gli utenti durante il trasferimento.  
  
     **In caso di errore, ricollega il database di origine**  
     Quando un database viene copiato, i rispettivi file originali vengono sempre ricollegati al server di origine. Utilizzare questa casella per ricollegare i file originali al database di origine se non è possibile completare lo spostamento di un database.  
  
     **Usa metodo SMO (SQL Management Objects)**  
     Questo metodo consente di leggere le definizioni di ogni oggetto di database nel database di origine e di creare ciascun oggetto nel database di destinazione. Consente quindi di trasferire i dati dalle tabelle di origine a quelle di destinazione, ricreando gli indici e i metadati.  
  
    > [!NOTE]  
    >  Gli utenti del database possono continuare ad accedere al database durante il trasferimento.  
  
5.  Nella pagina **Selezione database** selezionare i database che si desidera spostare o copiare dal server di origine a quello di destinazione. Vedere [limitazioni e restrizioni](#Restrictions) nella sezione ' prima di Begin di questo argomento.  
  
     **Spostamento**  
     Consente di spostare il database nel server di destinazione.  
  
     **Copia**  
     Consente di copiare il database nel server di destinazione.  
  
     **origine**  
     Consente di visualizzare i database disponibili nel server di origine.  
  
     **Stato**  
     Se il database può essere spostato, viene visualizzato **OK** . In caso contrario, viene visualizzato il motivo per cui il database non può essere spostato.  
  
     **Aggiorna**  
     Consente di aggiornare l'elenco dei database.  
  
     **Avanti**  
     Consente di avviare il processo di convalida, quindi di visualizzare la schermata successiva.  
  
6.  Nella pagina **Configurazione database di destinazione** modificare il nome del database, se necessario, e specificare il percorso e i nomi dei file di database. Questa pagina viene visualizzata solo una volta per ogni database spostato o copiato.  
  
7.  Nella pagina **Selezione oggetti database** selezionare gli oggetti da spostare o copiare. Questa pagina è disponibile solo se l'origine e la destinazione si trovano in server diversi. Per includere un oggetto, fare clic sul relativo nome nella casella **Oggetti correlati disponibili** , quindi fare clic sul pulsante **>>** per spostare l'oggetto nella casella **Oggetti correlati selezionati** . Per escludere un oggetto, fare clic sul nome dell'oggetto nella casella **oggetti correlati selezionati** , quindi fare ** < ** clic sul pulsante per spostare l'oggetto nella casella **oggetti correlati disponibili** . Per impostazione predefinita, vengono trasferiti tutti gli oggetti di ogni tipo selezionato, ad eccezione degli account di accesso. Per scegliere singoli oggetti di un tipo, fare clic sul pulsante con i puntini di sospensione accanto al tipo di oggetti nella casella **Oggetti correlati selezionati** . Verrà aperta una finestra di dialogo in cui è possibile selezionare i singoli oggetti.  
  
     **Account di accesso (tutti gli account di accesso in fase di esecuzione)**  
     Consente di includere gli account di accesso nell'operazione di spostamento o di copia. L'opzione è selezionata per impostazione predefinita.  
  
     **Stored procedure dal database master**  
     Consente di includere le stored procedure utente del database **master** nell'operazione di copia o spostamento.  
  
    > [!NOTE]  
    >  Le stored procedure estese e le DLL a loro associate non sono idonee alla copia automatizzata.  
  
     **SQL Server Agent - processi**  
     Consente di includere i processi del database **msdb** nell'operazione di copia o spostamento.  
  
     **Messaggi di errore definiti dall'utente**  
     Consente di includere i messaggi di errore definiti dall'utente nell'operazione di copia o spostamento.  
  
     **Endpoint**  
     Consente di includere gli endpoint definiti nel database di origine.  
  
     **Catalogo full-text**  
     Consente di includere i cataloghi full-text del database di origine.  
  
     **Pacchetto SSIS**  
     Consente di includere i pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] definiti nel database di origine.  
  
     **Descrizione**  
     Descrizione dell'oggetto .  
  
8.  Nella pagina **Percorso dei file di database di origine** specificare una condivisione del file system contenente i file di database del server di origine. Questa operazione è necessaria se le istanze dei server di origine e di destinazione si trovano in computer diversi.  
  
     **Database**  
     Consente di visualizzare il nome di ogni database da spostare.  
  
     **Percorso cartella**  
     Consente di specificare il percorso dei file di database di origine nel file system.  
  
     Ad esempio: C:\Programmi\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA  
  
     **Condivisione file nel server di origine**  
     Consente di specificare il percorso dei file del database di origine come percorso di una condivisione file.  
  
     Ad esempio: "\\\\*server_name*\c $ \Programmi\Microsoft SQL Server\MSSQL110. MSSQLSERVER\MSSQL\Data  
  
9. Tramite Copia guidata database è possibile creare un pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] per trasferire il database dalla pagina **Configurazione pacchetto** e, se necessario, personalizzare il pacchetto.  
  
     **Posizione pacchetto**  
     Consente di visualizzare il punto in cui verrà scritto il pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
     **Nome pacchetto**  
     Consente di immettere un nome per il pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
     **Opzioni di registrazione**  
     Consente di indicare se le informazioni di registrazione devono essere archiviate nel registro eventi di Windows o in un file di testo.  
  
     **Percorso file log degli errori**  
     Consente di fornire un percorso per il file di log. Questa opzione è disponibile solo se è selezionata l'opzione per la registrazione di file di testo.  
  
10. Nella pagina **Pianificazione pacchetto** specificare il momento in cui si desidera venga avviata l'operazione di copia o spostamento. Se non si è un amministratore di sistema, è necessario specificare un account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con accesso al sottosistema di esecuzione dei pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS).  
  
     **Esegui immediatamente**  
     L'operazione di spostamento o copia viene avviata dopo aver fatto clic su **Avanti**.  
  
     **Pianificazione**  
     L'operazione di spostamento o copia viene avviata in un secondo momento. Le impostazioni di pianificazione correnti vengono visualizzate nella casella della descrizione. Per modificare la pianificazione fare clic su **Cambia pianificazione**.  
  
     **Modificare**  
     Consente di aprire la finestra di dialogo **Nuova pianificazione processo** .  
  
     **Account proxy Integration Services**  
     Consente di selezionare un account proxy esistente. Per pianificare il trasferimento è necessario che sia disponibile almeno un account proxy per l'utente e che questo sia configurato con l'autorizzazione al sottosistema **esecuzione pacchetti di SQL Server Integration Services** .  
  
     Per creare un account proxy per l'esecuzione di pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] , in Esplora oggetti espandere **SQL Server Agent**, espandere **Proxy**, fare clic con il pulsante destro del mouse su **Esecuzione pacchetto SSIS**e quindi fare clic su **Nuovo proxy**.  
  
     I membri del ruolo predefinito del server **sysadmin** possono selezionare **Account del servizio SQL Server Agent**se dispongono delle autorizzazioni necessarie.  
  
11. Nella pagina **Completamento procedura guidata** rivedere il riepilogo delle opzioni selezionate. È possibile fare clic su **Indietro** per modificare le opzioni Fare clic su **Fine** per creare il database. Durante il trasferimento, nella pagina **Operazione in corso** vengono monitorate le informazioni sullo stato di esecuzione di **Copia guidata database**.  
  
     **Azione**  
     Vengono elencate tutte le azioni eseguite.  
  
     **Stato**  
     Viene indicato se l'azione è stata completata correttamente o meno.  
  
     **Messaggio**  
     Viene fornito qualsiasi messaggio restituito a ogni passaggio.  
  
##  <a name="follow-up-after-upgrading-a-sql-server-database"></a><a name="FollowUp"></a> Completamento: Dopo l'aggiornamento di un database di SQL Server  
 Dopo aver utilizzato Copia guidata database per aggiornare un database da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene reso immediatamente disponibile e aggiornato automaticamente. Se il database include indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che, quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati. Per informazioni sulla visualizzazione o sulla modifica dell'impostazione della proprietà **Opzione di aggiornamento full-text** , vedere [Gestione e monitoraggio della ricerca full-text per un'istanza del server](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 Se il livello di compatibilità di un database utente è 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità era 90 prima dell'aggiornamento, nel database aggiornato questo valore viene impostato su 100, cioè sul livello di compatibilità più basso supportato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
## <a name="see-also"></a>Vedi anche  
 [Aggiornare un database utilizzando le operazioni di scollegamento e collegamento &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Creazione di un proxy di SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  
