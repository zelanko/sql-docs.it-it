---
title: Storia dei driver per Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0eb869cf19f128515951421efddc229aa785cdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "72451844"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Storia dei driver per Microsoft SQL Server

In questa pagina vengono descritte le tecnologie di connessione dati storiche di Microsoft per la connessione a SQL Server.

## <a name="odbc"></a>ODBC

Sono disponibili tre generazioni distinte di driver Microsoft ODBC per SQL Server. Il primo driver ODBC "SQL Server" è ancora disponibile come parte di [Windows Data Access Components](#microsoft-or-windows-data-access-components). Non è consigliabile usare questo driver per nuovi progetti di sviluppo. A partire da SQL Server 2005, [SQL Server Native Client](#sql-server-native-client) include un'interfaccia ODBC ed è il driver ODBC disponibile in SQL Server 2005 fino a SQL Server 2012. Non è consigliabile usare questo driver per nuovi progetti di sviluppo. A partire da SQL Server 2012, [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) è il driver che in futuro verrà aggiornato con le funzionalità server più recenti.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client è una libreria autonoma usata sia per OLE DB che per ODBC. SQL Server Native Client (spesso abbreviato SNAC) era incluso in SQL Server a partire dalla versione 2005 fino a SQL Server 2012. SQL Server Native Client può essere usato per le applicazioni che devono sfruttare le nuove funzionalità introdotte in SQL Server 2005 e in uso fino a SQL Server 2012 (Microsoft/Windows Data Access Components non viene aggiornato per queste nuove funzionalità di SQL Server). Per le nuove funzionalità successive a SQL Server 2012, SQL Server Native Client non verrà aggiornato. Passare a Microsoft ODBC Driver for SQL Server o Microsoft OLE DB Driver per SQL Server se si vuole usufruire delle nuove funzionalità di SQL Server in futuro.

Per informazioni dettagliate su SQL Server Native Client, vedere la [documentazione di SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Dopo SQL Server 2012, il driver ODBC primario per SQL Server è stato sviluppato e rilasciato come Microsoft ODBC Driver for SQL Server. Per altre informazioni, vedere la [documentazione di Microsoft ODBC Driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Sono disponibili tre generazioni distinte di provider Microsoft OLE DB per SQL Server. Il primo "provider Microsoft OLE DB per SQL Server" (SQLOLEDB) viene ancora fornito come parte di [Windows Data Access Components](#microsoft-or-windows-data-access-components). Questo provider non verrà aggiornato con nuove funzionalità e non è consigliabile usarlo questo driver per un nuovo sviluppo. A partire da SQL Server 2005, [SQL Server Native Client](#sql-server-native-client) include un'interfaccia del provider OLE DB (SQLNCLI) ed è il provider OLE DB disponibile con SQL Server 2005 fino a SQL Server 2017. È stato [annunciato come deprecato nel 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e non è consigliabile usare questo driver per nuovi sviluppi. Nel 2017 la tecnologia OLE DB per l'accesso ai dati [è stata dichiarata non più deprecata ed è stato annunciato un nuovo rilascio pianificato](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) per il 2018. Il nuovo provider OLE DB viene chiamato "Microsoft OLE DB Driver per SQL Server" (MSOLEDBSQL) ed è attualmente gestito e supportato.

## <a name="adonet"></a>ADO.NET

ADO.NET è stato introdotto con Microsoft .NET Framework e continua a essere sottoposto a processi di manutenzione e ottimizzazione. Si tratta di un componente principale di Microsoft .NET Framework. Per altre informazioni, vedere [Microsoft ADO.NET per SQL Server](ado-net/microsoft-ado-net-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver per SQL Server

Introdotto nel 2000, Microsoft JDBC Driver per SQL Server continua a essere usato e migliorato. Era open source nel 2016. Per informazioni aggiornate, inclusa la procedura di download del driver, vedere [Panoramica del driver JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Driver Microsoft per PHP per SQL Server

Introdotti nel 2009 come progetto open source, i driver Microsoft per PHP per SQL Server continuano a essere gestiti e migliorati. Per informazioni aggiornate, inclusa la procedura di download del driver PHP, vedere [Driver Microsoft per PHP per SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver Microsoft per Node.js per SQL Server

Il driver Microsoft per Node.js per SQL Server consente alle applicazioni Node.js in Microsoft Windows e Microsoft Azure di accedere a Microsoft SQL Server e al database SQL di Microsoft Azure. Le attività di sviluppo non sono più incentrate su questo driver. Non è consigliabile creare nuove applicazioni usando il driver Microsoft per Node.js per SQL Server.

Per altre informazioni sul driver Microsoft per Node.js per SQL Server, vedere [WindowsAzure/node-sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Tedious

Attualmente Microsoft contribuisce a e supporta il modulo open source tedious in Node.js per la connettività ai SQL Server con JavaScript. Per altre informazioni, vedere [Driver Node.js per SQL Server](./node-js/node-js-driver-for-sql-server.md)

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft/Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) è un prodotto accluso a e supportato da Windows per la compatibilità con le versioni precedenti delle applicazioni e non fanno parte dell'attuale stack di tecnologie di SQL Server. Non verranno aggiunte altre funzionalità ai componenti di MDAC/WDAC e non è consigliabile usarli per lo sviluppo di nuove applicazioni.

Ai fini di questo documento, è possibile dividere lo stack MDAC/WDAC nei componenti seguenti, in base alla tecnologia e ai prodotti:

* **ADO** (inclusi ADOMD e ADOX)
* **OLE DB** (inclusi servizi OLE DB core, SQL Server provider OLE DB, provider OLE DB Oracle, provider OLE DB per i driver ODBC, provider di data shaping e provider di dati remoti)
* **ODBC** (inclusi Gestione driver ODBC, SQL ODBC Driver e Oracle ODBC Driver)

### <a name="mdacwdac-components"></a>Componenti MDAC/WDAC

MDAC/WDAC include i seguenti componenti:

* **ODBC:** Microsoft Open Database Connectivity (ODBC) è un'interfaccia del linguaggio di programmazione C che consente alle applicazioni di accedere ai dati da un'ampia gamma di sistemi di gestione di database. Le applicazioni che usano questa API sono limitate all'accesso alle origini dati relazionali.
* **OLE DB:** OLE DB è un set di interfacce COM per l'accesso ai dati in diversi archivi dati. Sono disponibili provider OLE DB per l'accesso ai dati in database, file system, archivi di messaggi, servizi directory, flussi di lavoro e archivi documenti.
* **ADO:** ActiveX Data Objects (ADO) offre un modello di programmazione di alto livello. Sebbene le prestazioni siano leggermente inferiori a quelle della codifica diretta in OLE DB o ODBC, ADO è semplice da apprendere e usare. Può quindi essere usato in linguaggi di script come Microsoft Visual Basic, Scripting Edition(VBScript) o Microsoft JScript.
* **ADOMD:** ADO Multi-Dimensional (ADOMD) è destinato all'uso con i provider di dati multidimensionali, ad esempio il provider Microsoft OLAP, noto anche come provider Microsoft Analysis Services. Non sono stati apportati miglioramenti significativi alle funzionalità rispetto a MDAC 2.0.
* **ADOX:** Le estensioni ADO per DDL e sicurezza (ADOX) consentono di creare e modificare le definizioni di un database, una tabella, un indice o una stored procedure. È possibile usare ADOX con qualsiasi provider. Il provider Microsoft OLE DB Jet offre il supporto completo per ADOX, mentre il provider OLE DB per Microsoft SQL Server offre un supporto limitato.
* **Librerie di rete di Microsoft SQL Server:** Le librerie di rete di SQL Server consentono a SQLOLEDB e SQLODBC di comunicare con il database di SQL Server. Le seguenti librerie di rete di SQL Server sono state deprecate nelle versioni di MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC. TCP/IP e Named Pipes continueranno a essere supportate e sono disponibili nel sistema operativo Windows a 64 bit.
* **MSDASQL:** Il provider Microsoft OLE DB per ODBC (MSDASQL) consente alle applicazioni basate su OLE DB e ADO (che usa OLEDB internamente) di accedere alle origini dati usando un driver ODBC. MSDASQL è un provider OLEDB che si connette a ODBC, anziché a un database. È concepito come un bridge da OLE DB a un driver ODBC quando non esiste un provider OLE DB diretto per un'origine dati. MSDASQL è incluso nel sistema operativo Windows e Windows Server 2008 e Vista SP1 sono state le prime versioni di Windows a includere una versione a 64 bit della tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componenti MDAC/WDAC deprecati

Questi componenti sono ancora supportati nella versione corrente di MDAC/WDAC, ma potrebbero essere rimossi nelle versioni future. Quando si sviluppano nuove applicazioni, Microsoft consiglia di evitare l'uso di questi componenti. Inoltre, quando si aggiornano o si modificano le applicazioni esistenti, rimuovere tutte le dipendenze relative a questi componenti.

* **SQLOLEDB:** Il provider Microsoft OLE DB per SQL Server (SQLOLEDB), che supporta l'accesso a Microsoft SQL Server, è stato deprecato e la relativa connettività alle future versioni di SQL Server può non essere supportata. La possibilità di connettersi a versioni precedenti a SQL Server 7 verrà eliminata dal sistema operativo dopo Windows 7. Le nuove applicazioni devono usare Microsoft OLE DB Driver per SQL Server (MSOLEDBSQL), che supporta nuove funzionalità di SQL Server. È consigliabile eseguire la migrazione delle applicazioni esistenti a Microsoft OLE DB Driver per SQL Server anche per migliorare le prestazioni, l'affidabilità e la facilità di supporto. Per altre informazioni, vedere [Aggiornamento di un'applicazione a OLE DB Driver per SQL Server da MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** Il driver ODBC Microsoft SQL Server (SQLOLEDB), che supporta l'accesso a Microsoft SQL Server, è stato deprecato e la relativa connettività alle future versioni di SQL Server può non essere supportata. La possibilità di connettersi a versioni precedenti a SQL Server 7 verrà eliminata dal sistema operativo dopo Windows 7. Le nuove applicazioni devono usare Microsoft ODBC Driver for SQL Server per Windows, che supporta nuove funzionalità di SQL Server. È consigliabile eseguire la migrazione delle applicazioni esistenti a Microsoft ODBC Driver for SQL Server anche per migliorare le prestazioni, l'affidabilità e la facilità di supporto. Per le informazioni pertinenti, vedere [Aggiornamento di un'applicazione da MDAC a SQL Server Native Client](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Motore di database Microsoft Jet 4.0:** A partire dalla versione 2.6 MDAC non contiene più componenti Jet. In altre parole, MDAC 2.6, 2.7 e 2.8 non contengono Microsoft Jet, il provider OLE DB Microsoft Jet, i driver del database desktop ODBC o gli oggetti DAO Jet. 

  Non esiste una versione a 64 bit del motore di database Jet, del driver OLEDB Jet, dei driver ODBC Jet e non è disponibile alcun oggetto DAO Jet. Per altre informazioni, vedere l'[articolo della Knowledge Base 957570](https://support.microsoft.com/kb/957570). Nelle versioni a 64 bit di Windows Jet a 32 bit viene eseguito nel sottosistema WOW64 di Windows. Per altre informazioni su WOW64, vedere la [documentazione di WOW64 in MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Le applicazioni native a 64 bit non possono comunicare con i driver Jet a 32 bit eseguiti in WOW64.

  Anziché Microsoft Jet, Microsoft consiglia di usare [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) per sviluppare nuove applicazioni non Microsoft Access che richiedono un archivio dati relazionale. Queste applicazioni Jet nuove o convertite possono continuare a usare Jet per l'uso di Microsoft Office 2003 e dei file più datati (MDB e XLS) per l'archiviazione di dati non primari. Tuttavia, per queste applicazioni è consigliabile pianificare la migrazione da Jet al motore di database di Microsoft Access. È possibile [scaricare il motore di database di Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), che consente di leggere e scrivere file pre-esistenti nei formati di Office 2003 (file con estensione mdb e xls) o di Office 2007 (con estensione accdb, xlsm, xlsx e xlsb).

  > [!IMPORTANT]
  > Leggere il contratto di licenza con l'utente finale di Office System 2007 per le limitazioni specifiche riguardo all'uso.

  > [!NOTE]
  > Le applicazioni SQL Server possono accedere ai file di Office System 2007 e versioni precedenti anche usando le funzionalità della connettività dei dati eterogenei e di Integrations Services in SQL Server con il driver di Office System 2007. Inoltre, le applicazioni SQL Server a 64 bit possono accedere ai file di Jet e Office System 2007 a 32 bit usando SQL Server Integration Services (SSIS) a 32 bit in Windows a 64 bit.

* **MSDADS:** Con il provider Microsoft OLE DB per data shaping (MSDADS), è possibile creare relazioni gerarchiche tra chiavi, campi o set di righe in un'applicazione. Non sono stati apportati miglioramenti significativi alle funzionalità dopo MDAC 2.1. Questo provider è stato deprecato. Microsoft consiglia di usare XML anziché MSDADS.
* **Oracle ODBC e Oracle OLE DB:** Microsoft Oracle ODBC Driver (Oracle ODBC) e il provider Microsoft OLE DB per Oracle (Oracle OLE DB) offrono l'accesso ai server di database Oracle. Vengono compilati usando Oracle Call Interface (OCI) versione 7 e offrono il supporto completo per Oracle 7. Inoltre, viene usata l'emulazione di Oracle 7 per offrire un supporto limitato per i database Oracle 8. Oracle non supporta più le applicazioni che utilizzano le chiamate OCI versione 7. Queste tecnologie sono deprecate. Se si usano origini dati Oracle, è necessario eseguire la migrazione al driver e al provider resi disponibili da Oracle.
* **RDS:** Servizi Desktop remoto (RDS) è un meccanismo proprietario di Microsoft per l'accesso a oggetti Recordset ADO remoti in Internet o Intranet. RDS è deprecato. Non sono stati apportati miglioramenti significativi alle funzionalità di RDS dopo MDAC 2.1. Microsoft ha rilasciato .NET Framework, che offre funzionalità SOAP complete e sostituisce i componenti RDS. Tutti i componenti server RDS verranno rimossi dal sistema operativo dopo Windows 7.
* **JRO:** Gli oggetti di replica Jet (JRO) sono deprecati. La libreria JRO viene usata all'interno di ADO con database Jet ( *.mdb) per creare e comprimere i database Jet (file MDB) ed eseguire la gestione della replica Jet. MDAC 2.7 sarà l'ultima versione. JRO non sarà disponibile nel sistema operativo Windows a 64 bit. Non è supportata nel formato di file Microsoft Access 2007 (* .accdb).
* **Supporto ODBC a 16 bit:** Se si usano applicazioni a 16 bit, è necessario eseguire la migrazione a un'applicazione a 32 bit. La funzionalità a 16 bit è deprecata ed è in corso la sua rimozione dai sistemi operativi a 64 bit. Per altre informazioni, vedere l'[articolo 896458 della Knowledge Base](https://support.microsoft.com/kb/896458).
* **Provider OLE DB semplice (MSDAOSP):** Il provider OLE DB semplice offre un framework per la creazione rapida di provider OLE DB usando dati semplici. MSDAOSP è deprecato.
* **Libreria di cursori ODBC:** La libreria di cursori ODBC (ODBCCR32.dll) offre cursori dati limitati sul lato client. La libreria di cursori ODBC è stata deprecata. L'applicazione può usare le implementazioni del cursore sul lato server come sostituzione.
* **Comunicazione remota out-of-process dell'interfaccia OLE DB:** La comunicazione remota dell'interfaccia OLEDB (msdaps.dll) è un tentativo di consentire l'esecuzione out-of-process ai provider OLE DB. La comunicazione remota out-of-process dell'interfaccia OLE DB è deprecata.
* **Librerie di rete SQL AppleTalk e Banyan Vines:** Le librerie di rete SQL Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC sono deprecate. Se si usa una di queste tecnologie, è necessario modificare le applicazioni in modo che usino una delle altre librerie di rete, ad esempio TCP/IP e Named Pipe.

### <a name="mdacwdac-releases"></a>Versioni di MDAC/WDAC

Di seguito è riportato un elenco degli scenari di supportabilità delle versioni precedenti di MDAC/WDAC, a partire dalla meno recente.

* **MDAC 1.5, MDAC 2.0 e MDAC 2.1:** Queste versioni di MDAC erano versioni indipendenti rilasciate attraverso Microsoft Windows NT Option Pack, l'SDK della piattaforma Microsoft Windows o il sito Web MDAC. Queste versioni di MDAC non sono più supportate.
* **MDAC 2.5:** Questa versione di MDAC era inclusa nel sistema operativo Windows 2000. I Service Pack di MDAC 2.5 erano inclusi nei Service Pack di Windows 2000 corrispondenti.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 e SP2 erano inclusi rispettivamente in Microsoft SQL Server 2000 RTM, SP1 e SP2. Inoltre, questi Service Pack di MDAC sono stati rilasciati nel sito Web MDAC in conformità alla pianificazione dei rilasci dei Service Pack di Microsoft SQL Server 2000. È possibile installare questa versione di MDAC e i relativi Service Pack sulle piattaforme Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Questa versione di MDAC non è più supportata.
* **MDAC 2.7:** Questa versione di MDAC era inclusa nei sistemi operativi Microsoft Windows XP RTM e SP1. È possibile installare questa versione di MDAC e i relativi Service Pack sulle piattaforme Windows 2000, Windows Millennium, Windows NT e Windows 98. È possibile installare questa versione sulla piattaforma Windows XP solo usando il sistema operativo o i relativi Service Pack. Questa versione di MDAC non è più supportata.
* **MDAC 2.8:** Questa versione di MDAC era inclusa in Windows Server 2003 e Windows XP SP2 e versioni successive. È possibile installare questa versione di MDAC e i relativi Service Pack anche in Windows 2000.

  * Anche la versione a 32 bit di MDAC 2.8 è stata rilasciata sul sito Web MDAC nello stesso momento in cui Windows Server 2003 è stato rilasciato ai clienti.
  * La versione a 64 bit di MDAC 2.8 è stata rilasciata con la versione a 64 bit di Windows Server 2003 e Windows XP.

* **Windows Data Access Components (WDAC):** Il nome MDAC è stato modificato in WDAC (Windows Data Access Components) a partire da Windows Vista e Windows Server 2008. WDAC è incluso come parte del sistema operativo e non è disponibile separatamente per la ridistribuzione. La manutenzione di WDAC è soggetta al ciclo di vita del sistema operativo.

  Le versioni a 32 bit e 64 bit di WDAC vengono rilasciate rispettivamente con le versioni a 32 bit e a 64 bit dei sistemi operativi Windows.

## <a name="obsolete-data-access-technologies"></a>Tecnologie di accesso ai dati obsolete

Si definiscono obsolete le tecnologie che non sono state migliorate o aggiornate in diverse versioni del prodotto e che verranno escluse dalle versioni future del prodotto. Non usare queste tecnologie quando si scrivono nuove applicazioni. Quando si modificano le applicazioni esistenti scritte usando queste tecnologie, è consigliabile eseguire la migrazione di tali applicazioni a ADO.NET o a un'altra tecnologia più aggiornata.

Sono considerati obsoleti i componenti seguenti:

* **DB-Library:** DB-Library è un modello di programmazione specifico di SQL Server che include le API C. Non sono stati apportati miglioramenti alle funzionalità per DB-Library a partire da SQL Server 6.5. La versione finale era quella inclusa in SQL Server 2000 e non verrà trasferita al sistema operativo Windows a 64 bit.
* **Embedded SQL (E-SQL):** E-SQL è un modello di programmazione specifico per SQL Server che consente di incorporare le istruzioni Transact-SQL nel codice Visual C. Non sono stati apportati miglioramenti alle funzionalità per E-SQL a partire da SQL Server 6.5. La versione finale era quella inclusa in SQL Server 2000 e non verrà trasferita al sistema operativo Windows a 64 bit.
* **Data Access Objects (DAO):** DAO consente di accedere ai database JET (Access). Questa API può essere usata da Microsoft Visual Basic, Microsoft Visual C++ e linguaggi di script. Era inclusa in Microsoft Office 2000 e Office XP. DAO 3.6 è la versione finale di questa tecnologia. Non sarà disponibile nel sistema operativo Windows a 64 bit.
* **Remote Data Objects (RDO):** RDO è stata progettata specificamente per accedere a origini dati relazionali ODBC remote e semplifica l'uso di ODBC senza complessi codici dell'applicazione. Era inclusa in Microsoft Visual Basic versioni 4, 5 e 6. RDO 2.0 è stata la versione finale di questa tecnologia.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
