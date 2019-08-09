---
title: Note sulla versione per SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/31/2019
ms.openlocfilehash: c30179ae89bc69e84005a95a4d370acf4b692bd2
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731135"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>Note sulla versione per SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Questo articolo fornisce informazioni dettagliate sugli aggiornamenti, i miglioramenti e le correzioni di bug per le versioni correnti e precedenti di SSMS.

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
Also, we are appending the 'Month yyyy.'

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md."
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-182"></a>SSMS 18.2

Download: [Scaricare SSMS 18.2](download-sql-server-management-studio-ssms.md)  
Numero di build: 15.0.18142.0  
Data di rilascio: 25 luglio 2019

SSMS 18.2 è la versione disponibile a livello generale più recente di SSMS. Se è necessaria una versione precedente, vedere [Versioni precedenti di SSMS](release-notes-ssms.md#previous-ssms-releases).

La versione 18.2 è un aggiornamento della versione 18.1 con i nuovi elementi e le correzioni di bug seguenti.

## <a name="whats-new-in-182"></a>Novità della versione 18.2

|  Nuovo elemento  |  Dettagli  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | Ottimizzazione delle prestazioni per l'utilità di pianificazione pacchetti SSIS in Azure. |
| IntelliSense/editor | Aggiunta del supporto per la classificazione dei dati. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Aggiunta del supporto di IntelliSense. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Attiva un'ottimizzazione all'interno del motore di database che contribuisce a migliorare la velocità effettiva per gli inserimenti nell'indice con un elevato grado di concorrenza. Questa opzione è destinata agli indici che sono soggetti a conflitti di inserimento dell'ultima pagina, che generalmente si verificano con gli indici con una chiave sequenziale, come una colonna Identity, una sequenza o una colonna di data/ora. Per altri dettagli, vedere [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys). |
| Esecuzione o risultati di query | Aggiunta di *Ora di completamento* nei messaggi per tenere traccia di quando viene completata l'esecuzione di una determinata query. |
| Esecuzione o risultati di query | È consentita la visualizzazione (risultato come testo) e l'archiviazione nelle celle (risultato come griglia) di più dati. SSMS consente ora fino a 2 M di caratteri per entrambi (rispettivamente, fino a 256 e 64 K). In questo modo è stato risolto anche il problema a causa del quale gli utenti non erano in grado di acquisire più di 43680 caratteri dalle celle della griglia. |
| Showplan | Aggiunta di un nuovo attributo in QueryPlan quando è abilitata la [funzionalità UDF scalare inline](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining) (ContainsInlineScalarTsqludfs). |
| SMO | Aggiunta del supporto per *Limitazioni delle funzionalità*. Per altre informazioni sulla funzionalità stessa, vedere [Limitazioni delle funzionalità](https://docs.microsoft.com/sql/relational-databases/security/feature-restrictions). |
| SMO | Aggiunta del supporto per l'*API Valutazione SQL*. Per altre informazioni, vedere [API Valutazione SQL](https://docs.microsoft.com/sql/sql-assessment-api/sql-assessment-api-overview). |
|  |  |

## <a name="bug-fixes-in-182"></a>Correzioni di bug nella versione 18.2

|  Nuovo elemento  |  Dettagli  |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accessibilità | Aggiornamento dell'interfaccia utente XEvent (la griglia) in modo che sia ordinabile premendo F3. |
| Always On | È stato risolto un problema a causa del quale SSMS generava un errore durante il tentativo di eliminare un gruppo di disponibilità |
| Always On | È stato risolto un problema a causa del quale SSMS presenta la procedura guidata di failover errata, con repliche configurate come sincrone, quando si usano gruppi di disponibilità con scalabilità in lettura (tipo cluster=NONE). SSMS presenta ora la procedura guidata per l'opzione Force_Failover_Allow_Data_Loss, che è l'unica consentita per la disponibilità con tipo di cluster NONE |
| Always On | È stato risolto un problema a causa del quale la procedura guidata limitava il numero di sincronizzazioni consentite a tre |
| Classificazione dei dati | È stato risolto un problema a causa del quale SSMS generava l'errore *L'indice deve essere maggiore o uguale a zero* durante il tentativo di visualizzare i report di classificazione dei dati nei database con livello di compatibilità minore di 150. |
| SQL Server Management Studio (SSMS) - Generale | È stato risolto un problema a causa del quale l'utente non era in grado di scorrere orizzontalmente il riquadro dei risultati tramite la rotellina del mouse. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34145641). |
| SQL Server Management Studio (SSMS) - Generale | Aggiornamento di *Monitoraggio attività* per ignorare i tipi di attesa benigni SQLTRACE_WAIT_ENTRIES |
| SQL Server Management Studio (SSMS) - Generale | È stato risolto un problema a causa del quale alcune opzioni relative ai colori *(Editor di testo > Scheda editor e barra di stato)* non venivano mantenute. Vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37924165)
| SQL Server Management Studio (SSMS) - Generale | Nella finestra di dialogo di connessione l'opzione *Active Directory - Universale con supporto MFA* è stata sostituita con *Azure Active Directory - Universale con supporto MFA* (la funzionalità è la stessa, ma si auspica generi meno confusione). |
| SQL Server Management Studio (SSMS) - Generale | Aggiornamento di SSMS per l'uso dei valori predefiniti corretti durante la creazione di un database SQL di Azure. |
| SQL Server Management Studio (SSMS) - Generale | È stato risolto un problema a causa del quale l'utente non era in grado di *avviare PowerShell* da un nodo in [Registra server](register-servers/register-servers.md) quando il server è un [contenitore SQL Linux](../linux/quickstart-install-connect-docker.md). |
| Importare file flat | È stato risolto un problema a causa del quale *Importa file flat* non funzionava dopo l'aggiornamento da SSMS 18.0 a 18.1. Vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37912636) |
| Importare file flat | È stato risolto un problema a causa del quale la *procedura guidata Importa file flat segnalava una colonna duplicata o non valida* in un file con estensione CSV con intestazioni con caratteri Unicode. |
| Esplora oggetti | È stato risolto un problema a causa del quale alcune voci di menu (ad esempio, *Importazione/esportazione guidata* SQL Server) risultavano mancanti o disabilitate quando connessi a SQL Express. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37500016). |
| Esplora oggetti | È stato risolto un problema che causava l'arresto anomalo di SSMS quando un oggetto veniva trascinato da Esplora oggetti all'editor. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37887988). |
| Esplora oggetti | È stato risolto un problema a causa del quale la ridenominazione dei database comportava la visualizzazione di nomi di database non corretti in Esplora oggetti. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37638472). |
| Esplora oggetti | È stato risolto un problema di lunga data a causa del quale viene generato un errore quando si tenta di espandere il nodo *Tabelle* in Esplora oggetti per un database impostato per l'uso di regole di confronto non più supportate da Windows (e l'utente non può espandere le tabelle). Un esempio di tali regole di confronto è Korean_Wansung_Unicode_CI_AS. |
| [Registrazione di server](register-servers/register-servers.md) | È stato risolto un problema a causa del quale il tentativo di eseguire una query su più server (in un *gruppo* di server registrati) quando il server registrato usa *Active Directory - Integrata* o *Active Directory - Universale con supporto MFA* non funziona perché SSMS non riesce a connettersi. |
| [Registrazione di server](register-servers/register-servers.md) | È stato risolto un problema a causa del quale il tentativo di eseguire una query su più server (in un *gruppo* di server registrati) quando il server registrato usa *Active Directory - Password* o *Autenticazione SQL* e l'utente sceglie di non memorizzare la password causa l'arresto anomalo di SSMS. |
| Report | È stato risolto un problema nei report di *utilizzo del disco* che causava un errore del report quando i file di dati includevano un numero elevato di extent. |
| Strumenti di replica | È stato risolto un problema a causa del quale Monitoraggio replica non funzionava con il database di pubblicazione nel gruppo di disponibilità e con il server di distribuzione nel gruppo di disponibilità (risolto in precedenza in SSMS 17.x) |
| SQL Agent | È stato risolto un problema a causa del quale con l'aggiunta, l'inserimento, la modifica o la rimozione dei passaggi di processo lo stato attivo veniva reimpostato sulla prima riga invece della riga attiva. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/38070892). |
| SMO/scripting | È stato risolto un problema a causa del quale *CREATE OR ALTER* non creava script per oggetti con proprietà estese. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/37236748). |
| SMO/scripting | È stato risolto un problema a causa del quale SSMS non era in grado di inserire correttamente in uno script CREATE EXTERNAL LIBRARY. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37868089). |
| SMO/scripting |  È stato risolto un problema a causa del quale quando si tentava di *generare script* per un database con poche migliaia di tabelle la finestra di dialogo di stato sembrava bloccata. |
| SMO/scripting | È stato risolto un problema a causa del quale la creazione di script per la *tabella esterna* in SQL 2019 non funzionava. |
| SMO/scripting | È stato risolto un problema a causa del quale la creazione di script per l'*origine dati esterna* in SQL 2019 non funzionava. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34295080). |
| SMO/scripting | È stato risolto un problema a causa del quale le *proprietà estese* per le colonne non venivano incluse nello script quando la destinazione era il database SQL di Azure. Per altri dettagli, vedere [stackoverflow](https://stackoverflow.com/questions/56952337/how-can-i-script-the-descriptions-of-columns-in-ms-sql-server-management-studio). |
| SMO/scripting | Inserimento ultima pagina: SMO - Aggiunta della proprietà *Index.IsOptimizedForSequentialKey* |
|**Installazione di SSMS**| **È stato risolto un problema a causa del quale il programma di installazione di SSMS bloccava erroneamente l'installazione di lingue non corrispondenti per i report SSMS. Questo poteva essere un problema in alcune situazioni anomale, ad esempio un'installazione interrotta o una disinstallazione non corretta di una versione precedente di SSMS. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37483594/).** |
| Profiler XEvent | Correzione di un arresto anomalo durante la chiusura del visualizzatore. |

