---
title: Filegroup e file di database | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 782536e79336c0224638707538e8a12a31f5af84
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287985"
---
# <a name="database-files-and-filegroups"></a>Filegroup e file di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ogni database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene almeno due file del sistema operativo: un file di dati e un file di log. I file di dati contengono dati e oggetti come tabelle, indici, stored procedure e viste. I file di log contengono le informazioni necessarie per il recupero di tutte le transazioni del database. I file di dati possono essere raggruppati in filegroup ai fini dell'allocazione e dell'amministrazione.  
  
## <a name="database-files"></a>File di database  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database contengono tre tipi di file, come illustrato nella tabella seguente.  
  
|File|Descrizione|  
|----------|-----------------|  
|Primaria|Il file di dati primario contiene le informazioni di avvio del database e punta agli altri file del database. I dati e gli oggetti degli utenti possono essere archiviati in questo file o nei file di dati secondari. In ogni database è disponibile un unico file di dati primario. L'estensione consigliata per i file di dati primari è mdf.|  
|Secondari|I file di dati secondari sono facoltativi e definiti dall'utente e vengono utilizzati per archiviare i dati dell'utente. Possono essere utilizzati per suddividere i dati su più dischi, memorizzandoli in unità disco distinte. Se un database supera le dimensioni massime consentite per un singolo file di Windows, è inoltre possibile utilizzare i file di dati secondari per consentire l'aumento di dimensioni del database.<br /><br /> L'estensione consigliata per i file di dati secondari è ndf.|  
|Log delle transazioni|I file di log delle transazioni contengono le informazioni necessarie per il recupero del database. È necessario che sia disponibile almeno un file di log per ogni database. L'estensione consigliata per i file di log è ldf.|  
  
 Ad esempio, è possibile creare un database semplice, denominato **Sales** , con un file primario che include tutti i dati e gli oggetti e un file di log che include le informazioni del log delle transazioni. In alternativa, è possibile creare un database più complesso, denominato **Orders** , con un file primario e cinque file secondari. I dati e gli oggetti all'interno del database vengono suddivisi nei sei file e i quattro file di log includono le informazioni del log delle transazioni.  
  
 Per impostazione predefinita, i dati e i log delle transazioni vengono archiviati nella stessa unità e nello stesso percorso. Ciò consente la gestione nei sistemi a disco singolo, ma può non essere la soluzione ottimale per gli ambienti di produzione. È consigliabile archiviare i dati e i file di log in dischi separati.  

