---
title: Catalogo del database WideWorldImporters OLTP - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e26299f221facfc6828369e1c75225f206937eb4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579581"
---
# <a name="wideworldimporters-database-catalog"></a>Catalogo del database WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Il database WideWorldImporters contiene tutte le le informazioni sulle transazioni e dei dati giornaliera per vendite e acquisti, nonché i dati del sensore per veicoli e chat ad accesso sporadico.

## <a name="schemas"></a>Schemi

WideWorldImporters Usa gli schemi per scopi diversi, ad esempio l'archiviazione dei dati, la definizione come gli utenti possono accedere ai dati e fornendo gli oggetti per l'integrazione e sviluppo di data warehouse.

### <a name="data-schemas"></a>Schemi di dati

Gli schemi includano i dati. Alcune tabelle è necessarie per tutti gli altri schemi e si trova nello schema dell'applicazione.

|schema|Descrizione|
|-----------------------------|---------------------|
|Applicazione|Gli utenti a livello di applicazione, contatti e i parametri. Contiene anche le tabelle di riferimento con i dati che viene usati in più schemi|
|Purchasing|Elemento titolo acquista da fornitori e i dettagli relativi ai fornitori.|  
|Sales|Titolo elemento vendita ai clienti di vendita al dettaglio e i dettagli relativi alle persone di vendite e clienti. |  
|Warehouse|Inventario di magazzino e le transazioni.|  

### <a name="secure-access-schemas"></a>Schemi di accesso sicuro

Questi schemi vengono utilizzati per le applicazioni esterne che non sono consentite per accedere direttamente alle tabelle di dati. Contengono le viste e stored procedure utilizzate dalle applicazioni esterne.

|schema|Descrizione|
|-----------------------------|---------------------|
|Sito Web|Tutti gli accessi al database dal sito Web della società sono tramite questo schema.|
|Report|Tutti gli accessi al database da report di Reporting Services sono tramite questo schema.|
|PowerBI|Tutti gli accessi al database dal dashboard di Power BI tramite il Gateway aziendale sono tramite questo schema.|

Si noti che i report e Power BI gli schemi non vengono utilizzati nella versione iniziale del database di esempio. Tuttavia, gli esempi di tutti i Reporting Services e Power BI basati su questo database sono invitati a usare questi schemi.

### <a name="development-schemas"></a>Schemi di sviluppo

Schemi con finalità speciali

|schema|Descrizione|
|-----------------------------|---------------------|
|Integrazione|Gli oggetti e le procedure necessari per l'integrazione di data warehouse (ad esempio la migrazione dei dati nel database WideWorldImportersDW).|
|Sequenze|Contiene le sequenze usate da tutte le tabelle nell'applicazione.|

## <a name="tables"></a>Tabelle

Tutte le tabelle nel database sono negli schemi di dati.

### <a name="application-schema"></a>Schema dell'applicazione

Dettagli dei parametri e gli utenti (utenti e contatti), insieme a tabelle di riferimento comuni (comuni a più altri schemi).

|Tabella|Descrizione|
|-----------------------------|---------------------|
|SystemParameters|Contiene i parametri configurabili a livello di sistema.|
|Utenti|Contiene i nomi utente, informazioni di contatto, per tutti coloro che usano l'applicazione e per le persone che si occupa di Wide World Importers in organizzazioni del cliente. Ciò include personale, i clienti, fornitori e gli eventuali altri contatti. Per gli utenti che dispongono dell'autorizzazione per utilizzare il sistema o un sito Web, le informazioni includono i dettagli di accesso.|
|Città|Esistono molti indirizzi archiviati nel sistema, per gli utenti, indirizzi di recapito di organizzazione dei clienti, gli indirizzi di inizio corsa a fornitori e così via. Ogni volta che viene archiviato un indirizzo, è presente un riferimento a una città in questa tabella. È inoltre disponibile una posizione spaziale per ogni città.|
|StateProvinces|Città fanno parte di stati o province. Questa tabella contiene i dettagli di questi strumenti, tra cui i dati spaziali che descrive i limiti di ogni stato o provincia.|
|Countries|Stati o province fanno parte di terzi. Questa tabella contiene i dettagli di questi strumenti, tra cui i dati spaziali che descrive i limiti di ogni paese.|
|DeliveryMethods|Possibilità per fornire elementi azionari (ad esempio, furgone/furgone, post, pickup, courier e così via)|
|PaymentMethods|Opzioni per eseguire pagamenti (ad esempio, contanti, assegno, EFT, ecc.)|
|TransactionTypes|Tipi di clienti, fornitore o transazioni azionarie (ad esempio, fatturazione, nota di credito e così via)|