### <a name="known-issues-182"></a>Problemi noti (18.2)

- Il diagramma di database creato in un'istanza di SSMS in esecuzione nel computer A non può essere modificato dal computer B (causando un arresto anomalo di SSMS). Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649).

- Problemi di aggiornamento di SSMS 18.0 durante il passaggio tra finestre di query diverse. Vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042). Una soluzione alternativa per questo problema è disabilitare l'accelerazione hardware in **Strumenti** > **Opzioni**.

- Esiste una limitazione alle dimensioni dei dati visualizzati dai risultati di SSMS in griglia, testo o file.

È possibile fare riferimento a [UserVoice](https://feedback.azure.com/forums/908035-sql-server) per altri problemi noti e per inviare commenti e suggerimenti al team del prodotto. 

## <a name="previous-ssms-releases"></a>Versioni precedenti di SSMS

Scaricare le versioni precedenti di SSMS facendo clic sui collegamenti dei titoli nelle sezioni seguenti:

## <a name="downloadssdtmediadownloadpng-ssms-181httpsgomicrosoftcomfwlinklinkid2094583"></a>![download](../ssdt/media/download.png) [SSMS 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)

- Numero di versione: 18.1  
- Numero di build: 15.0.18131.0  
- Data di rilascio: 11 giugno 2019  

[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

SSMS 18.1 è la versione GA più recente di SSMS. Se è necessaria una versione precedente, vedere [Versioni precedenti di SSMS](release-notes-ssms.md#previous-ssms-releases).

18.1 è un aggiornamento di piccole dimensioni della versione 18.0 con i nuovi elementi e le correzioni di bug seguenti.

## <a name="whats-new-in-181"></a>Novità della versione 18.1

| Nuovo elemento| Dettagli|
| :-------| :------|
| Diagrammi di database | [I diagrammi di database sono stati nuovamente aggiunti a SSMS](https://feedback.azure.com/forums/908035/suggestions/37507828).
| SSBDIAGNOSE.EXE |Lo strumento da riga di comando di diagnostica di SQL Server è stato nuovamente aggiunto al pacchetto di SSMS.|
| Integration Services (SSIS) | Supporto per la pianificazione del pacchetto SSIS, che si trova nel catalogo SSIS in Azure o nel file system, in Azure. Esistono tre voci di menu per l'avvio della finestra di dialogo Nuova pianificazione: *Nuova pianificazione* che viene visualizzata quando si fa clic con il pulsante destro del mouse sul pacchetto SSIS nel catalogo SSIS in Azure, *Schedule SSIS Package in Azure* (Pianifica pacchetto SSIS in Azure) in *Esegui migrazione ad Azure* nel menu *Strumenti* e "Schedule SSIS in Azure" (Pianifica SSIS in Azure) che viene visualizzata quando si fa clic con il pulsante destro del mouse sulla cartella Processi in SQL Server Agent dell'Istanza gestita del database SQL di Azure.|

## <a name="bug-fixes-in-181"></a>Correzioni di bug nella versione 18.1

| Nuovo elemento | Dettagli |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accessibilità | Migliorata l'accessibilità dell'interfaccia utente del processo di Agent. |
| Accessibilità | Migliorata l'accessibilità nella pagina di monitoraggio di Stretch grazie all'aggiunta del nome accessibile per il pulsante *Aggiornamento automatico* e anche all'aggiunta di un nome accessibile intelligente che consentirà agli utenti di sapere su quale pulsante si trovano e quale sarà l'effetto se viene selezionato. |
| Integrazione ADS| Correzione di un possibile arresto anomalo di SSMS nel tentativo di usare i server registrati ADS.|
| Progettazione database | Aggiunto il supporto per le regole di confronto Latin1_General_100_BIN2_UTF8 (disponibile in SQL Server 2019 CTP3.0) |
| Classificazione dati | Impedisce l'aggiunta di etichette di riservatezza alle colonne nella tabella di cronologia, che non è supportata. |
| Classificazione dati | Correzione del problema relativo alla gestione non corretta del livello di compatibilità (server/database). |
| Progettazione database | Aggiunto il supporto per le regole di confronto Latin1_General_100_BIN2_UTF8 (disponibile in SQL2019 CTP3.0). |
| SQL Server Management Studio (SSMS) - Generale | Correzione di un problema per cui lo scripting di pseudocolonne in un indice non era corretto. |
| SQL Server Management Studio (SSMS) - Generale | Correzione di un problema nella pagina delle proprietà Account di accesso in cui la selezione del pulsante *Aggiungi credenziali* poteva generare un'eccezione di riferimento Null. |
| SQL Server Management Studio (SSMS) - Generale | Correzione della visualizzazione delle dimensioni della colonna Money nella pagina delle proprietà Indice. |
| SQL Server Management Studio (SSMS) - Generale | Correzione di un problema per cui SSMS non rispettava le impostazioni di Intellisense di *Strumenti/Opzioni* nella finestra dell'editor di SQL. |
| SQL Server Management Studio (SSMS) - Generale | Correzione di un problema a causa del quale SSMS non rispettava le impostazioni di IntelliSense di Guida (online/offline). |
| Valori DPI alti | Correzione del layout dei controlli nelle finestre di dialogo di errore per le opzioni di query non supportate. |
| Valori DPI alti | Correzione del layout dei controlli nella pagina *Nuovo gruppo di disponibilità* in alcune versioni localizzate di SSMS. |
| Valori DPI alti | Correzione del layout della pagina *Nuova pianificazione processo*. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37632094). |
| Importa file flat | Correzione di un problema a causa del quale durante l'importazione era possibile che le righe venissero automaticamente perse.|
| Intellisense/editor | Ridotto il traffico delle query basato su SMO verso i database SQL di Azure per IntelliSense. |
| Intellisense/editor | Correzione dell'errore grammaticale nella descrizione comando visualizzata durante la digitazione di T-SQL per creare un utente. È stato anche corretto il messaggio di errore per evitare ambiguità tra utenti e account di accesso. |
| Visualizzatore log | Correzione di un problema a causa del quale SSMS apriva sempre il log (o l'agente) del server corrente anche in caso di doppio clic sul segno di un archivio precedente in Esplora oggetti. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37633648). |
| Installazione di SSMS | Correzione del problema che impediva l'installazione di SSMS quando il percorso del log del programma di installazione conteneva spazi. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37496110). |
| Installazione di SSMS | Correzione di un problema per cui SSMS si chiudeva immediatamente dopo aver visualizzato la schermata iniziale. </br> Per altri dettagli, vedere questi siti: [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37502512), [SSMS Refuses to Start](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start) (SSMS rifiuta l'avvio) e [Database Administrators](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up) (Amministratori di database). |
| Esplora oggetti | Elevazione della restrizione per abilitare *Avvia Powershell* quando si è connessi a SQL in Linux. |
| Esplora oggetti | Correzione di un problema che causava l'arresto anomalo di SSMS durante il tentativo di espandere il nodo Gruppo con scalabilità orizzontale PolyBase (quando si è connessi a un nodo di calcolo). |
| Esplora oggetti | Correzione di un problema per cui la voce di menu *Disabilitato* restava abilitata anche dopo aver disabilitato un determinato indice. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37735375). |
| Report | Correzione del report per la visualizzazione di GrantedQueryMemory in KB (report Performance Dashboard di SQL). Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37167289). |
| Report | Miglioramento della traccia del blocco del log negli scenari Always On. |
| Showplan | Aggiunta del nuovo elemento showplan *SpillOccurred* allo schema showplan. |
| Showplan | Aggiunta delle letture remote (*ActualPageServerReads*, *ActualPageServerReadAheads* *ActualLobPageServerReads*, *ActualLobPageServerReadAheads*) allo schema showplan. |
| SMO/scripting | Evita l'esecuzione di query ai vincoli di arco durante la creazione di script per tabelle non grafo. |
| SMO/scripting | Rimozione del vincolo sulla classificazione di riservatezza durante la creazione di script per colonne con *Classificazione dati*. |
| SMO/scripting | Correzione di un problema a causa del quale "Genera script" in una tabella grafo non funziona durante la generazione di dati. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466). |
| SMO/scripting | Correzione di un problema a causa del quale il metodo EnumObjects() non recuperava il nome dello schema per un oggetto Synonym. |
| SMO/scripting | Correzione di un problema in UIConnectionInfo.LoadFromStream() in cui la sezione *AdvancedOptions* non veniva letta (quando non era specificata una password). |
| SQL Agent | Correzione di un problema che causava l'arresto anomalo di SSMS durante l'uso della finestra Proprietà processo. Per altri dettagli, vedere [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37164244). |
| SQL Agent | Correzione di un problema per cui il pulsante "Visualizza" in *Proprietà passaggio processo* non era sempre abilitato impedendo così la visualizzazione dell'output di un passaggio di processo specifico. |
| Interfaccia utente XEvent | Aggiunta della colonna "Pacchetto" all'elenco XEvents per evitare ambiguità tra eventi con nomi identici. |
| Interfaccia utente XEvent | Aggiunta del mapping del tipo di classe "EXTERNAL LIBRARY" mancante a XEventUI. |

### <a name="known-issues-181"></a>Problemi noti (18.1)

- Gli utenti potrebbe visualizzare un errore trascinando un oggetto tabella da Esplora oggetti nell'editor di query. Siamo a conoscenza del problema, la cui correzione è prevista nella prossima versione.

- Le opzioni colore di *Connessioni di gruppo* e *Connessioni a un unico server* in Opzioni -> Editor di testo -> Scheda editor e barra di stato -> Layout e colori barra di stato non vengono mantenute dopo la chiusura di SSMS 18.1. Alla riapertura di SSMS, l'opzione Layout e colori barra di stato ripristina il valore predefinito (bianco).

- Esiste una limitazione alle dimensioni dei dati visualizzati dai risultati di SSMS in griglia, testo o file

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![scaricare ](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- Numero di versione: 18.0  
- Numero di build: 15.0.18118.0  
- Data di rilascio: 24 aprile 2019

[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [Francese](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [Tedesco](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [Giapponese](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>Novità della versione 18.0

| Nuovo elemento| Dettagli|
| :-------| :------|
|Supporto per SQL Server 2019|SSMS 18.0 è la prima versione di SSMS che *supporta completamente* SQL Server 2019 (livello di compatibilità 150).|
|Supporto per SQL Server 2019|Supporto di "BATCH_STARTED_GROUP" e "BATCH_COMPLETED_GROUP" in SQL Server 2019 e in un'istanza gestita di SQL.|
|Supporto per SQL Server 2019|SMO: aggiunta del supporto per l'inlining della funzione definita dall'utente.|
|Supporto per SQL Server 2019|GraphDB: aggiunta di un flag nello showplan per la sequenza Graph TC.|
|Supporto per SQL Server 2019|Always Encrypted: aggiunta del supporto per AEv2/Enclave.|
|Supporto per SQL Server 2019|Always Encrypted: la finestra di dialogo di connessione ha una nuova scheda "Always Encrypted" quando l'utente fa clic sul pulsante "Opzioni" per abilitare e configurare il supporto degli enclave.|
|File di download di SSMS di dimensioni più piccole| Le dimensioni correnti sono di circa 500 MB, quasi la metà del bundle SSMS 17.x.
|SSMS è basato su Visual Studio 2017 Shell (Isolated).|La nuova shell (SSMS è basato su Visual Studio 2017 15.9.11) include tutte le correzioni per l'accessibilità apportate sia in SSMS sia in Visual Studio, oltre alle ultime correzioni per la sicurezza.|
|Miglioramenti di accessibilità di SSMS| È stata dedicata un'attenzione particolare ai problemi di accessibilità in tutti gli strumenti (SSMS, DTA e Profiler)|
|SSMS può ora essere installato in una cartella personalizzata| Questa opzione è disponibile sia dalla riga di comando (utile per l'installazione automatica) che dall'interfaccia utente di installazione. Dalla riga di comando passare questo argomento aggiuntivo a SSMS-Setup-ENU.exe:   SSMSInstallRoot=C:\MySSMS18 Per impostazione predefinita, il nuovo percorso di installazione per SSMS è: %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe.  Questo non significa che SSMS sia multi-istanza.|
|SSMS consente l'installazione in una lingua diversa da quella del sistema operativo|Il blocco per l'installazione in lingue miste è stato rimosso. È ad esempio possibile installare SSMS in tedesco in una versione di Windows in francese. Se la lingua del sistema operativo non corrisponde a quella di SSMS, l'utente deve cambiare la lingua in **Strumenti** > **Opzioni** > **Impostazioni internazionali**, altrimenti SSMS visualizza l'interfaccia utente in inglese.|
|SSMS non condivide più componenti con il motore SQL|È stata dedicata un'attenzione particolare a evitare la condivisione di componenti con il motore SQL. Questa condivisione generava spesso problemi di funzionalità quando venivano usati i file installati da altre applicazioni.|
|SSMS richiede NetFx 4.7.2 o versioni successive|Il requisito minimo è passato da NetFx4.6.1 a NetFx4.7.2: in tal modo è possibile trarre vantaggio dalle nuove funzionalità incluse nel nuovo framework.|
|Possibilità di eseguire la migrazione delle impostazioni di SSMS| La prima volta che SSMS 18 viene avviato, all'utente viene richiesto di eseguire la migrazione delle impostazioni della versione 17.x. I file di impostazioni dell'utente vengono ora archiviati in un file XML normale, migliorando la portabilità e possibilmente consentendo le modifiche.|
|Supporto per valori DPI alti| Il supporto per valori DPI alti è ora abilitato per impostazione predefinita.|
|SSMS viene fornito con il driver Microsoft OLE DB| Per i dettagli, vedere [Scaricare il driver Microsoft OLE DB per SQL Server](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server).|
|SSMS non è supportato in Windows 8. Per Windows 10/Windows Server 2016 è richiesta la versione 1607 (10.0.14393) o successiva|A causa della nuova dipendenza da NetFx 4.7.2, SSMS 18.0 non viene installato in Windows 8, nelle versioni meno recenti di Windows 10 e in Windows Server 2016. Il programma di installazione di SSMS blocca tali sistemi. Windows 8.1 è ancora supportato.|
|SSMS non viene più aggiunto alla variabile di ambiente PATH|Il percorso di SSMS.EXE e degli strumenti in generale non viene più aggiunto al percorso. Gli utenti possono aggiungerlo direttamente o, nel caso di un computer Windows moderno, tramite il menu Start.|
|Gli ID pacchetto non sono più necessari per sviluppare le estensioni di SSMS| In passato SSMS caricava in modo selettivo solo i pacchetti noti e gli sviluppatori dovevano registrare i propri pacchetti. Questo non si verifica più.|
|SQL Server Management Studio (SSMS) - Generale|Opzione di configurazione AUTOGROW_ALL_FILES disponibile per i filegroup in SSMS.|
|SQL Server Management Studio (SSMS) - Generale|Rimozione delle opzioni a rischio 'lightweight pooling' e 'priority boost' dalla GUI di SSMS. Per i dettagli, vedere [Priority boost details – and why it's not recommended](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/).
|SQL Server Management Studio (SSMS) - Generale|Nuovi menu e tasti di scelta rapida per la creazione di file: **CTRL+ALT+N**. **CTRL+N** continua a funzionare per creare una nuova query.|
|SQL Server Management Studio (SSMS) - Generale|La finestra di dialogo **Nuova regola del firewall** consente ora di specificare un nome di regola invece di generarne uno automaticamente.|
|SQL Server Management Studio (SSMS) - Generale|Funzionalità IntelliSense migliorata nell'editor, in particolare per T-SQL v140 e successive.|
|SQL Server Management Studio (SSMS) - Generale|Aggiunta del supporto UTF-8 nella finestra di dialogo delle regole di confronto dell'interfaccia utente di SSMS.|
|SQL Server Management Studio (SSMS) - Generale|Passaggio a "Gestione credenziali di Windows" per le password MRU della finestra di dialogo Connessione. Risolve un problema rilevato da tempo per cui la persistenza delle password non era sempre affidabile.|
|SQL Server Management Studio (SSMS) - Generale|Supporto migliorato per i sistemi con più monitor, con un numero crescente di finestre e più finestre di dialogo ora visualizzate sul monitor previsto.|
|SQL Server Management Studio (SSMS) - Generale|Viene visualizzata la configurazione server "backup checksum default" nella nuova pagina Impostazioni database della finestra di dialogo Proprietà server. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974](https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974).|
|SQL Server Management Studio (SSMS) - Generale|Dimensioni massime dei file di log degli errori incluse in "Configura log degli errori di SQL Server". Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/33624115](https://feedback.azure.com/forums/908035/suggestions/33624115).|
|SQL Server Management Studio (SSMS) - Generale|Aggiunta dell'opzione "Esegui migrazione ad Azure" al menu Strumenti. Sono stati integrati Database Migration Assistant e Servizio Migrazione del database per un accesso rapido e veloce e per accelerare le migrazioni ad Azure.|
|SQL Server Management Studio (SSMS) - Generale|È stata aggiunta logica per chiedere all'utente di eseguire il commit delle transazioni aperte quando si usa "Cambia connessione".|
|Integrazione di Azure Data Studio|Aggiunta di una voce di menu per avviare e scaricare Azure Data Studio.|
|Integrazione di Azure Data Studio|Aggiunta della voce di menu "Start Azure Data Studio" (Avvia Azure Data Studio) in Esplora oggetti.|
|Integrazione di Azure Data Studio|Quando si fa clic con il pulsante destro del mouse su un nodo di database in Esplora oggetti, vengono visualizzati i menu di scelta rapida per eseguire una query o per creare un nuovo notebook in Azure Data Studio.|
|Supporto di Azure SQL| Le proprietà del database SLO/Edition/MaxSize ora accettano nomi personalizzati, facilitando il supporto delle edizioni future del database SQL di Azure.|
|Supporto di Azure SQL| Aggiunto il supporto per gli SKU vCore (utilizzo generico e business critical): Gen4_24 e tutti gli SKU Gen5.|
|Istanza gestita di database SQL di Azure|Aggiunta di un nuovo tipo di account di accesso di AAD in SMO e SSMS quando ci si connette a un'istanza gestita di database SQL di Azure.|
|Always On|Rigenerazione hash per RTO (tempo di recupero stimato) e RPO (perdita di dati stimata) nel dashboard Always On di SSMS. Vedere la documentazione aggiornata all'indirizzo [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md).|
|Always Encrypted| La casella di controllo Abilita Always Encrypted nella nuova scheda Always Encrypted nella finestra di dialogo Connetti al server ora consente di abilitare o disabilitare facilmente la funzionalità Always Encrypted per una connessione di database.|
|Always Encrypted con enclave sicuri| Nell'anteprima di SQL Server 2019 sono stati apportati diversi miglioramenti per il supporto della funzionalità Always Encrypted con enclave sicuri:  Un campo di testo per specificare l'URL di attestazione dell'enclave nella finestra di dialogo Connetti al server (la nuova scheda Always Encrypted).  La nuova casella di controllo nella finestra di dialogo Nuova chiave master della colonna per controllare se una nuova chiave master della colonna consente i calcoli dell'enclave.  Altre finestre di dialogo di gestione delle chiavi Always Encrypted ora visualizzano informazioni su quali chiavi master della colonna consentono i calcoli dell'enclave.|
|File di controllo|Metodo di autenticazione cambiato dal metodo basato sulla Chiave account di archiviazione all'autenticazione basata su Azure AD.|
|File di controllo|Aggiornato l'elenco delle azioni di controllo conosciute per includere la RESTRIZIONE FUNZIONALITÀ AGGIUNGI/MODIFICA GRUPPO/ELIMINA.|
|Classificazione dei dati| Riorganizzazione del menu attività Classificazione dati : è stato aggiunto un sottomenu al menu delle attività del database ed è stata aggiunta un'opzione per aprire il report dal menu senza dover aprire prima la finestra Classifica dati.|
|Classificazione dei dati|Aggiunta della nuova funzionalità 'Classificazione dati' in SMO. L'oggetto colonna espone nuove proprietà: SensitivityLabelName, SensitivityLabelId, SensitivityInformationTypeName, SensitivityInformationTypeId e IsClassified (sola lettura). Per altre informazioni, vedere [ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)|
|Classificazione dei dati|Aggiunta della nuova voce di menu "Classification Report" (Report di classificazione) nel riquadro a comparsa "Classificazione dati".|
|Classificazione dei dati| Raccomandazioni aggiornate.|
|Aggiornamento del livello di compatibilità del database|Aggiunta di una nuova opzione in ***Nome database*** > ***Attività*** > ***Aggiornamento database***. Questa opzione consentirà di avviare il nuovo **Assistente ottimizzazione query** per guidare gli utenti nel processo di: Raccolta di baseline delle prestazioni prima dell'aggiornamento del livello di compatibilità del database. Aggiornamento al livello di compatibilità del database desiderato.  Raccolta di un secondo passaggio di dati sulle prestazioni nel corso dello stesso carico di lavoro. Rilevamento delle regressioni del carico di lavoro e specifica di elementi consigliati testati per migliorare le prestazioni del carico di lavoro.  È simile al processo di aggiornamento del database documentato negli [scenari di utilizzo dell'archivio query](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade), tranne nell'ultimo passaggio in cui l'Assistente ottimizzazione query non si basa su uno stato valido noto in precedenza per generare le raccomandazioni.|
|Importazione guidata applicazione livello dati|È stato aggiunto il supporto per l'applicazione livello dati di importazione/esportazione con tabelle grafi.|
|Procedura guidata Importa file flat|Aggiunta della logica per notificare all'utente che un'importazione può aver causato una ridenominazione delle colonne.|
|Integration Services (SSIS)|Aggiunta del supporto per consentire ai clienti di pianificare in Azure-SSIS IR i pacchetti SSIS che si trovano nel cloud di Azure per enti pubblici.|
|Integration Services (SSIS)|Quando si usa il servizio SQL Agent dell'istanza gestita di Azure SQL tramite SSMS, è possibile configurare i parametri e la gestione connessione nel passaggio di processo dell'agente SSIS.|
|Integration Services (SSIS)|Quando ci si connette al database SQL di Azure o a un'istanza gestita di database SQL di Azure, è possibile effettuare la connessione con *default* come database iniziale.|
|Integration Services (SSIS)|Aggiunta della nuova voce **Try SSIS in Azure Data Factory** (Prova SSIS in Azure Data Factory) nel nodo "Cataloghi di Integration Services", che può essere usata per avviare "Integration Runtime Creation Wizard" (Creazione guidata Integration Runtime) e creare rapidamente "Azure-SSIS Integration Runtime".
|Integration Services (SSIS)|Aggiunta del pulsante **Create SSIS IR** (Crea SSIS IR) in "Catalog Creation Wizard" (Creazione guidata catalogo), che può essere usato per avviare "Integration Runtime Creation Wizard" (Creazione guidata Integration Runtime) e creare rapidamente "Azure-SSIS Integration Runtime".|
|Integration Services (SSIS)|ISDeploymentWizard supporta ora l'autenticazione SQL, nonché l'autenticazione integrata e l'autorizzazione tramite password di Azure Active Directory in modalità riga di comando.|
|Integration Services (SSIS)|La distribuzione guidata supporta ora la creazione e la distribuzione in SSIS Integration Runtime di Azure Data Factory.|
|Scripting per gli oggetti|Aggiunta di nuove voci di menu per "CREATE OR ALTER" quando si esegue lo scripting per gli oggetti.|
|Archivio query|Migliorata l'usabilità di alcuni report (Consumo complessivo risorse) grazie all'aggiunta di migliaia di separatori per i numeri visualizzati sull'asse Y dei grafici.|
|Archivio query|Aggiunto un nuovo report Statistiche di attesa query.|
|Archivio query|Aggiunta della metrica "Conteggio esecuzioni" alla vista "Tracked Query" (Query rilevata).|
|Strumenti di replica|Aggiunta del supporto per la funzionalità di specifica delle porte non predefinite in Monitoraggio replica e SSMS.|
|Showplan|Aggiunti il tempo trascorso reale e le righe effettive rispetto alle righe stimate (se disponibili) sotto il nodo dell'operatore ShowPlan. Questa modifica fa sì che il piano effettivo sia coerente con il piano Statistiche query dinamiche.|
|Showplan|Modificata la descrizione comando e aggiunto un commento quando si fa clic sul pulsante Modifica query per un elemento ShowPlan, per indicare all'utente che l'elemento ShowPlan potrebbe essere troncato dal motore SQL se la query supera i 4000 caratteri.|
|Showplan|Aggiunto codice per visualizzare "Materializer Operator (External Select)".|
|Showplan|Aggiunto un nuovo attributo showplan BatchModeOnRowStoreUsed per identificare facilmente le query che usano la funzionalità "batch-mode scan on rowstores". Ogni volta che una query esegue "batch mode scan on rowstores" (analisi in modalità batch su rowstore) viene aggiunto un nuovo attributo (BatchModeOnRowStoreUsed="true") all'elemento StmtSimple.|
|Showplan|Aggiunta del supporto di Showplan a LocalCube RelOp per DW ROLLUP e CUBE.|
|Showplan|Nuovo operatore LocalCube per la nuova funzionalità di aggregazione ROLLUP e CUBE in Azure SQL Data Warehouse.|
|SMO| Supporto SMO esteso per la creazione di indici ripristinabili.|
|SMO| Aggiunto un nuovo evento per gli oggetti SMO ("PropertyMissing") che aiuta gli autori di applicazioni a rilevare i problemi di prestazioni SMO in tempi più rapidi.|
|SMO| Nuova proprietà DefaultBackupChecksum esposta nell'oggetto Configuration, che corrisponde alla configurazione del server "backup checksum default".|
|SMO| Nuova proprietà ProductUpdateLevel inclusa nell'oggetto Server, che esegue il mapping al livello di servizio per la versione di SQL in uso (ad esempio CU12, RTM).|
|SMO| Nuova proprietà LastGoodCheckDbTime inclusa in un oggetto Database, che esegue il mapping alla proprietà del database "lastgoodcheckdbtime". Se tale proprietà non è disponibile, sarà restituito il valore predefinito 1/1/1900 12:00:00 AM.|
|SMO|Percorso del file RegSrvr.xml (file di configurazione Server registrato) spostato in "%AppData%\Microsoft\SQL Server Management Studio"(senza versione, quindi può essere condiviso tra più versioni di SSMS).|
|SMO|Aggiunta di "Cloud di controllo" come nuovo tipo di quorum e nuovo tipo di risorsa.|
|SMO|Aggiunta del supporto per i "vincoli di arco" sia in SMO che in SSMS.|
|SMO|Aggiunto il supporto per l'eliminazione a catena nei "vincoli di arco" sia in SMO che in SSMS.|
|SMO|Aggiunto il supporto dell'autorizzazione di "lettura/scrittura" per la classificazione dei dati.|
|Valutazione della vulnerabilità| Abilitazione del menu delle attività Valutazione della vulnerabilità in Azure SQL DW.|
|Valutazione della vulnerabilità|Modifica del set di regole di valutazione della vulnerabilità eseguito nei server dell'istanza gestita di database SQL di Azure, in modo da rendere coerenti con il database SQL di Azure i risultati dell'analisi di "Valutazione della vulnerabilità".|
|Valutazione della vulnerabilità| "Valutazione vulnerabilità" supporta ora Azure SQL Data Warehouse.|
|Valutazione della vulnerabilità|Aggiunta di una nuova funzionalità per l'esportazione in Excel dei risultati dell'analisi di Valutazione vulnerabilità.|
|Visualizzatore XEvent|Visualizzatore XEvent: abilitata la finestra di showplan per un maggior numero di XEvent.|

### <a name="bug-fixes-in-180"></a>Correzioni di bug nella versione 18.0

| Nuovo elemento| Dettagli|
| :-------| :------|
|Arresti anomali e blocchi|Correzione di un'origine di arresti anomali SSMS comuni associati agli oggetti GDI.|
|Arresti anomali e blocchi|Correzione di un'origine comune di blocchi del sistema e prestazioni insufficienti quando si seleziona "Script come Crea/Aggiorna/Rilascia" (rimosse operazioni inutili di recupero di oggetti SMO).|
|Arresti anomali e blocchi|Correzione di un blocco durante la connessione a un database SQL di Azure con MFA mentre sono abilitate le tracce ADAL.|
|Arresti anomali e blocchi|Correzione di un blocco (o un blocco percepito) in Statistiche query dinamiche chiamato da Monitor attività (il problema si manifesta quando si usa l'autenticazione di SQL Server senza nessuna impostazione "Mantieni informazioni di sicurezza").|
|Arresti anomali e blocchi|Correzione di un blocco quando si seleziona "Report" in Esplora oggetti e si rilevano connessioni con latenza elevata o impossibilità temporanea di accesso alle risorse.|
|Arresti anomali e blocchi|Correzione di un problema di arresto anomalo in SSMS quando si prova a usare il server di gestione centrale e i server SQL di Azure. Per informazioni dettagliate, vedere l'articolo sull'[errore e arresto anomalo dell'applicazione SMSS 17.5 quando si usa il server di gestione centrale](https://feedback.azure.com/forums/908035/suggestions/33374884).|
|Arresti anomali e blocchi|Risolto un blocco in Esplora oggetti mediante l'ottimizzazione del modo in cui viene recuperata la proprietà IsFullTextEnabled.|
|Arresti anomali e blocchi|Correzione di un blocco in "Copia guidata database" evitando la compilazione di query non necessarie per recuperare le proprietà del database.|
|Arresti anomali e blocchi|Correzione di un problema che causa il blocco o l'arresto anomalo di SSMS durante la modifica di T-SQL.|
|Arresti anomali e blocchi|Riduzione di un problema per cui SSMS non risponde durante la modifica di grandi script T-SQL.|
|Arresti anomali e blocchi|Correzione di un problema a causa del quale la memoria di SSMS si esaurisce durante la gestione dei set di dati di grandi dimensioni restituiti dalle query.|
|SQL Server Management Studio (SSMS) - Generale|Correzione di un problema per cui "ApplicationIntent" non veniva passato nelle connessioni in "Server registrati".|
|SQL Server Management Studio (SSMS) - Generale|Correzione di un problema a causa del quale il rendering del modulo dell'interfaccia utente della creazione guidata di una nuova sessione di XEvent non veniva eseguito correttamente nei monitor con valori DPI alti.|
|SQL Server Management Studio (SSMS) - Generale|Correzione di un problema che si verifica durante il tentativo di importare un file bacpac.|
|SQL Server Management Studio (SSMS) - Generale|Correzione di un problema a causa del quale veniva generato un errore di overflow aritmetico durante il tentativo di visualizzare le proprietà di un database (con FILEGROWTH > 2048 GB).|
|SQL Server Management Studio (SSMS) - Generale|Risolto un problema in cui il report Perf Dashboard segnalava attese PAGELATCH e PAGEIOLATCH che non si trovavano nei sottoreport.|
|SQL Server Management Studio (SSMS) - Generale|Un'altra serie di correzioni per fare in modo che SSMS riconosca più monitor e apra una finestra di dialogo nel monitor corretto.|
|Analysis Services|Correzione di un problema per cui "Impostazioni avanzate" per l'interfaccia utente AS Xevent viene troncata.|
|Analysis Services|Risolto un problema per cui l'analisi DAX generava l'eccezione File non trovato.|
|Database SQL di Azure|Correzione di un problema per cui l'elenco di database non veniva compilato correttamente per la finestra delle query del database SQL di Azure in caso di connessione a un database utente nel database SQL di Azure invece che a un database master.|
|Database SQL di Azure|Correzione di un problema per cui non era possibile aggiungere "Tabella temporale" a un database SQL di Azure.|
|Database SQL di Azure|Abilitata l'opzione di sottomenu Proprietà statistiche nel menu Statistiche in Azure, che è ormai completamente supporta da molto tempo.|
|Azure SQL - Supporto generale|Correzione di problemi in un controllo comune dell'interfaccia utente di Azure UI che impedisce all'utente di visualizzare le sottoscrizioni di Azure (se il loro numero è maggiore di 50). Impostazione dell'ordinamento in base al nome anziché in base all'ID sottoscrizione. L'utente poteva trovare questa impostazione ad esempio quando provava a ripristinare un backup da un URL.|
|Azure SQL - Supporto generale|Correzione di un problema nel controllo interfaccia utente di Azure comune a causa del quale l'enumerazione di sottoscrizioni può generare un errore "L'indice non è compreso nell'intervallo. Deve essere non negativo e inferiore al numero di colonne." quando l'utente non aveva sottoscrizioni in alcuni tenant. L'utente poteva trovare questa impostazione ad esempio quando provava a ripristinare un backup da un URL.|
|Azure SQL - Supporto generale|Correzione di un problema per cui gli obiettivi del livello di servizio vengono impostati come hardcoded, rendendo più difficile per SSMS supportare gli obiettivi del livello di servizio più recenti di SQL di Azure. Ora gli utenti possono accedere ad Azure e consentire a SSMS di recuperare tutti i dati degli obiettivi del livello di servizio applicabili (Edition e Max Size)|
|Supporto per l'istanza gestita di database SQL di Azure|Miglioramento del supporto di istanze gestite: disabilitazione delle opzioni non supportate nell'interfaccia utente e risoluzione di un problema di Visualizza log di controllo per la gestione della destinazione di controllo URL.|
|Supporto per l'istanza gestita di database SQL di Azure|La procedura guidata "Genera e pubblica script" include clausole CREATE DATABASE non supportate.|
|Supporto per l'istanza gestita di database SQL di Azure|Abilitazione di Statistiche query dinamiche per le istanze gestite.|
|Supporto per l'istanza gestita di database SQL di Azure|Proprietà database -> File generava codice script errato per ALTER DB ADD FILE.|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione della regressione con l'utilità di pianificazione di SQL Agent in cui la pianificazione ONIDLE veniva scelta anche quando era stato scelto un altro tipo di pianificazione.|
|Supporto per l'istanza gestita di database SQL di Azure|Regolazione di MAXTRANSFERRATE, MAXBLOCKSIZE per i backup in Archiviazione di Azure.|
|Supporto per l'istanza gestita di database SQL di Azure|Problema per cui il backup della parte finale del log viene aggiunto allo script prima dell'operazione RESTORE (operazione non supportata in CL).|
|Supporto per l'istanza gestita di database SQL di Azure|La procedura guidata Crea database non esegue correttamente lo scripting dell'istruzione CREATE DATABASE.|
|Supporto per l'istanza gestita di database SQL di Azure|Gestione speciale dei pacchetti SSIS all'interno di SSMS durante la connessione a istanze gestite.|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione di un problema per cui veniva visualizzato un errore quando si provava a usare "Monitor attività" durante la connessione a istanze gestite.|
|Supporto per l'istanza gestita di database SQL di Azure|Supporto migliorato per l'accesso di AAD (in SSMS Explorer).|
|Supporto per l'istanza gestita di database SQL di Azure|Scripting degli oggetti filegroup di SMO migliorato.|
|Supporto per l'istanza gestita di database SQL di Azure|Interfaccia utente migliorata per le credenziali.|
|Supporto per l'istanza gestita di database SQL di Azure|Supporto aggiunto per la logica di replica.|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione di un problema a causa del quale se si fa clic con il pulsante destro del mouse su un database e si sceglie 'Importa applicazione livello dati', l'operazione ha esito negativo.|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione di un problema a causa del quale se si fa clic con il pulsante destro del mouse su "TempDB" vengono generati errori.|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione di un problema per cui quando si prova a creare lo script dell'istruzione ALTER DB ADD FILE in SMO, lo script T-SQL generato è vuoto.|
|Supporto per l'istanza gestita di database SQL di Azure|Migliorata la visualizzazione di proprietà specifiche del server delle istanze gestite (generazione di hardware, livello di servizio, spazio di archiviazione usato e riservato).|
|Supporto per l'istanza gestita di database SQL di Azure|Correzione di un problema per cui lo scripting di un database ("Script come CREATE") non includeva filegroup e file aggiuntivi. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799). |
|Backup/ripristino/collegamento/scollegamento del database|Correzione di un problema per cui l'utente non è in grado di associare un database quando il nome file fisico del file con estensione mdf non corrisponde al nome file originale.|
|Backup/ripristino/collegamento/scollegamento del database|Correzione di un problema a causa del quale SSMS non trova un piano di ripristino valido o ne trova uno non ottimale. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752). |
|Backup/ripristino/collegamento/scollegamento del database|Risolto un problema per cui nella procedura guidata "Collega database" non venivano visualizzati file secondari rinominati. Ora tali file vengono visualizzati con un commento aggiunto, ad esempio, "Non trovato". Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434). |
|Copia guidata database|Il tentativo di Genera script/Trasferisci/Copia guidata database di creare una tabella con una tabella in memoria non forza ansi_padding on.|
|Copia guidata database|Attività Trasferisci database/Copia guidata database interrotte in SQL Server 2017 e SQL Server 2019.|
|Copia guidata database|Creazione della tabella di script di Genera script/Trasferisci/Copia guidata database prima della creazione di un'origine dati esterni associata.|
|Finestra di dialogo di connessione|Abilitazione della rimozione di nomi utente dall'elenco di nomi utente precedente premendo CANC. Per informazioni dettagliate, vedere l'articolo su come [consentire l'eliminazione di utenti dalla finestra di accesso di SSMS](https://feedback.azure.com/forums/908035/suggestions/32897632).|
|Importazione guidata applicazione livello dati|Correzione di un problema per cui l'importazione guidata di applicazione livello dati non funzionava se connessi tramite AAD.|
|Classificazione dei dati|Correzione di un problema che si verifica quando si salvano le classificazioni nel riquadro di classificazione dei dati mentre sono aperti altri riquadri di classificazione dei dati in altri database.|
|Importazione guidata applicazione livello dati|Correzione di un problema a causa del quale l'utente non poteva importare un'applicazione livello dati (con estensione dacpac) a causa dell'accesso limitato al server (ad esempio nessun accesso a tutti i database nello stesso server).|
|Importazione guidata applicazione livello dati|Risolto un problema che rendeva l'importazione estremamente lenta quando molti database erano ospitati nello stesso server di Azure SQL.|
|Tabelle esterne|Aggiunta del supporto per Rejected_Row_Location in modelli, SMO, IntelliSense e nella griglia delle proprietà.|
|Procedura guidata Importa file flat|Correzione di un problema per cui la procedura guidata "Importa file flat" non gestiva correttamente le virgolette doppie (escape). Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998). |
|Procedura guidata Importa file flat|Correzione di un problema di gestione errata dei tipi a virgola mobile (per impostazioni locali che usano un delimitatore diverso dal punto).|
|Procedura guidata Importa file flat|Correzione di un problema associato all'importazione di bit quando i valori sono 0 o 1. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535). |
|Procedura guidata Importa file flat|Correzione di un problema a causa del quale i valori *float* venivano immessi come *null*.|
|Procedura guidata Importa file flat|Correzione di un problema per cui l'importazione guidata non elaborava valori decimali negativi.|
|Procedura guidata Importa file flat|Correzione di un problema per cui la procedura guidata non eseguiva l'importazione da file CSV a colonna singola.|
|Procedura guidata Importa file flat|[In SSMS 17.9] Correzione di un problema per cui la procedura guidata Importa file flat non consente di cambiare la tabella di destinazione se esiste già. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186). |
|Visualizzatore della Guida|Miglioramento della logica associata al supporto delle modalità online/offline. Alcuni problemi devono essere ancora risolti.|
|Visualizzatore della Guida|Correzione di "Visualizza Guida" per rispettare le impostazioni online/offline. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791). |
|Disponibilità elevata e ripristino di emergenza<BR> Gruppi di disponibilità (disponibilità generale)|Correzione di un problema per cui i ruoli nella procedura guidata "Failover gruppo di disponibilità" vengono sempre visualizzati come "Risoluzione in corso".|
|Disponibilità elevata e ripristino di emergenza<BR> Gruppi di disponibilità (disponibilità generale)|Risolto un problema per cui SSMS visualizzava avvisi troncati nel dashboard del gruppo di disponibilità.|
|Integration Services|Correzione di un problema per cui la distribuzione guidata non si connette a SQL Server quando nello stesso computer sono installati sia SQL Server 2019 che SSMS 18.0.|
|Integration Services|Risolto un problema per cui l'attività di pianificazione della manutenzione non poteva essere modifica al momento della progettazione della pianificazione della manutenzione.|
|Integration Services|Correzione di un problema a causa del quale la distribuzione guidata si blocca se il progetto in distribuzione viene rinominato.|
|Integration Services|Abilitata l'impostazione dell'ambiente nella funzionalità di pianificazione di Azure-SSIS IR.|
|Integration Services|Correzione di un problema per cui la creazione guidata di SSIS Integration Runtime smette di rispondere se l'account utente appartiene a più di 1 tenant.|
|Monitoraggio attività processi|Correzione di un arresto anomalo quando si usa Monitoraggio attività processi (con filtri).|
|Esplora oggetti|Correzione di un problema per cui SSMS genera un'eccezione, ad esempio perché non è possibile eseguire il cast dell'oggetto da DBNull ad altri tipi, quando si prova a espandere il nodo "Gestione" in Esplora oggetti (errore di configurazione di DataCollector).|
|Esplora oggetti|Correzione di un problema per cui Esplora oggetti non applicava escape alle virgolette prima di richiamare "Modifica le prime righe"rendendo confusa la finestra di progettazione.|
|Esplora oggetti|Correzione di un problema per cui la procedura guidata "Importare un'applicazione livello dati" non viene avviata dalla struttura di Archiviazione di Azure.|
|Esplora oggetti|Correzione di un problema per cui in "Configurazione Posta elettronica database" lo stato della casella di controllo SSL non veniva mantenuto. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541). |
|Esplora oggetti|Correzione di un problema per cui in SSMS l'opzione Chiudi connessioni esistenti viene disattivata quando si prova a ripristinare il database con is_auto_update_stats_async_on.|
|Esplora oggetti|Correzione di un problema a causa del quale quando si faceva clic con il pulsante destro del mouse sui nodi in Esplora oggetti, ad esempio "Tabelle", e si voleva eseguire un'azione come ad esempio filtrare le tabelle selezionando Filtro > Impostazioni filtro, le impostazioni di filtro potevano essere visualizzate in un altro schermo rispetto a quello in cui SSMS era attivo. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106). |
|Esplora oggetti|Correzione di un problema rilevato da tempo per cui CANC non funzionava in Esplora oggetti quando si tentava di rinominare un oggetto. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510](https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510), [https://feedback.azure.com/forums/908035/suggestions/32910247](https://feedback.azure.com/forums/908035/suggestions/32910247) e altri duplicati.|
|Esplora oggetti|Quando si visualizzano le proprietà di file di database esistenti, le dimensioni vengono visualizzate in una colonna "Dimensioni (MB)" anziché "Dimensioni iniziali (MB)", che è la colonna visualizzata quando si crea un nuovo database. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024](https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024). |
|Esplora oggetti|Disattivazione della voce di menu contestuale "Progettazione" in "Tabelle grafi" perché queste tabelle non sono supportate nella versione corrente di SSMS.|
|Esplora oggetti|Correzione di un problema per cui la finestra di dialogo "Nuova pianificazione processo" non veniva visualizzata correttamente nei monitor con valori DPI alti. Per informazioni dettagliate, vedere [https://feedback.azure.com/admin/v3/suggestions/35541262](https://feedback.azure.com/admin/v3/suggestions/35541262). |
|Esplora oggetti|Correzione del problema e ottimizzazione della visualizzazione delle dimensioni del database ("Dimensioni (MB)") in Esplora oggetti. Si usano solo 2 cifre decimali e il separatore delle migliaia. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/34379308](https://feedback.azure.com/forums/908035/suggestions/34379308).|
|Esplora oggetti|Correzione di un problema che impedisce la creazione di un "Indice spaziale" con un errore analogo a "Per eseguire questa azione, impostare la proprietà PartitionScheme".|
|Esplora oggetti|Miglioramenti delle prestazioni minori in Esplora oggetti per evitare di eseguire query aggiuntive, quando possibile.|
|Esplora oggetti|Estensione della logica per richiedere una conferma quando si rinomina un database per tutti gli oggetti dello schema (l'impostazione può essere configurata).|
|Esplora oggetti|Aggiunto il corretto escape nel filtro di Esplora oggetti. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/36678803](https://feedback.azure.com/forums/908035/suggestions/36678803). |
|Esplora oggetti|Correzione/ottimizzazione della visualizzazione in Dettagli Esplora oggetti per mostrare i numeri con i separatori corretti. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/32900944](https://feedback.azure.com/forums/908035/suggestions/32900944). |
|Esplora oggetti|Correzione del menu di scelta rapida nel nodo "Tabelle" per cui, quando ci si connette a SQL Express, il riquadro a comparsa "Nuovo" è mancante, le tabelle grafi vengono visualizzate in modo non corretto e la tabella System-Versioned è mancante. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/37245529](https://feedback.azure.com/forums/908035/suggestions/37245529). |
|Scripting per gli oggetti|Miglioramento delle prestazioni generali: la generazione di script WideWorldImporters viene eseguita in metà tempo rispetto a SSMS 17.7.|
|Scripting per gli oggetti|Durante lo scripting di oggetti la configurazione con ambito database con valori predefiniti viene omessa.|
|Scripting per gli oggetti|Evitare di generare T-SQL dinamico durante lo scripting. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391). |
|Scripting per gli oggetti|Omettere le sintassi dei grafi "as edge" e "as node" per lo scripting di una tabella in SQL Server 2016 e versioni precedenti.|
|Scripting per gli oggetti|Correzione di un problema per cui non è possibile eseguire lo script degli oggetti di database quando si usa AAD con MFA per connettersi al database SQL di Azure.|
|Scripting per gli oggetti|Correzione di un problema per cui il tentativo di creare lo script di un indice spaziale con GEOMETRY_AUTO_GRID/GEOGRAPHY_AUTO_GRID in un database SQL di Azure generava un errore.|
|Scripting per gli oggetti|Correzione di un problema a causa del quale gli script di un database SQL di Azure usavano sempre come destinazione un'istanza di SQL locale, anche se le impostazioni di scripting di "Esplora oggetti" erano definite in modo da corrispondere all'origine.|
|Scripting per gli oggetti|Correzione di un problema per cui durante il tentativo di creare lo script di una tabella in un database SQL Data Warehouse che include indici cluster e non cluster vengono generate istruzioni T-SQL non corrette.|
|Scripting per gli oggetti|Correzione di un problema per cui durante il tentativo di creare lo script di una tabella in un database SQL Data Warehouse con indici columnstore cluster e indici cluster vengono generate istruzioni T-SQL non corrette (duplicate).|
|Scripting per gli oggetti|Correzione del problema di scripting di tabelle partizionate senza valori di intervallo (database SQL Data Warehouse).|
|Scripting per gli oggetti|Correzione di un problema per cui l'utente non è in grado di creare lo script di un controllo o di una specifica di controllo SERVER_PERMISSION_CHANGE_GROUP.|
|Scripting per gli oggetti|Correzione di un problema per cui l'utente non è in grado di creare lo script di statistiche da SQL Data Warehouse. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296). |
|Scripting per gli oggetti|Correzione di un problema per cui la "Generazione guidata script" visualizza una tabella errata con un errore di scripting se l'opzione "Continua generazione di script in caso di errore" è impostata su False.|
|Scripting per gli oggetti|Miglioramento della generazione di script in SQL Server 2019.|
|Profiler|Aggiunta dell'evento "Aggregate Table Rewrite Query" (Aggrega query di riscrittura tabella) agli eventi Profiler.|
|Query Data Store|Correzione di un problema per cui si può generare un'eccezione "DocumentFrame (SQLEditors)".|
|Query Data Store|Correzione di un problema che si verificava nel tentativo di impostare un intervallo di tempo personalizzato nei report predefiniti di Query Store. L'utente non poteva selezionare AM o PM nell'intervallo iniziale/finale.|
|Griglia dei risultati|Correzione di un problema in modalità Contrasto elevato (i numeri di riga selezionati non erano visibili).|
|Griglia dei risultati|Correzione di un problema che generava un'eccezione "Indice fuori intervallo" quando si faceva clic sulla griglia.|
|Griglia dei risultati|Risolto un problema in cui è il colore di sfondo della griglia risultati veniva ignorato. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916). |
|Showplan|Vengono visualizzate le proprietà del nuovo operatore di concessione memoria quando esiste più di un thread.|
|Showplan|Aggiungere i seguenti 4 attributi in RunTimeCountersPerThread del piano di esecuzione xml: HpcRowCount (numero di righe elaborate dal dispositivo hpc), HpcKernelElapsedUs (tempo di attesa scaduto per l'esecuzione del kernel in uso), HpcHostToDeviceBytes (byte trasferiti dall'host al dispositivo) e HpcDeviceToHostBytes (byte trasferiti dal dispositivo all'host).|
|Showplan|Correzione di un problema per cui i nodi di piano simili vengono evidenziati nella posizione errata.|
|SMO|Correzione di un problema per cui SMO/ServerConnection non gestisce correttamente le connessioni basate su SqlCredential. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941). |
|SMO|Correzione di un problema per cui un'applicazione scritta con SQL Server Management Objects (SMO) genera un errore se si tenta di enumerare i database dallo stesso server in più thread, anche se usa istanze di SqlConnection diverse in ogni thread.|
|SMO|Correzione della regressione delle prestazioni durante il trasferimento da tabelle esterne.|
|SMO|Correzione del problema nel thread safety ServerConnection a causa del quale l'interfaccia SMO perdeva istanze di SqlConnection con la destinazione Azure.|
|SMO|Correzione di un problema che causava un errore StringBuilder.FormatError durante il tentativo di ripristinare un database con parentesi graffe nel nome.|
|SMO|Correzione di un problema per cui i database di Azure in SMO usano per impostazione predefinita le regole di confronto senza distinzione tra maiuscole e minuscole per tutti i confronti tra stringhe invece di usare le regole di confronto specificate per il database.|
|Editor SSMS|Correzione di un problema a causa del quale nella "Tabella di sistema SQL" il ripristino dei colori predefiniti impostava il colore verde limone invece del verde predefinito, rendendo difficile la lettura su uno sfondo bianco. Per informazioni dettagliate, vedere l'articolo sul [ripristino del colore predefinito errato per la tabella di sistema SQL](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906). Questo problema persiste ancora nelle versioni di SSMS non in lingua inglese.|
|Editor SSMS|Correzione di un problema per cui IntelliSense non funzionava quando si usava l'autenticazione AAD per connettersi ad Azure SQLDW.|
|Editor SSMS|Correzione di un problema di IntelliSense in Azure quando l'utente non ha accesso al database **master**.|
|Editor SSMS|Corretti frammenti di codice per la creazione di "tabelle temporanee" che venivano interrotti quando le regole di confronto del database di destinazione facevano distinzione tra maiuscole e minuscole.|
|Editor SSMS|Nuova funzione TRANSLATE ora riconosciuta da IntelliSense. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430). |
|Editor SSMS|Funzionalità IntelliSense migliorata nella funzione FORMAT predefinita. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676). |
|Editor SSMS|LAG e LEAD vengono ora riconosciuti come funzioni predefinite. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757). |
|Editor SSMS|Correzione di un problema per cui IntelliSense genera un avviso quando si usa "ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)".|
|Editor SSMS|Correzione di un problema a causa del quale varie viste di sistema e funzioni con valore di tabella non erano colorate correttamente.|
|Editor SSMS|Correzione di un problema per cui quando si fa clic su una scheda dell'editor, questa si chiude invece di ricevere lo stato attivo. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/37291114](https://feedback.azure.com/forums/908035/suggestions/37291114). |
|Opzioni SSMS|Correzione di un problema per cui la pagina **Strumenti** > **Opzioni** > **Esplora oggetti di SQL Server** > **Comandi** non veniva ridimensionata correttamente.|
|Opzioni SSMS|Per impostazione predefinita, SSMS ora disabilita il download automatico di DTD nell'editor XMLA. L'editor di script XMLA usa il servizio di linguaggio XML e per impostazione predefinita impedisce ora di scaricare automaticamente DTD per file XMLA potenzialmente dannosi. Questo comportamento viene controllato disattivando l'impostazione "Scarica automaticamente le DTD e gli schemi" in **Strumenti** > **Opzioni** > **Ambiente** > **Editor di testo** > **XML** > **Varie**.|
|Opzioni SSMS|Ripristinata la scelta rapida da tastiera **CTRL+D**, disponibile nella versione precedente di SSMS. Per informazioni dettagliate, vedere [https://feedback.azure.com/forums/908035/suggestions/35544754](https://feedback.azure.com/forums/908035/suggestions/35544754). |
|Progettazione tabelle|Correzione di un arresto anomalo in "Modifica 200 righe".|
|Progettazione tabelle|Correzione di un problema per cui la finestra di progettazione consente l'aggiunta di una tabella durante la connessione a un database Azure SQL.|
|Valutazione della vulnerabilità|Correzione di un problema per cui i risultati dell'analisi non vengono caricati correttamente.|
|XEvent|Aggiunte due colonne "action_name" e "class_type_desc" che visualizzano i campi ID azione e tipo classe come stringhe leggibili.|
|XEvent|Rimosso il limite massimo di 1.000.000 di eventi per il visualizzatore XEvent.|
|Profiler XEvent|Correzione di un problema per cui il profiler XEvent non veniva avviato se connesso a un server SQL Server a 96 nuclei.|
|Visualizzatore XEvent|Correzione di un problema per cui il visualizzatore XEvent si arresta in modo anomalo quando si prova a raggruppare gli eventi usando le opzioni della barra degli strumenti Eventi estesi.|

### <a name="deprecated-and-removed-features-in-180"></a>Funzionalità deprecate e rimosse nella versione 18.0

Funzionalità deprecate e rimosse
- Debugger Transact-SQL
- Diagrammi di database
- Gli strumenti seguenti non vengono più installati con SSMS:
  - OSQL.EXE
  - DReplay.exe
  - SQLdiag.exe
  - SSBDiagnose.exe
  - bcp.exe
  - sqlcmd.exe
- Strumenti di Configuration Manager:
  - Gestione configurazione SQL Server e Gestione configurazione server di report non sono più inclusi nell'installazione di SSMS.
- Criteri standard DMF
  - I criteri non vengono più installati con SSMS. Verranno spostati in Git. Gli utenti potranno contribuire allo sviluppo e scaricarli/installarli in base alle esigenze.
- Opzione della riga di comando -P di SSMS rimossa
  - A causa di problemi di sicurezza, l'opzione per specificare password non crittografate nella riga di comando è stata rimossa.
- Rimozione dell'opzione Genera script > Pubblica su servizio Web
  - Questa funzionalità deprecata è stata rimossa dall'interfaccia utente di SSMS.
- Rimozione del nodo "Manutenzione > Legacy" di Esplora oggetti.
  - I nodi obsoleti "Piani di manutenzione del database" e "SQL Mail" non saranno più accessibili. I nodi recenti "Posta elettronica database" e "Piani di manutenzione" funzionano come di consueto.

### <a name="known-issues-180"></a>Problemi noti (18.0)

- Si potrebbe verificare un problema durante l'installazione della versione 18.0, per cui non è possibile eseguire SQL Server Management Studio. Se si verifica questo problema, seguire la procedura descritta nell'articolo [SSMS2018: installato, ma non viene eseguito](https://feedback.azure.com/forums/908035-sql-server/suggestions/37502512-ssms2018-installed-but-will-not-run).

- Esiste una limitazione alle dimensioni dei dati visualizzati dai risultati di SSMS in griglia, testo o file

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>![Scaricare](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- Numero di versione: 17.9.1<br>
- Numero di build: 14.0.17289.0<br>
- Data di rilascio: 21 novembre 2018

17.9.1 è un aggiornamento di piccole dimensioni della versione 17.9 con le correzioni di bug seguenti:

- Correzione di un problema a causa del quale la connessione degli utenti veniva chiusa e riaperta ogni volta che veniva chiamata una query durante l'uso dell'autenticazione "Azure Active Directory - Universale con supporto MFA" con l'editor di query SQL. Gli effetti collaterali della chiusura della connessione includevano il rilascio imprevisto delle tabelle temporanee e talvolta l'assegnazione di un nuovo SPID alla connessione.
- Risolto un problema che persisteva da tempo per cui il piano di ripristino poteva non trovare o generare un piano di ripristino inefficiente in determinate condizioni.
- Correzione di un problema nella procedura guidata "Importa applicazione livello dati" che poteva causare un errore durante la connessione a un database SQL di Azure.

> [!NOTE]
> Le versioni di SSMS 17.x localizzate in lingue diverse dall'inglese richiedono il [pacchetto di aggiornamento della sicurezza KB 2862966](https://support.microsoft.com/kb/2862966) se sono installate in Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [Francese](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [Tedesco](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [Giapponese](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![Download](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
Disponibilità generale| Numero di build: 13.0.16106.4

[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [Francese](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [Tedesco](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [Giapponese](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [Spagnolo](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

In questa versione sono stati risolti i problemi seguenti:

* Correzione di un problema introdotto in SSMS 16.5.2 che causava l'espansione del nodo 'Tabella' quando la tabella aveva più di una colonna di tipo sparse.

* Gli utenti possono distribuire pacchetti SSIS contenenti Gestione connessione OData per connettere una risorsa Microsoft Dynamics AX/CRM Online al catalogo SSIS. Per altre informazioni dettagliate, vedere [Gestione connessione OData](../integration-services/connection-manager/odata-connection-manager.md).

* La configurazione di Always Encrypted per una tabella esistente ha esito negativo con errori per gli oggetti correlati. [ID Connect 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* La configurazione di Always Encrypted per un database esistente con più schemi non funziona. [ID Connect 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* La procedura guidata Always Encrypted, Colonna crittografata ha esito negativo a causa del database che contiene viste che fanno riferimento a viste di sistema. [ID Connect 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Durante la crittografia con Always Encrypted, gli errori derivanti dall'aggiornamento dei moduli dopo la crittografia non vengono gestiti in modo corretto.

* Il menu *Apri recenti* non mostra i file salvati di recente. [ID Connect 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS è lento quando si fa clic con il pulsante destro del mouse su un indice per una tabella (tramite una connessione Internet remota). [ID Connect 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)

* Risolto un problema con la barra di scorrimento di SQL Designer. [ID Connect 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* Il menu di scelta rapida per le tabelle si blocca momentaneamente 
 
* SSMS in alcuni casi genera eccezioni in Monitoraggio attività e subisce un arresto anomalo. [ID Connect 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* Si verifica un arresto anomalo di SSMS 2016 con l'errore "Il processo è stato terminato a causa di un errore interno del runtime .NET in IP 71AF8579 (71AE0000) con codice di uscita 80131506"


## <a name="uninstall-and-reinstall-ssms-17x"></a>Disinstallare e reinstallare SSMS 17.x

Se si verificano problemi durante l'installazione di SSMS che non vengono risolti con una disinstallazione e reinstallazione standard, è possibile provare a [ripristinare](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs) Visual Studio 2015 Isolated Shell. Se il ripristino di Visual Studio 2015 Isolated Shell non risolve il problema, la procedura seguente consente di risolvere molti problemi casuali:

1. Disinstallare SSMS nello stesso modo in cui si disinstalla qualsiasi applicazione, usando *App e funzionalità*, *Programmi e funzionalità*, a seconda della versione di Windows in uso.

2. Disinstallare Visual Studio 2015 Isolated Shell **da un prompt dei comandi con privilegi elevati**:

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3. Disinstallare Microsoft Visual C++ 2015 Redistributable nello stesso modo in cui si disinstalla un'applicazione qualsiasi. Disinstallare sia la versione x86 che la x64 se sono entrambe presenti nel computer.

4. Reinstallare Visual Studio 2015 Isolated Shell **da un prompt dei comandi con privilegi elevati**:  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  

    ```vs_isoshell.exe /PromptRestart```

5. Reinstallare SSMS.

6. Eseguire l'aggiornamento alla [versione più recente di Visual C++ 2015 Redistributable](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) se non è già stato fatto.

## <a name="additional-downloads"></a>Download aggiuntivi

Per un elenco di tutti i download di SQL Server Management Studio, vedere [Area download Microsoft](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Per la versione più recente di SQL Server Management Studio, vedere [Scaricare SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