### <a name="logical-and-physical-file-names"></a>Nomi di file logici e fisici
I file [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hanno due tipi di nome file: 

**logical_file_name:**  logical_file_name è il nome del file fisico in tutte le istruzioni Transact-SQL. Il nome di file logico deve essere conforme alle regole per gli identificatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve essere univoco tra i nomi di file logici nel database. Viene impostato dall'argomento `NAME` in `ALTER DATABASE`. Per altre informazioni, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

**os_file_name:** os_file_name è il nome del file fisico che include il percorso di directory. Tale nome deve essere conforme alle regole relative ai nomi di file del sistema operativo. Viene impostato dall'argomento `FILENAME` in `ALTER DATABASE`. Per altre informazioni, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

> [!IMPORTANT]
> I dati e i file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere memorizzati sia in file system FAT che NTFS. Nei sistemi Windows è consigliabile utilizzare il file system NTFS per i vantaggi di sicurezza intrinseci di NTFS. 

> [!WARNING]
> I file di log e i filegroup di dati di lettura/scrittura non sono supportati in un file system compresso NTFS. Solo i database e i filegroup secondari di sola lettura possono essere memorizzati in un file system compresso NTFS.
> Per un risparmio di spazio, è consigliabile utilizzare la [compressione dei dati](../../relational-databases/data-compression/data-compression.md) anziché la compressione del file system.

Se nello stesso computer sono in esecuzione più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a ogni istanza viene assegnata una directory predefinita specifica in cui verranno archiviati i file dei database creati nell'istanza. Per altre informazioni, vedere [Percorsi dei file per le istanze predefinite e denominate di SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).

### <a name="data-file-pages"></a>Pagine di file di dati
Le pagine dei file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono numerate progressivamente a partire dalla prima, che corrisponde al numero zero (0). A ogni file di un database è associato un numero di ID file univoco. Per identificare in modo univoco una pagina in un database, sono necessari sia ID file che numero di pagina. Nell'esempio seguente vengono illustrati i numeri di pagina di un database che include un file di dati primario di 4 MB e un file di dati secondario di 1 MB.

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

La prima pagina di ogni file è la pagina dell'intestazione, che include informazioni sugli attributi del file. Anche molte altre pagine all'inizio del file contengono informazioni di sistema, ad esempio mappe delle allocazioni. Una delle pagine di sistema archiviate sia nel file di dati primario che nel primo file di log è una pagina di avvio del database contenente informazioni sugli attributi del database. Per altre informazioni su pagine e tipi di pagina, vedere [Guida all'architettura di pagine ed extent](../..//relational-databases/pages-and-extents-architecture-guide.md).

### <a name="file-size"></a>Dimensioni file
Le dimensioni dei file di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono aumentare automaticamente rispetto ai valori originari. Quando si definisce un file, è possibile specificare un incremento di crescita specifico. Quando lo spazio assegnato al file si esaurisce, le sue dimensioni aumentano in base all'incremento specificato. Se un filegroup include più file, le loro dimensioni non aumentano automaticamente finché lo spazio di tutti i file non si esaurisce. L'aumento delle dimensioni avviene quindi in base a un meccanismo round robin utilizzando il [riempimento proporzionale](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill).

È inoltre possibile specificare le dimensioni massime di ogni file. Se non vengono specificate le dimensioni massime, il file può continuare ad aumentare fino a occupare tutto lo spazio disponibile nel disco. Questa caratteristica è particolarmente utile quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzato come database incorporato in un'applicazione per cui l'utente non può rivolgersi direttamente all'amministratore di sistema. L'utente può lasciare aumentare i file in base alle necessità per alleggerire il carico amministrativo derivante dal monitoraggio dello spazio libero nel database e dall'allocazione manuale di spazio aggiuntivo.  

Se [l'inizializzazione dei file immediata](../../relational-databases/databases/database-instant-file-initialization.md) è abilitata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], durante l'allocazione di spazio aggiuntivo per i file di dati l'overhead è minimo.

Per altre informazioni sulla gestione del file di log delle transazioni, vedere [Gestione delle dimensioni del file di log delle transazioni](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations).   

## <a name="database-snapshot-files"></a>File di snapshot di database
La forma del file utilizzato da uno snapshot del database per archiviare i propri dati copy-on-write cambia a seconda che lo snapshot venga creato da un utente o utilizzato internamente:

* Quando lo snapshot del database viene creato da un utente, i dati vengono archiviati in uno o più file sparse. La tecnologia file sparse è una caratteristica del file system NTFS. Inizialmente un file sparse non contiene alcun dato utente e lo spazio su disco per i dati utente non viene allocato per tale file. Per informazioni generali sull'uso di file sparse negli snapshot del database e sul modo in cui aumentano le dimensioni degli snapshot del database, vedere [Visualizzare le dimensioni del file sparse di uno snapshot del database](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md). 
* Gli snapshot del database vengono utilizzati internamente da alcuni comandi DBCC, tra cui DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC e DBCC CHECKFILEGROUP. Uno snapshot interno del database utilizza flussi di dati alternativi sparse dei file originali del database. Come i file sparse, anche i flussi di dati alternativi rappresentano una caratteristica del file system NTFS. L'utilizzo dei flussi di dati alternativi sparse consente l'associazione di più allocazioni di dati a un solo file o a una sola cartella senza incidere sulla dimensione del file o sulle statistiche del volume. 
  
## <a name="filegroups"></a>Filegroup  
 Ogni database contiene un filegroup primario, che include il file di dati primario e gli eventuali file secondari non inclusi in altri filegroup. È possibile creare filegroup definiti dall'utente per raggruppare i file di dati a fini amministrativi e di allocazione e posizione dei dati.  
  
 Ad esempio, è possibile creare tre file, `Data1.ndf`, `Data2.ndf` e `Data3.ndf`, rispettivamente su tre unità disco e assegnarli al filegroup `fgroup1`. È quindi possibile creare una tabella specifica nel filegroup `fgroup1`. Le query sui dati della tabella verranno suddivise sui tre dischi con il conseguente miglioramento delle prestazioni. È possibile ottenere lo stesso risultato in termini di prestazioni utilizzando un singolo file creato su un set di striping RAID. File e filegroup, tuttavia, consentono di aggiungere nuovi file su nuovi dischi in modo semplice.  
  
 Tutti i file di dati vengono archiviati nei filegroup elencati nella tabella seguente.  
  
|Filegroup|Descrizione|  
|---------------|-----------------|  
|Primaria|Il filegroup che contiene il file primario. Tutte le tabelle di sistema vengono allocate al filegroup primario.|  
|Dati ottimizzati per la memoria|Un filegroup ottimizzato per la memoria è basato sul filegroup FileStream|  
|Filestream||    
|Route definite dall'utente|Qualsiasi filegroup creato specificamente dall'utente in fase di creazione o di successiva modifica del database.|  
  
### <a name="default-primary-filegroup"></a>Filegroup predefinito (PRIMARY)  
 Gli oggetti di database creati senza specificare un filegroup di appartenenza vengono assegnati al filegroup predefinito. Viene designato sempre e solo un filegroup predefinito. I file nel filegroup predefinito devono essere di dimensioni sufficienti a contenere tutti i nuovi oggetti non allocati ad altri filegroup.  
  
 A meno che non venga modificato tramite l'istruzione ALTER DATABASE, PRIMARY è il filegroup predefinito. Gli oggetti e le tabelle di sistema, tuttavia, restano allocati all'interno del filegroup PRIMARY e non all'interno del nuovo filegroup predefinito.  
 
### <a name="memory-optimized-data-filegroup"></a>Filegroup di dati ottimizzati per la memoria

Per altre informazioni sui filegroup ottimizzati per la memoria, vedere [Filegroup ottimizzato per la memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).

### <a name="filestream-filegroup"></a>Filegroup FileStream

Per altre informazioni sui filegroup FileStream, vedere [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md#filestream-storage) e [Creare un database abilitato per FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).

### <a name="file-and-filegroup-example"></a>Esempio di file e filegroup
 Nell'esempio seguente viene illustrata la creazione di un database in un'istanza di SQL Server. Nel database sono presenti un file di dati primario, un filegroup definito dall'utente e un file di log. Il file di dati primario è incluso nel filegroup primario e il filegroup definito dall'utente include due file di dati secondari. Tramite l'istruzione ALTER DATABASE viene impostato come predefinito il filegroup definito dall'utente e quindi viene creata una tabella che specifica tale filegroup. Questo esempio usa un percorso generico `c:\Program Files\Microsoft SQL Server\MSSQL.1` per evitare di specificare una versione di SQL Server.

```sql
USE master;
GO
-- Create the database with the default data
-- filegroup, filstream filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM
  ( NAME = 'MyDB_FG_FS',
    FILENAME = 'c:\Data\filestream1')
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO

-- Create a table in the filestream filegroup
CREATE TABLE MyFSTable
(
    cola int PRIMARY KEY,
  colb VARBINARY(MAX) FILESTREAM NULL
)
GO
```

La figura seguente riepiloga i risultati dell'esempio precedente (esclusi i dati FileStream).

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)

## <a name="file-and-filegroup-fill-strategy"></a>Strategia di riempimento dei file e dei filegroup
I filegroup utilizzano una strategia di riempimento proporzionale per tutti i file presenti in ogni filegroup. Quando i dati vengono scritti nel filegroup, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] scrive una quantità di dati proporzionale allo spazio disponibile in ogni file del filegroup anziché scrivere tutti i dati nel primo file fino all'esaurimento dello spazio e quindi passa al file successivo. Ad esempio, se nel file f1 sono disponibili 100 megabyte (MB) e nel file f2 sono disponibili 200 MB, un extent verrà allocato dal file f1, due extent dal file f2 e così via. In questo modo, entrambi i file vengono riempiti quasi simultaneamente e si ottiene uno striping semplice.

Non appena si esaurisce lo spazio di tutti i file di un filegroup, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] espande automaticamente i file uno alla volta in in base a un meccanismo round robin per consentire l'inserimento di ulteriori dati, a condizione che sia stato impostato l'aumento di dimensioni automatico del database. Si supponga, ad esempio, che un filegroup includa tre file per i quali è stato impostato l'aumento di dimensioni automatico. Quando lo spazio viene esaurito in tutti i file del filegroup, viene espanso solo il primo file. Quando il primo file è pieno e non è possibile scrivere altri dati nel filegroup, viene espanso il secondo file. Quando il secondo file è pieno e non è possibile scrivere altri dati nel filegroup, viene espanso il terzo file. Quando il terzo file è pieno e non è possibile scrivere altri dati nel filegroup, viene espanso nuovamente il primo file e così via.

## <a name="rules-for-designing-files-and-filegroups"></a>Regole per la progettazione di file e filegroup
Per i file e i filegroup sono valide le regole seguenti:
- Un file o un filegroup non può essere utilizzato da più database. Ad esempio, i file sales.mdf e sales.ndf, che includono dati e oggetti del database sales, non possono essere usati da altri database.
- Un file può essere membro di un solo filegroup.
- I file di log delle transazioni non fanno mai parte di un filegroup.

## <a name="recommendations"></a><a name="Recommendations"></a> Raccomandazioni
Vengono riportate di seguito alcune indicazioni di carattere generale relative all'utilizzo di file e filegroup: 
- La maggior parte dei database funziona in modo ottimale con un singolo file di dati e un unico file di log delle transazioni.
- Se si utilizzano più file di dati, creare un secondo filegroup per i file aggiuntivi e impostarlo come filegroup predefinito. In questo modo, il file primario conterrà unicamente le tabelle e gli oggetti di sistema.
- Per ottimizzare le prestazioni, creare i file o i filegroup sul numero maggiore possibile di dischi disponibili. Posizionare in filegroup diversi gli oggetti che creano conflitti di spazio.
- Utilizzare i filegroup per la posizione di oggetti su dischi fisici specifici.
- Posizionare in filegroup diversi le diverse tabelle utilizzate nelle stesse query di join. Questa operazione consente di ottimizzare le prestazioni, grazie al fatto che i dati uniti in join vengono cercati con operazioni di I/O su disco in parallelo.
- Posizionare in filegroup diversi le tabelle utilizzate molto frequentemente e gli indici non cluster che appartengono a queste tabelle. Questa operazione consente di ottimizzare le prestazioni, grazie al fatto che vengono eseguite operazioni di I/O in parallelo se i file si trovano su dischi fisici diversi.
- Non posizionare il file o i file di log delle transazioni sullo stesso disco fisico in cui si trovano gli altri file o filegroup.

Per altre informazioni sulle raccomandazioni relative alla gestione del file di log delle transazioni, vedere [Gestione delle dimensioni del file di log delle transazioni](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md#Recommendations).   

## <a name="related-content"></a>Contenuto correlato  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)    
 [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)      
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
 [Architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)    
 [Guida sull'architettura di pagina ed extent](../../relational-databases/pages-and-extents-architecture-guide.md)    
 [Gestione delle dimensioni del file di log delle transazioni](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)     