### <a name="purchasing-schema"></a>Schema di acquisto

Dettagli di fornitori e acquisti in magazzino.

|Tabella|Descrizione|
|-----------------------------|---------------------|
|Suppliers|Tabella dell'entità principale dei fornitori (organizzazioni)|
|SupplierCategories|Categorie dei fornitori (ad esempio, novità, toys, clothing, creazione di pacchetti e così via).|
|SupplierTransactions|Tutte le transazioni finanziarie che sono correlati al fornitore (fatture, pagamenti)|
|PurchaseOrders|Gli ordini di acquisto dei dettagli del fornitore|
|PurchaseOrderLines|Le righe di dettaglio da fornitori di ordini di acquisto|

 
### <a name="sales-schema"></a>Schema di vendita

Dettagli di clienti, i venditori e delle vendite in magazzino.

|Tabella|Descrizione|
|-----------------------------|---------------------|
|Customers|Tabelle di entità principale per i clienti (aziende o utenti singoli)|
|CustomerCategories|Categorie per i clienti (ad esempio archivi originalità supermercati, e così via.)|
|BuyingGroups|Le organizzazioni dei clienti possono far parte di gruppi di esercitare un maggiore potenza di acquisto|
|CustomerTransactions|Tutte le transazioni finanziarie che sono correlati al cliente (fatture, pagamenti)|
|SpecialDeals|Prezzi speciali. Questo può includere prezzi fissi, discount in dollari o percentuale di sconto.|
|Orders|Dettagli di ordini dei clienti|
|OrderLines|Righe di dettaglio degli ordini cliente|
|Fatture|Dettagli di fatture dei clienti|
|InvoiceLines|Righe di dettaglio da fatture dei clienti|

### <a name="warehouse-schema"></a>Schema del warehouse

Dettagli elementi azionari, le aziende e le transazioni.

