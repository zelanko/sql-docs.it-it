---
title: Procedura guidata Genera e pubblica script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.generatescriptswizard.setscriptingoptions.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql12.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql12.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql12.swb.generatescriptswizard.summarypage.f1
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql12.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
- sql12.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql12.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql12.swb.generatescriptswizard.introduction.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql12.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.choosetables.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b3bb00837c4c3e8e6fae187a902d95c54736882
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063985"
---
# <a name="generate-and-publish-scripts-wizard"></a>Genera e pubblica script
  È possibile usare la procedura guidata **Genera e pubblica script** per creare script per il trasferimento di un database tra le istanze del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. È possibile generare script per un database in un'istanza del motore di database nella rete locale o da [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Gli script generati possono essere eseguiti in un'altra istanza del motore di database o in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. È inoltre possibile usare la procedura guidata per pubblicare direttamente il contenuto di un database in un servizio Web creato tramite Database Publishing Services. È possibile creare script per un intero database o limitare la creazione a oggetti specifici.  
  
1.  **Prima di iniziare:**  [La pubblicazione in un servizio ospitato](#PubHostSvc), [autorizzazioni](#Permissions)  
  
2.  **Per generare o pubblicare uno script, utilizzando:**  [Genera e pubblica script](#GenPubScriptWiz)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 I database di origine e di destinazione possono trovarsi in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] eseguita in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva.  
  
###  <a name="PubHostSvc"></a> Pubblicazione in un servizio ospitato  
 Oltre a creare script, la procedura guidata **Genera e pubblica script** può essere usata per pubblicare un database in un tipo specifico di servizio Web di SQL Server ospitato. SQL Server Hosting Toolkit include Database Publishing Services come progetto di origine condiviso su CodePlex. Il progetto Database Publishing Services può essere usato dai provider di hosting Web per compilare un set di servizi Web per facilitare la distribuzione di database nel servizio Web da parte dei clienti. Per altre informazioni sul download di SQL Server Hosting Toolkit, vedere [Database Publishing Services di SQL Server](https://go.microsoft.com/fwlink/?LinkId=142025).  
  
 Per pubblicare un database in un servizio di hosting Web, selezionare l'opzione **Pubblica su servizio Web** nella pagina **Imposta opzioni di generazione script** della procedura guidata.  
  
###  <a name="Permissions"></a> Autorizzazioni  
 L'autorizzazione minima per pubblicare un database è l'appartenenza al ruolo predefinito del database db_ddladmin per il database di origine. L'autorizzazione minima per pubblicare uno script del database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al provider di hosting è l'appartenenza al ruolo predefinito del database db_ddladmin sul database di destinazione.  
  
 È inoltre necessario fornire un nome utente e una password per accedere all'account del provider di hosting ed eseguire la pubblicazione guidata. Il database di destinazione deve essere creato nel provider di hosting prima della pubblicazione del database di origine. La pubblicazione sovrascrive gli oggetti presenti nel database esistente.  
  
##  <a name="GenPubScriptWiz"></a> Utilizzo della procedura guidata Genera e pubblica script  
 **Per generare o pubblicare uno script**  
  
1.  In **Esplora oggetti**espandere il nodo dell'istanza contenente il database per il quale generare lo script.  
  
2.  Scegliere **Attività**, quindi fare clic su **Genera script**.  
  
3.  Completare le finestre di dialogo della procedura guidata.  
  
    -   [Pagina Introduzione](#Introduction)  
  
    -   [Pagina Seleziona oggetti](#ChooseObjects)  
  
    -   [Pagina Imposta opzioni di generazione script](#SetScriptOpt)  
  
    -   [Pagina Opzioni di generazione script avanzate](#AdvScriptOpt)  
  
    -   [Pagina Gestisci provider](#MgProviders)  
  
    -   [Pagina Opzioni di pubblicazione avanzate](#AdvPubOpts)  
  
    -   [Pagina Configurazione del provider](#ProvConfig)  
  
    -   [Pagina Riepilogo](#Summary)  
  
    -   [Pagina Salva o pubblica script](#SavePubScripts)  
  
###  <a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per la generazione o la pubblicazione di uno script.  
  
 **Non visualizzare più questa pagina**: consente di non visualizzare più questa pagina al successivo avvio della procedura guidata **Genera e pubblica script**.  
  
 **Avanti >**: consente di passare alla pagina **Seleziona metodo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza generare o pubblicare uno script dal database.  
  
###  <a name="ChooseObjects"></a> Pagina Seleziona oggetti  
 Usare questa pagina per scegliere quali oggetti si desidera includere negli script generati dalla procedura guidata. Nella pagina successiva della procedura guidata, è possibile salvare gli script nel percorso desiderato oppure usarli per pubblicare oggetti di database su un provider di hosting Web remoto in cui sia installato [Database Publishing Services di SQL Server](https://go.microsoft.com/fwlink/?LinkId=142025).  
  
 **Opzione Genera script per intero database** : fare clic per generare script per tutti gli oggetti nel database e includere uno script per il database stesso.  
  
 **Seleziona oggetti di database specifici** : fare clic per limitare la generazione degli script solo agli oggetti specifici nel database prescelto:  
  
-   **Oggetti di database** : consente di selezionare almeno un oggetto da includere nello script.  
  
-   **Seleziona tutto** : consente di selezionare tutte le caselle di controllo disponibili.  
  
-   **Deseleziona tutto** : consente di deselezionare tutte le caselle di controllo. Per continuare, è necessario selezionare almeno un oggetto di database.  
  
###  <a name="SetScriptOpt"></a> Pagina Imposta opzioni di generazione script  
 Usare questa pagina per specificare se si desidera che tramite la procedura guidata gli script vengano salvati nel percorso prescelto o vengano usati per pubblicare oggetti di database in un provider di hosting Web remoto. Ai fini della pubblicazione, è necessario avere accesso a un servizio Web installato usando il servizio Web Database Publishing Services.  
  
 **Opzioni** : se si vuole che gli script vengano salvati in un percorso specifico, selezionare **Salva script in un percorso specifico**. È possibile eseguire in un secondo momento gli script in a un'istanza del motore di database o in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Se si desidera pubblicare gli oggetti di database in un provider di hosting Web remoto tramite una procedura guidata, selezionare **Pubblica su servizio Web**.  
  
 **Salva script in una posizione specifica** : salvare uno o più. File di script Transact-SQL in un percorso specificato.  
  
-   **Avanzate** : consente di visualizzare la finestra di dialogo **Opzioni di generazione script avanzate** in cui è possibile selezionare opzioni avanzate per la generazione di script.  
  
-   **Salva nel file** : consente di salvare lo script in uno o più file con estensione sql. Fare clic sul pulsante Sfoglia (**…**) per specificare il nome e il percorso del file. Selezionare la casella di controllo **Sovrascrivi file esistente** per sostituire il file se ne esiste già uno con lo stesso nome. Fare clic su **File singolo** o **Singolo file per oggetto** per specificare come devono essere generati gli script. Fare clic su **Testo Unicode** o **Testo ANSI** per specificare il tipo di testo che deve essere usato nello script.  
  
-   **Salva negli Appunti** : consente di salvare lo script Transact-SQL negli Appunti.  
  
-   **Salva in una nuova finestra Query** : consente di generare lo script in una finestra dell'editor di query del motore di database. Se non vi sono finestre dell'editor aperte, viene aperta una nuova finestra dell'editor da usare come destinazione dello script.  
  
 **Pubblica su servizio Web** : consente di pubblicare gli oggetti selezionati in un servizio di hosting Web remoto per il quale è stato configurato un provider.  
  
-   **Gestisci provider** : consente di visualizzare la finestra di dialogo **Gestisci provider** . Usare la finestra di dialogo **Gestisci provider** per aggiungere, modificare ed eliminare provider di hosting. Ogni provider specifica le informazioni di connessione per un servizio di hosting Web e i database di destinazione presenti nel servizio.  
  
-   **Avanzate** : consente di visualizzare la finestra di dialogo **Opzioni di pubblicazione avanzate** in cui è possibile selezionare opzioni avanzate per la pubblicazione di script.  
  
-   **Provider** : consente di selezionare il provider che specifica le informazioni di connessione per il servizio di hosting Web che ospita il database nel quale pubblicare gli oggetti selezionati. È necessario avere almeno un provider nella finestra di dialogo **Gestisci provider** per selezionare un provider.  
  
-   **Database di destinazione** : consente di selezionare il database di destinazione nel quale pubblicare gli oggetti selezionati. È necessario selezionare un provider prima di selezionare un database di destinazione.  
  
###  <a name="AdvScriptOpt"></a> Pagina Opzioni di generazione script avanzate  
 Usare questa pagina per specificare come si desidera che vengano generati gli script tramite la procedura guidata. Sono disponibili molte opzioni diverse. Le opzioni sono disattivate se non sono supportate dalla versione di SQL Server o di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] specificata in **Tipo di motore di database**.  
  
 **Opzioni** : consente di specificare le opzioni avanzate selezionando un valore tra quelli disponibili nell'elenco visualizzato a destra di ciascuna opzione.  
  
 **Generale**: le opzioni seguenti si applicano all'intero script.  
  
-   **ANSI Padding** -include `ANSI PADDING ON` nello script. Il valore predefinito è **True**.  
  
-   **Accoda a file** : se è impostato su **True**, questo script viene aggiunto alla fine di uno script esistente specificato nella pagina **Imposta opzioni di generazione script** . Se è impostato su **False**, il nuovo script sovrascrive uno script precedente. Il valore predefinito è **False**.  
  
-   **Continua generazione script in caso di errore** : se è impostato su **True**, la generazione di script viene arrestata in caso di errore. Se è impostato su **False**, la creazione di script continua. Il valore predefinito è **False**.  
  
-   **Converti UDDT in tipi di base** : se è impostato su **True**, i tipi di dati definiti dall'utente (UDDT) vengono convertiti nei tipi di dati di base sottostanti che erano stati usati per crearli. Usare **True** se il tipo di dati UDDT non esiste nel database in cui verrà eseguito lo script. Se è impostato su **False**, vengono usati gli UDDT. Il valore predefinito è **False**.  
  
-   **Genera script per oggetti dipendenti** : consente di generare uno script per un oggetto la cui presenza è necessaria quando viene eseguito lo script per l'oggetto selezionato. Il valore predefinito è **True**.  
  
-   **Includi intestazioni descrittive** : se è impostato su **True**, allo script vengono aggiunti commenti descrittivi dividendolo in sezioni per ogni oggetto. Il valore predefinito è **False**.  
  
-   **Includi IF NOT EXISTS** : se è impostato su **True**, lo script include un'istruzione che verifica se l'oggetto esiste già nel database e non prova a creare un nuovo oggetto se già presente. Il valore predefinito è **False**.  
  
-   **Includi nomi di vincoli di sistema** : se è impostato su **False**, i valori predefiniti dei vincoli nominati automaticamente nel database di origine vengono automaticamente rinominati nel database di destinazione. Se è impostato su **True**, i vincoli hanno lo stesso nome nel database di origine e in quello di destinazione.  
  
-   **Includi istruzioni non supportate** : se è impostato su **False**, lo script non contiene istruzioni per oggetti che non sono supportati nella versione del server o nel tipo di motore selezionati. Se impostato su **Vero**, lo script contiene gli oggetti non supportati. Ogni istruzione per un oggetto non supportato sarà accompagnata da un commento che specifica che è necessario modificare l'istruzione prima di potere eseguire lo script con la versione di SQL Server o il tipo di motore selezionati. Il valore predefinito è **False**.  
  
-   **Schema per qualifica dei nomi degli oggetti** : consente di includere il nome dello schema nel nome degli oggetti che vengono creati. Il valore predefinito è **True**.  
  
-   **Genera script per associazioni** : consente di generare uno script per l'associazione di oggetti predefiniti e oggetti della regola. Il valore predefinito è **False**. Per altre informazioni, vedere [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) e [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
-   **Script per regole di confronto**: consente di includere nello script le informazioni sulle regole di confronto. Il valore predefinito è **False**. Per altre informazioni, vedere [Collation and Unicode Support](../collations/collation-and-unicode-support.md).  
  
-   **Script per valori predefiniti** : consente di includere nelle colonne della tabella gli oggetti predefiniti usati per impostare i valori predefiniti. Il valore predefinito è **True**. Per altre informazioni, vedere [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
-   **Genera script per DROP e CREATE**: se è impostato su **Genera script per CREATE**, vengono incluse le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] per creare oggetti. Se impostato su **Genera script per DROP**, vengono incluse le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] per eliminare oggetti. Se è impostato su **Genera script per DROP e CREATE**, nello script viene inclusa l'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] di eliminazione seguita dall'istruzione di creazione per ogni oggetto inserito nello script. Il valore predefinito è **Genera script per CREATE**.  
  
-   **Script per proprietà estese** : consente di includere le proprietà estese nello script, se presenti nell'oggetto. Il valore predefinito è **True**.  
  
-   **Script per il tipo di motore di database** : consente di creare uno script che può essere eseguito nel tipo selezionato di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] o di un'istanza del motore di database di SQL Server. Oggetti non supportati sul tipo specificato non sono inclusi nello script. Il tipo predefinito è quello del server di origine.  
  
-   **Script per versione server** : consente di creare uno script eseguibile nella versione selezionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per le nuove funzionalità non è possibile generare script per le versioni precedenti. La versione predefinita è quella del server di origine.  
  
-   **Script per account di accesso** : se l'oggetto per il quale generare uno script è un utente di database, questa opzione consente di creare gli account di accesso da cui l'utente dipende. Il valore predefinito è **False**.  
  
-   **Script per autorizzazioni a livello oggetto** : consente di includere script per l'impostazione dell'autorizzazione per gli oggetti del database. Il valore predefinito è **False**.  
  
-   **Generare script per statistiche** -se impostato su **Script per statistiche**, questa opzione include il `CREATE STATISTICS` istruzione per ricreare le statistiche sull'oggetto. L'opzione **Genera script per statistiche e istogrammi** consente inoltre di creare informazioni sugli istogrammi. Il valore predefinito è **Non generare script per statistiche**. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
-   **Script per USE DATABASE** -aggiunge il `USE DATABASE` istruzione allo script. Per verificare che gli oggetti di database vengano creati nel database corretto, includere l'istruzione `USE DATABASE`. Quando si prevede che lo script da usare in un database diverso, selezionare **False** omettere il `USE DATABASE` istruzione. Il valore predefinito è **True**. Per altre informazioni, vedere [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   **Tipi di dati da script** -consente di selezionare cosa deve essere inserito negli script: **Data only**, **solo Schema**, o entrambi. Il valore predefinito è **Solo schema**.  
  
 **Opzioni tabella/vista** : le opzioni seguenti si applicano solo agli script per tabelle o viste.  
  
-   **Genera script per il rilevamento modifiche** : consente di generare script per il rilevamento delle modifiche se è abilitato nel database di origine o nelle tabelle del database di origine. Il valore predefinito è **False**. Per altre informazioni, vedere [Informazioni sul rilevamento delle modifiche &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
-   **Script per vincoli check** -aggiunge `CHECK` allo script. Il valore predefinito è **True**. I vincoli `CHECK` richiedono che i dati immessi in una tabella rispettino una condizione specificata. Per altre informazioni, vedere [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
-   **Genera script per le opzioni di compressione dati** : consente di includere le opzioni di compressione dati, se sono configurate nel database di origine o nelle tabelle del database di origine. Per altre informazioni, vedere [Data Compression](../data-compression/data-compression.md). Il valore predefinito è **False**.  
  
-   **Script per chiavi esterne** : consente di aggiungere chiavi esterne allo script. Il valore predefinito è **True**. Le chiavi esterne indicano e impongono le relazioni tra tabelle.  
  
-   **Script per indici full-text** : consente di generare script per la creazione di indici full-text. Il valore predefinito è **False**.  
  
-   **Script per indici** : consente di generare script per la creazione di indici. Il valore predefinito è **True**. Gli indici consentono di trovare dati rapidamente.  
  
-   **Script per chiavi primarie** : consente di generare script per la creazione di chiavi primarie nelle tabelle. Il valore predefinito è **True**. Le chiavi primarie identificano in modo univoco ogni riga di una tabella.  
  
-   **Script per trigger** : consente di generare script per la creazione di trigger DML nelle tabelle. Il valore predefinito è **False**. Un trigger DML è un'azione programmata per l'esecuzione quando si verifica un evento DML (Data Manipulation Language) nel server di database. Per altre informazioni, vedere [DML Triggers](../triggers/dml-triggers.md).  
  
-   **Script per chiavi univoche** : consente di generare script per la creazione di chiavi univoche nelle tabelle. Le chiavi univoche impediscono l'immissione di dati duplicati. Il valore predefinito è **True**. Per altre informazioni, vedere [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
###  <a name="MgProviders"></a> Pagina Gestisci provider  
 Usare questa finestra di dialogo per visualizzare, aggiungere, modificare, eliminare o testare le connessioni del provider di hosting. Un provider di hosting specifica le informazioni di connessione per un servizio Web creato tramite il progetto Database Publishing Service in SQL Server Hosting Toolkit su CodePlex.  
  
 **Provider configurati** : consente di elencare il nome e l'indirizzo del servizio **Web** di ciascun provider di hosting salvato.  
  
 **Nuovo** : consente di aprire la finestra di dialogo **Configurazione del provider per nuovo provider** per aggiungere un nuovo provider di hosting.  
  
 **Modifica** : consente di aprire la finestra di dialogo **Configurazione del provider** corrispondente per modificare un provider di hosting esistente.  
  
 **Elimina** : consente di eliminare il provider di hosting selezionato.  
  
 **Test** : consente di eseguire un test della connessione a un servizio di hosting usando le informazioni dal provider selezionato.  
  
 **OK** : consente di salvare tutte le modifiche apportate alla finestra di dialogo **Provider di hosting** .  
  
 **Annulla** : consente di annullare tutte le modifiche apportate alla finestra di dialogo **Provider di hosting** .  
  
###  <a name="AdvPubOpts"></a> Pagina Opzioni di pubblicazione avanzate  
 Usare questa pagina per specificare il modo in cui si desidera pubblicare un database tramite la procedura guidata. Sono disponibili molte opzioni diverse. Le opzioni sono disattivate se non sono supportate dalla versione di SQL Server o di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] specificata in **Tipo di motore di database**.  
  
 **Opzioni** : consente di specificare le opzioni avanzate selezionando un valore tra quelli disponibili nell'elenco visualizzato a destra di ciascuna opzione.  
  
 **Generale**: le opzioni seguenti si applicano all'intera pubblicazione.  
  
1.  **Converti UDDT in tipi di base** : se è impostato su **True**, i tipi di dati definiti dall'utente (UDDT) vengono convertiti nei tipi di dati di base sottostanti che erano stati usati per crearli. Usare **True** se il tipo di dati UDDT non esiste nel database in cui verrà eseguito lo script. Se è impostato su **False**, vengono usati gli UDDT. Il valore predefinito è **False**.  
  
2.  **Pubblica regole di confronto** : consente di includere informazioni sulle regole di confronto per le colonne della tabella. Il valore predefinito è **False**. Per altre informazioni, vedere [Collation and Unicode Support](../collations/collation-and-unicode-support.md).  
  
3.  **Pubblica valori predefiniti** : consente di includere nelle colonne della tabella gli oggetti predefiniti usati per impostare i valori predefiniti. Il valore predefinito è **True**. Per altre informazioni, vedere [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
4.  **Pubblica oggetti dipendenti**: consente di pubblicare un oggetto la cui presenza è necessaria quando viene eseguito lo script per l'oggetto selezionato. Il valore predefinito è **True**.  
  
5.  **Pubblica proprietà estese** : consente di includere le proprietà estese nello script che viene inviato al provider per la pubblicazione, se presenti nell'oggetto. Il valore predefinito è **True**.  
  
6.  **Pubblica per versione del server** : consente di creare uno script che viene inviato al provider remoto per la pubblicazione, in modo che possa essere eseguito nella versione selezionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per le nuove funzionalità non è possibile generare script per le versioni precedenti. La versione predefinita è quella del server di origine.  
  
7.  **Pubblica autorizzazioni a livello di oggetto** : consente di includere le autorizzazioni per gli oggetti selezionati del database. Il valore predefinito è **False**.  
  
8.  **Pubblica statistiche** -se impostato su **pubblica statistiche**, include il `CREATE STATISTICS` istruzione per ricreare le statistiche sull'oggetto. L'opzione **Pubblica statistiche e istogrammi** consente di creare anche informazioni sugli istogrammi. Il valore predefinito è **Non pubblicare statistiche**. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
9. **Pubblica opzioni vardecimal** -consente il `vardecimal` formato della tabella nella tabella di database di destinazione quando è abilitato nella tabella del database di origine. Il valore predefinito è **True**.  
  
10. **Schema per qualifica dei nomi degli oggetti** : consente di includere il nome dello schema nel nome degli oggetti che vengono creati. Il valore predefinito è **True**.  
  
11. **Genera script per associazioni** : consente di includere nello script inviato al provider per la pubblicazione l'associazione per gli oggetti predefiniti e gli oggetti della regola. Il valore predefinito è **True**. Per altre informazioni, vedere [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) e [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
12. **Tipi di dati da pubblicare** -consente di selezionare cosa deve essere inserito negli script: **Data only**, **solo Schema**, o entrambi. Il valore predefinito è **Schema e dati**.  
  
 **Opzioni di pubblicazione**: consente di specificare se usare transazioni per la pubblicazione nel provider di hosting Web.  
  
1.  **Pubblicazione con transazione** : consente di usare le transazioni per la pubblicazione su un provider di hosting Web remoto. Se il database di destinazione non può completare la pubblicazione, viene eseguito il rollback delle transazioni. Il valore predefinito è **True**.  
  
 **Opzioni tabella/vista** : le opzioni seguenti si applicano solo alle tabelle o alle viste.  
  
1.  **Pubblica vincoli check** -include la creazione di `CHECK` vincoli nel processo di pubblicazione. Il valore predefinito è **True**. I vincoli `CHECK` richiedono che i dati immessi in una tabella rispettino una condizione specificata. Per altre informazioni, vedere [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
2.  **Pubblica chiavi esterne** : consente di includere la creazione di chiavi esterne nel processo di pubblicazione. Il valore predefinito è **True**. Le chiavi esterne indicano e impongono le relazioni tra tabelle. Per altre informazioni, vedere [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
3.  **Pubblica indici full-text** : consente di generare script per la creazione di indici full-text. Il valore predefinito è **False**.  
  
4.  **Pubblica indici** : consente di includere indici nelle tabelle nel processo di pubblicazione. Il valore predefinito è **True**. Gli indici consentono di trovare dati rapidamente.  
  
5.  **Pubblica chiavi primarie** : consente di includere la creazione di chiavi primarie nel processo di pubblicazione. Il valore predefinito è **True**. Le chiavi primarie identificano in modo univoco ogni riga di una tabella. Per altre informazioni, vedere [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
6.  **Pubblica trigger** : consente di includere la creazione di trigger DML nel processo di pubblicazione. Il valore predefinito è **True**. Un trigger DML è un'azione programmata per l'esecuzione quando si verifica un evento DML (Data Manipulation Language) nel server di database. Per altre informazioni, vedere [DML Triggers](../triggers/dml-triggers.md).  
  
7.  **Pubblica chiavi univoche** : consente di includere la creazione di chiavi univoche nelle tabelle nel processo di pubblicazione. Le chiavi univoche impediscono l'immissione di dati duplicati. Il valore predefinito è **True**. Per altre informazioni, vedere [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
8.  **Pubblica rilevamento modifiche** : consente di includere il rilevamento delle modifiche nel processo di pubblicazione, se è abilitato nel database di origine o nelle tabelle del database di origine. Il valore predefinito è **False**. Per altre informazioni, vedere [Informazioni sul rilevamento delle modifiche &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
9. **Pubblica opzioni di compressione dati**: consente di includere le opzioni di compressione dati nel processo di pubblicazione, se sono configurate nel database di origine o nelle tabelle del database di origine. Il valore predefinito è **True**. Per altre informazioni, vedere [Data Compression](../data-compression/data-compression.md).  
  
###  <a name="ProvConfig"></a> Pagina Configurazione del provider  
 Usare questa finestra di dialogo per visualizzare o modificare le impostazioni per il provider di hosting. È possibile usare questa finestra di dialogo per eseguire le operazioni seguenti:  
  
-   Visualizzazione, aggiunta o modifica delle informazioni di connessione per un provider di hosting.  
  
-   Visualizzazione, aggiunta, modifica o eliminazione di un database per la connessione di un provider.  
  
-   Configurazione automatica dei database di un provider di hosting.  
  
 Un provider di hosting specifica le informazioni di connessione per un servizio Web creato tramite il progetto Database Publishing Service in SQL Server Hosting Toolkit su CodePlex.  
  
 **Nome** : nome del provider di hosting.  
  
 **Indirizzo servizio Web** : indirizzo HTTPS del servizio di hosting.  
  
 **Autenticazione servizio Web** : nome utente e password necessari per accedere al servizio di hosting.  
  
 **Salva password** : consente di crittografare e salvare la password nel computer locale.  
  
 **Database disponibili** : i database configurati per i provider di hosting sono elencati in ordine crescente nel formato *nome_server*.*nome_database*.  
  
 **Nuovo** : consente di aprire la finestra di dialogo di configurazione **Database** e di aggiungere un nuovo database.  
  
 **Modifica** : consente di aprire la finestra di dialogo di configurazione **Database** per il database selezionato.  
  
 **Elimina** : consente di eliminare il database selezionato.  
  
 **Predefinito** : consente di impostare il database come predefinito.  
  
 **OK** : consente di salvare tutte le modifiche apportate in questa finestra di dialogo e di tornare alla procedura guidata.  
  
 **Annulla** : consente di annullare tutte le modifiche apportate in questa finestra di dialogo e di tornare alla procedura guidata.  
  
###  <a name="Summary"></a> Pagina Riepilogo  
 In questa pagina vengono riepilogate le opzioni selezionate nella procedura guidata. Per modificare un'opzione, fare clic su **Indietro**. Per avviare la generazione di script da salvare o pubblicare, fare clic su **Avanti**.  
  
 **Verificare le selezioni** : consente di visualizzare le opzioni selezionate per ogni pagina della procedura guidata. Espandere un nodo per visualizzare le opzioni selezionate per la pagina corrispondente.  
  
###  <a name="SavePubScripts"></a> Pagina Salva o pubblica script  
 Usare questa pagina per monitorare lo stato di avanzamento della procedura guidata durante l'esecuzione.  
  
 **Dettagli** : consente di visualizzare la colonna **Azione** per vedere lo stato di avanzamento della procedura guidata. Dopo avere generato gli script, la procedura guidata li salva in un file o li usano per la pubblicazione su un servizio Web, a seconda delle selezioni. Al termine di ciascuno di questi passaggi, fare clic sul valore nella colonna **Risultato** per vedere il risultato del passaggio corrispondente.  
  
 **Salva report** fare clic per salvare i risultati dello stato della procedura guidata in un file.  
  
 **Annulla** : fare clic per chiudere la procedura guidata prima che venga completata o se si verifica un errore.  
  
 **Fine** fare clic per chiudere la procedura guidata una volta completata o se si verifica un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di SMO (SQL Server Management Objects)](../server-management-objects-smo/installing-smo.md)   
 [Copia di database in altri server](../databases/copy-databases-to-other-servers.md)  
  
  
