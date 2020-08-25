---
title: Caricare con Integration Services
description: Vengono fornite informazioni di riferimento e di distribuzione per il caricamento di dati in Parallel data warehouse (PDW) utilizzando pacchetti di SQL Server Integration Services (SSIS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ea2a4f39b16fe2f8b23d6a6a229ce9b936e6e6d7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766760"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Caricare i dati con Integration Services in parallelo data warehouse
Fornisce informazioni di riferimento e distribuzione per il caricamento di dati in SQL Server data warehouse parallele mediante pacchetti SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="basics"></a><a name="Basics"></a>Nozioni di base  
Integration Services è il componente di SQL Server per l'estrazione, la trasformazione e il caricamento (ETL) a prestazioni elevate di dati e viene comunemente utilizzato per popolare e aggiornare un data warehouse.  
  
L'adattatore di destinazione PDW è un componente Integration Services che consente di caricare i dati in PDW usando Integration Services pacchetti dtsx. In un flusso di lavoro del pacchetto per SQL ServerPDW è possibile caricare e unire dati da più origini e caricare i dati in più destinazioni. I caricamenti avvengono in parallelo, sia all'interno di un pacchetto sia tra più pacchetti in esecuzione contemporaneamente, fino a un massimo di 10 caricamenti paralleli sullo stesso strumento.  
  
Oltre alle attività descritte in questo argomento, è possibile usare altre funzionalità di Integration Services per filtrare, trasformare, analizzare e pulire i dati prima di caricarli nel data warehouse. È inoltre possibile migliorare il flusso di lavoro del pacchetto eseguendo istruzioni SQL e pacchetti figlio o inviando messaggi di posta elettronica.  
  
Per la documentazione completa di Integration Services, vedere [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="methods-for-running-an-integration-services-package"></a><a name="HowToDeployPackage"></a>Metodi per l'esecuzione di un pacchetto di Integration Services  
Usare uno di questi metodi per eseguire un pacchetto Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Esegui da SQL Server 2008 R2 Business Intelligence Development Studio (offerte)  
Per eseguire il pacchetto dall'interno di offerte, fare clic con il pulsante destro del mouse sul pacchetto e scegliere **Esegui pacchetto**.  
  
Per impostazione predefinita, le offerte eseguono i pacchetti usando i file binari a 64 bit. Questa operazione è determinata dalla proprietà del pacchetto **Run64BitRuntime** . Per impostare questa proprietà, passare a **Esplora soluzioni**, fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà**. Nelle **pagine delle proprietà Integration Services**passare a **proprietà di configurazione** e selezionare **debug**. Viene visualizzata la proprietà **Run64BitRuntime** sotto le **Opzioni di debug**. Per usare i runtime a 32 bit, impostare questa impostazione su **false**. Per usare i runtime a 64 bit, impostare questa impostazione su **true**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Eseguire da SQL Server 2012 SQL Server Data Tools  
Per eseguire il pacchetto dall'interno SQL Server Data Tools, fare clic con il pulsante destro del mouse sul pacchetto e scegliere **Esegui pacchetto**.  
  
### <a name="run-from-powershell"></a>Esegui da PowerShell  
Per eseguire il pacchetto da Windows PowerShell, utilizzando l'utilità **dtexec** : `dtexec /FILE <packagePath>`  
  
Ad esempio: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Esegui da un prompt dei comandi di Windows 
Per eseguire il pacchetto da un prompt dei comandi di Windows, utilizzando l'utilità **dtexec** : `dtexec /FILE <packagePath>`  
  
ad esempio `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="data-types"></a><a name="DataTypes"></a>Tipi di dati  
Quando si utilizza Integration Services per caricare dati da un'origine dati in un database SQL Server PDW, i dati vengono prima mappati dai dati di origine ai tipi di dati di Integration Services. In questo modo è possibile eseguire il mapping dei dati di più origini a un set comune di tipi di dati.  
  
Viene quindi eseguito il mapping dei dati da Integration Services a SQL Server PDW tipi di dati. Per ogni tipo di dati SQL Server PDW, nella tabella seguente sono elencati i tipi di dati Integration Services che possono essere convertiti nel tipo di dati SQL Server PDW.  
  
|Tipo di dati PDW|Integration Services tipi di dati mappati al tipo di dati PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Supporto limitato per la precisione del tipo di dati**  
  
PDW genera un errore di convalida se si esegue il mapping di una colonna di input DT_NUMERIC o DT_DECIMAL contenente un valore con precisione maggiore di 28.  
  
**Tipi di dati non supportati**  
  
SQL Server PDW non supporta i tipi di dati Integration Services seguenti:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Per caricare colonne che contengono dati di questi tipi in SQL Server PDW, è necessario aggiungere una trasformazione Conversione dati a Monte nel flusso di dati per convertire i dati in un tipo di dati compatibile.  
  
## <a name="permissions"></a>Autorizzazioni  
Per eseguire un pacchetto di caricamento Integration Services, è necessario:  
  
-   Autorizzazione LOAD per il database.  
  
-   Autorizzazioni INSERT, UPDATE e DELETE applicabili per la tabella di destinazione.  
  
-   Se viene utilizzato un database di gestione temporanea, creare l'autorizzazione per il database di gestione temporanea. Per la creazione di una tabella temporanea.  
  
-   Se non viene utilizzato alcun database di gestione temporanea, creare l'autorizzazione per il database di destinazione. Per la creazione di una tabella temporanea.  
  
## <a name="general-remarks"></a><a name="GenRemarks"></a>Osservazioni generali  
Quando un pacchetto di Integration Services dispone di più destinazioni SQL Server PDW in esecuzione e una delle connessioni viene terminata, Integration Services interrompe il push dei dati in tutte le destinazioni SQL Server PDW.  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>Limitazioni e restrizioni  
Per un pacchetto di Integration Services, il numero di destinazioni SQL Server PDW per la stessa origine dati è limitato dal numero massimo di caricamenti attivi. Il numero massimo è preconfigurato e non è configurabile dall'utente. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Ogni destinazione del pacchetto Integration Services per la stessa origine dati viene conteggiata come un carico quando il pacchetto è in esecuzione. Si supponga ad esempio che il numero massimo di caricamenti attivi sia 10. Il pacchetto non viene eseguito se tenta di aprire 11 o più destinazioni per la stessa origine dati.  
  
È possibile eseguire contemporaneamente più pacchetti purché ogni pacchetto non utilizzi un numero di caricamenti attivi superiore al limite massimo consentito. Ad esempio, se il numero massimo di caricamenti attivi è 10, è possibile eseguire contemporaneamente due pacchetti che utilizzino entrambi 10 destinazioni. Mentre un pacchetto viene eseguito, l'altro rimane in attesa nella coda di caricamento.  
  
Se il numero di caricamenti in coda supera il numero massimo consentito di caricamenti in coda, il pacchetto non verrà eseguito. Se, ad esempio, il numero massimo di caricamenti è 10 per dispositivo e il numero massimo di caricamenti in coda è pari a 40 per ogni appliance, è possibile eseguire simultaneamente cinque pacchetti Integration Services ognuno dei quali apre 10 destinazioni. L'eventuale tentativo di eseguire un sesto pacchetto avrà esito negativo.  

> [!IMPORTANT]
> L'uso di un'origine dati OLE DB in SSIS con l'adattatore di destinazione PDW può causare il danneggiamento dei dati se la tabella di origine contiene colonne char e varchar con regole di confronto SQL. È consigliabile usare un'origine ADO.NET se la tabella di origine contiene colonne char o varchar con regole di confronto SQL. 

  
## <a name="locking-behavior"></a><a name="Locks"></a>Comportamento di blocco  
Quando si caricano dati con Integration Services, SQL ServerPDW usa i blocchi a livello di riga per aggiornare i dati nella tabella di destinazione. Ciò significa che durante l'aggiornamento ogni riga viene bloccata per la lettura e la scrittura. Le righe della tabella di destinazione non sono bloccate mentre i dati vengono caricati nella tabella di staging.  
  
## <a name="examples"></a><a name="Examples"></a>Esempi  
  
### <a name="a-simple-load-from-flat-file"></a><a name="Walkthrough"></a>A. Caricamento semplice da file flat  
La procedura dettagliata seguente illustra un caricamento semplice dei dati usando Integration Services per caricare i dati dei file flat in un'appliance di SQL Server PDW.  In questo esempio si presuppone che Integration Services sia già stato installato nel computer client e che sia stata installata la destinazione SQL Server PDW, come descritto in precedenza.  
  
In questo esempio verrà caricato nella `Orders` tabella, che include il codice DDL seguente. La `Orders` tabella fa parte del `LoadExampleDB` database.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Ecco i dati di caricamento:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
Per preparare il carico, creare il file flat `exampleLoad.txt` contenente i dati di caricamento:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
Per prima cosa, creare un pacchetto di Integration Services eseguendo questi passaggi:  
  
1.  In SQL Server Data Tools \( SSDT \) selezionare **file**, **nuovo**, quindi **progetto**. Selezionare **Integration Services progetto** dalle opzioni elencate. Assegnare un nome al progetto `ExampleLoad` e fare clic su **OK**.  
  
2.  Fare clic sulla scheda **flusso di controllo** , quindi trascinare l' **attività flusso di dati** dalla **casella degli strumenti** al riquadro **flusso di controllo** .  
  
3.  Fare clic sulla scheda **flusso di dati** e quindi trascinare **origine file Flat** dalla **casella degli strumenti** nel riquadro **flusso di dati** . Fare doppio clic sulla casella appena creata per aprire l' **Editor origine file flat**.  
  
4.  Fare clic su **gestione connessione** , quindi fare clic su **nuovo**.  
  
5.  Nella casella **Nome gestione connessione** immettere un nome descrittivo per la connessione. Per questo esempio, `Example Load Flat File CM` .  
  
6.  Fare clic su **Sfoglia** e selezionare il `ExampleLoad.txt` file dal computer locale.  
  
7.  Poiché il file flat contiene una riga con i nomi di colonna, fare clic sui **nomi delle colonne nella prima** casella della riga di dati.  
  
8.  Fare clic su **colonne** nella colonna a sinistra e visualizzare in anteprima i dati che verranno caricati per assicurarsi che i nomi e i dati delle colonne siano stati interpretati correttamente.  
  
9. Fare clic su **Avanzate** nella colonna a sinistra. Fare clic su ogni nome di colonna per esaminare il tipo di dati associato ai dati. Consente di digitare le modifiche nella casella in modo che i tipi di dati dei dati caricati siano compatibili con i tipi di colonna di destinazione.  
  
10. Fare clic su **OK** per salvare la gestione connessione.  
  
11. Fare clic su **OK** per uscire dall' **Editor origine file flat**.  
  
Specificare la destinazione per il flusso di dati.  
  
1.  Trascinare la **destinazione SQL Server PDW** dalla **casella degli strumenti** nel riquadro **flusso di dati** .  
  
2.  Fare doppio clic sulla casella appena creata per caricare l' **editor di destinazione SQL Server PDW**.  
  
3.  Fare clic sulla freccia verso il basso accanto a **gestione connessione**.  
  
4.  Selezionare **Crea una nuova connessione**.  
  
5.  Immettere le informazioni relative al server, all'utente, alla password e al database di destinazione con informazioni specifiche per il dispositivo. (Di seguito sono riportati alcuni esempi). Fare quindi clic su **OK**.  
  
    Per le connessioni InfiniBand, **nome server**: immettere <nome-dispositivo>-SQLCTL01, 17001.  
  
    Per le connessioni Ethernet, **nome server**: immettere l'indirizzo IP del cluster del nodo di controllo, la virgola, la porta 17001. Ad esempio, 10.192.63.134, 17001.  
  
    **Utente**`user1`  
  
    **Password**`password1`  
  
    **Database di destinazione:**`LoadExampleDB`  
  
6.  Selezionare la tabella di destinazione: `Orders` .  
  
7.  Selezionare **Accoda** come modalità di caricamento e fare clic su **OK**.  
  
Specificare il flusso di dati dall'origine alla destinazione.  
  
1.  Nel riquadro **flusso di dati** trascinare la freccia verde dalla casella **origine file flat** alla casella **destinazione SQL Server PDW** .  
  
2.  Fare doppio clic sulla casella **destinazione SQL Server PDW** per visualizzare di nuovo l' **editor di SQL Server PDW destinazione** . Verranno visualizzati i nomi delle colonne del file flat a sinistra, in colonne di **input senza mapping**. Verranno visualizzati i nomi delle colonne della tabella di destinazione a destra, in **colonne di destinazione senza mapping**. Eseguire il mapping delle colonne trascinando o facendo doppio clic sui nomi delle colonne corrispondenti negli elenchi colonne di **input senza mapping** e colonne di **destinazione non mappate** nella casella **colonne** di cui è stato eseguito il mapping. Fare clic su **OK** per salvare le impostazioni.  
  
3.  Salvare il pacchetto scegliendo **Salva** dal menu **file** .  
  
Eseguire il pacchetto nel computer Integration Services.  
  
1.  Nella Integration Services**Esplora soluzioni** (colonna a destra), fare clic con il pulsante destro del mouse `Package.dtsx` e scegliere **Esegui**.  
  
2.  Il pacchetto verrà eseguito e lo stato di avanzamento e gli eventuali errori verranno visualizzati nel riquadro **stato** . Usare un client SQL per confermare il carico o monitorare il carico tramite la console di amministrazione SQL Server PDW.  
  
## <a name="see-also"></a>Vedere anche  
[Creare un'attività script che usa l'adattatore di destinazione di SSIS PDW](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Progettazione e implementazione di pacchetti (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Esercitazione: Creazione di un pacchetto di base tramite una procedura guidata](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introduzione (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[Esempio di generazione di pacchetti dinamici](https://go.microsoft.com/fwlink/?LinkId=202413)  
[Designing Your SSIS Packages for Parallelism (SQL Server Video)](/previous-versions/sql/sql-server-2008/dd795221(v=sql.100))  
[Esempi di Microsoft SQL Server Community: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[Miglioramento dei caricamenti incrementali tramite Change Data Capture](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Trasformazione Dimensione a modifica lenta](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Attività Inserimento bulk](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->