|Tabella|Descrizione|
|-----------------------------|---------------------|
|StockItems|Tabella dell'entità principale per gli elementi di scorte|
|StockItemHoldings|Colonne non temporali per gli elementi di scorte. Queste sono le colonne aggiornate di frequente.|
|StockGroups|Gruppi per la classificazione titoli degli articoli (ad esempio, novità, toys, novità commestibili e così via)|
|StockItemStockGroups|Quali azioni sono gli elementi in cui stock Raggruppa (molti a molti)|
|Colori|Gli elementi azionari (facoltativamente) possono avere colori|
|PackageTypes|Modi in cui gli elementi delle scorte possono essere incluso nel pacchetto (ad esempio, casella carton, gruppo, kg, e così via.|
|StockItemTransactions|Transazioni che coprono tutti gli spostamenti di tutti gli elementi azionari (ricezione, la vendita, annullamento)|
|VehicleTemperatures|Regolarmente registrate le temperature di chillers del veicolo|
|ColdRoomTemperatures|Regolarmente registrate le temperature di chillers chat room ad accesso sporadico|


## <a name="design-considerations"></a>Considerazioni di progettazione

Progettazione di database è soggettiva e non è possibile progettare un database giusto o sbagliato. Gli schemi e tabelle in questo database mostrano le idee per come è possibile progettare il proprio database.

### <a name="schema-design"></a>Progettazione dello schema

WideWorldImporters Usa un numero ridotto di schemi in modo che sia facile da comprendere il sistema di database e illustrano i principi di database.  

Laddove possibile, il database colloca le tabelle che vengono in genere eseguite query nello stesso schema per ridurre al minimo la complessità di join.

Lo schema del database è stata generata dal codice basato su una serie di tabelle di metadati in un altro database WWI_Preparation. In questo modo WideWorldImporters un livello molto elevato di coerenza di progettazione, denominazione coerenza e completezza. Per informazioni dettagliate sul modo in cui è stato generato lo schema, vedere il codice sorgente: [wide-world-utilità di importazione/wwi-database-scripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Progettazione di tabelle

- Tutte le tabelle hanno chiavi primarie di colonna singola per motivi di semplicità di join.
- Tutti gli schemi, tabelle, colonne, indici e vincoli check associata una descrizione della proprietà che può essere utilizzato per identificare lo scopo dell'oggetto o colonna estesa. Le tabelle ottimizzate per la memoria sono un'eccezione a questa perché attualmente non supporta le proprietà estese.
- Tutte le chiavi esterne vengono indicizzate automaticamente a meno che non è un altro indice non cluster con lo stesso componente a sinistra.
- Numerazione automatica nelle tabelle è basata su sequenze. Queste sequenze sono più facili da usare in ambienti simili rispetto alle colonne di identità e i server collegati. Le tabelle ottimizzate per la memoria usano colonne IDENTITY perché non supportano in SQL Server 2016.
- Una singola sequenza (TransactionID) viene usata per queste tabelle: CustomerTransactions SupplierTransactions e StockItemTransactions. Ciò dimostra come un set di tabelle può avere un'unica sequenza.
- Alcune colonne contengono valori predefiniti appropriati.

### <a name="security-schemas"></a>Schemi di sicurezza

Per la sicurezza, WideWorldImporters non consente le applicazioni esterne accedere direttamente gli schemi di dati. Per isolare l'accesso, WideWorldImporters Usa gli schemi di accesso di sicurezza che non contengono dati, ma contengono viste e stored procedure. Le applicazioni esterne usano gli schemi di sicurezza per recuperare i dati che sono autorizzati a visualizzare.  In questo modo, gli utenti possono eseguire soltanto le viste e stored procedure negli schemi di accesso sicuro

Ad esempio, in questo esempio include i dashboard di Power BI. Un'applicazione esterna consente di accedere ai dashboard di Power BI dal gateway di Power BI come utente che dispone dell'autorizzazione di sola lettura per lo schema di Power BI.  L'autorizzazione di sola lettura, l'utente deve solo l'autorizzazione SELECT ed EXECUTE per lo schema di Power BI. Un amministratore del database WWI vengono assegnate queste autorizzazioni in base alle esigenze.

## <a name="stored-procedures"></a>Stored procedure

Le stored procedure sono organizzate in schemi. La maggior parte degli schemi vengono usata per la configurazione o a scopo di esempio.

Il `Website` schema contiene le stored procedure che possono essere usate da un front-end Web.

Il `Reports` e `PowerBI` gli schemi sono pensati per reporting services e a scopo di Power BI. Tutte le estensioni dell'esempio sono invitate a usare gli schemi per la creazione di report.

### <a name="website-schema"></a>Schema di sito Web

Queste sono le procedure utilizzate da un'applicazione client, ad esempio un Web front-end.

|Routine|Scopo|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Consente a una persona (da `Application.People`) di accedere al sito Web.|
|ChangePassword|Modifica password dell'utente (per gli utenti che non usano meccanismi di autenticazione esterni).|
|InsertCustomerOrders|Consente l'inserimento di uno o più ordini di clienti (incluse le righe d'ordine).|
|InvoiceCustomerOrders|Accetta un elenco di ordini di ricevere una fattura ed elabora le fatture.|
|RecordColdRoomTemperatures|Accetta un elenco di dati di sensori, come un parametro con valori di tabella (TVP) e applica i dati per il `Warehouse.ColdRoomTemperatures` tabella temporale.|
|RecordVehicleTemperature|Accetta una matrice JSON e lo usa per aggiornare `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Esegue la ricerca per i clienti per nome o parte del nome (il nome della società o il nome di persona).|
|SearchForPeople|Cerca persone per nome o parte del nome.|
|SearchForStockItems|Cerca le voci dal nome o parte del nome o i commenti di marketing.|
|SearchForStockItemsByTags|Cerca le voci dai tag.|
|SearchForSuppliers|Consente di cercare fornitori per nome o parte del nome (il nome della società o il nome di persona).|

### <a name="integration-schema"></a>Schema di integrazione

Le stored procedure in questo schema vengono utilizzate dal processo ETL. Ottengono i dati necessari da diverse tabelle per l'intervallo di tempo necessari per il [pacchetto ETL semplice](wide-world-importers-perform-etl.md).

### <a name="dataloadsimulation-schema"></a>Schema DataLoadSimulation

Simula un carico di lavoro che inserisce le vendite e acquisti. La stored procedure principale è `PopulateDataToCurrentDate`, che consente di inserire i dati di esempio fino alla data corrente.

|Routine|Scopo|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Crea nuovamente le procedure necessarie per i dati di simulazione di carico. È necessario per spostare i dati fino alla data corrente.|
|Configuration_RemoveDataLoadSimulationProcedures|Questa operazione rimuove le procedure nuovamente dopo la simulazione di dati è stata completata.|
|DeactivateTemporalTablesBeforeDataLoad|Rimuove la natura temporale di tutte le tabelle temporali e laddove, viene applicato un trigger in modo che è possibile apportare modifiche come se sono stati applicati a una data precedente rispetto a consentono le tabelle temporali con sys.|
|PopulateDataToCurrentDate|Utilizzato per visualizzare i dati fino alla data corrente. Deve essere eseguito prima di qualsiasi altra opzione di configurazione dopo il ripristino del database da un backup iniziale.|
|ReactivateTemporalTablesAfterDataLoad|Ristabilisce le tabelle temporali, inclusi controllo della coerenza dei dati. (Rimuove i trigger associati).|


### <a name="application-schema"></a>Schema dell'applicazione

Queste procedure vengono utilizzate per configurare l'esempio. Vengono utilizzati per applicare le funzionalità dell'edizione enterprise per la versione standard edition dell'esempio, nonché per aggiungere il controllo e l'indicizzazione full-text.

|Routine|Scopo|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Aggiunge un membro a un ruolo se non è già membro del ruolo|
|Configuration_ApplyAuditing|Aggiunge il controllo. Il controllo server viene applicato per i database standard edition; il controllo del database aggiuntivo viene aggiunta per enterprise edition.|
|Configuration_ApplyColumnstoreIndexing|Si applica a indici columnstore `Sales.OrderLines` e `Sales.InvoiceLines` e reindexes in modo appropriato.|
|Configuration_ApplyFullTextIndexing|Si applica a indici full-text per `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, e `Warehouse.StockItems`. Sostituisce `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` con le procedure di sostituzione che usano l'indicizzazione full-text.|
|Configuration_ApplyPartitioning|Si applica al partizionamento delle tabelle `Sales.CustomerTransactions` e `Purchasing.SupplierTransactions`e consente di riorganizzare gli indici in base alle proprie.|
|Configuration_ApplyRowLevelSecurity|Applica la sicurezza a livello di riga per filtrare i clienti per sales territory relativi ruoli.|
|Configuration_ConfigureForEnterpriseEdition|Si applica l'indicizzazione columnstore, full-text, in memoria, polybase e partizionamento.|
|Configuration_EnableInMemory|Aggiunge un filegroup ottimizzato per la memoria (quando non funziona in Azure), sostituisce `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` con gli equivalenti in memoria e viene eseguita la migrazione dei dati, verrà ricreata la `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` tipi con le tabelle equivalenti ottimizzate per la memoria, Elimina e crea nuovamente le procedure descritte `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, e `Website.RecordColdRoomTemperatures` che usa questi tipi di tabella.|
|Configuration_RemoveAuditing|Rimuove la configurazione di controllo.|
|Configuration_RemoveRowLevelSecurity|Rimuove la configurazione di sicurezza a livello di riga (questa è necessaria per le modifiche apportate alle tabelle associate).|
|CreateRoleIfNonExistant|Crea un ruolo del database se non esiste già.|


### <a name="sequences-schema"></a>Schema di sequenze

Procedure per configurare le sequenze nel database.

|Routine|Scopo|
|-----------------------------|---------------------|
|ReseedAllSequences|Chiama la routine ReseedSequenceBeyondTableValue per tutte le sequenze.|
|ReseedSequenceBeyondTableValue|Usato per riposizionare il valore di sequenza successivo oltre il valore in qualsiasi tabella che utilizza la stessa sequenza. (Ad esempio, un DBCC CHECKIDENT per equivalente a colonne identity per le sequenze ma tra potenzialmente più tabelle).|
