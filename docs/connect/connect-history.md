---
title: Cronologia driver per Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05936a9555cacfc88c9219e19bc57772109ed047
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957517"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Cronologia driver per Microsoft SQL Server

In questa pagina vengono descritte le tecnologie di connessione dati storiche di Microsoft per la connessione a SQL Server.

## <a name="odbc"></a>ODBC

Sono disponibili tre generazioni distinte di driver Microsoft ODBC per SQL Server. Il primo driver ODBC "SQL Server" viene comunque incluso nei [componenti di accesso ai dati di Windows](#microsoft-or-windows-data-access-components). Non è consigliabile usare questo driver per la nuova attività di sviluppo. A partire da SQL Server 2005, il [SQL Server Native Client](#sql-server-native-client) include un'interfaccia ODBC ed è il driver ODBC fornito con SQL Server da 2005 a SQL Server 2012. Non è consigliabile usare questo driver per la nuova attività di sviluppo. Dopo la SQL Server 2012, il [Microsoft ODBC driver for SQL Server](#microsoft-odbc-driver-for-sql-server) è il driver aggiornato con le funzionalità server più recenti in futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client è una libreria autonoma utilizzata sia per OLE DB sia per ODBC. SQL Server Native Client (spesso abbreviato SNAC) è stato incluso SQL Server da 2005 a 2012. SQL Server Native Client può essere usato per le applicazioni che devono sfruttare le nuove funzionalità introdotte in SQL Server 2005 tramite SQL Server 2012. I componenti di accesso ai dati di Microsoft/Windows non vengono aggiornati per queste nuove funzionalità in SQL Server. Per le nuove funzionalità oltre SQL Server 2012, SQL Server Native Client non verranno aggiornate. Passare al Microsoft ODBC Driver for SQL Server o al driver Microsoft OLE DB per SQL Server se si desidera sfruttare le nuove funzionalità di SQL Server in futuro.

Per la documentazione completa del SQL Server Native Client, vedere la [documentazione di SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Dopo la SQL Server 2012, il driver ODBC primario per SQL Server è stato sviluppato e rilasciato come Microsoft ODBC Driver for SQL Server. Per ulteriori informazioni, vedere la [documentazione Microsoft ODBC driver for SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Sono disponibili tre generazioni distinte di provider Microsoft OLE DB per SQL Server. Il primo "provider Microsoft OLE DB per SQL Server" (SQLOLEDB) viene ancora fornito come parte di [Windows Data Access Components](#microsoft-or-windows-data-access-components). Questo provider non verrà aggiornato con nuove funzionalità e non è consigliabile utilizzare questo driver per un nuovo sviluppo. A partire da SQL Server 2005, il [SQL Server Native Client](#sql-server-native-client) include un'interfaccia del provider di OLE DB (SQLNCLI) ed è il provider OLE DB fornito con SQL Server 2005 a SQL Server 2017. È stato [annunciato come deprecato nel 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e non è consigliabile usare questo driver per nuovi sviluppi. In 2017 OLE DB tecnologia di accesso ai dati non è stata [deprecata ed è stata annunciata una nuova versione pianificata](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) per 2018. Il nuovo provider di OLE DB è denominato "Microsoft OLE DB driver for SQL Server" (MSOLEDBSQL) ed è attualmente gestito e supportato.

## <a name="adonet"></a>ADO.NET

ADO.NET è stato introdotto con il Framework Microsoft .NET e continua a essere migliorato e mantenuto. Si tratta di un componente principale del Framework Microsoft .NET. Per ulteriori informazioni, vedere [Microsoft ADO.NET per SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver per SQL Server

Introdotta in 2000, Microsoft JDBC Driver for SQL Server continua a essere migliorato e mantenuto. Era open source in 2016. Per le informazioni più aggiornate, incluso il download del driver, vedere [Panoramica del driver JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Driver Microsoft per PHP per SQL Server

Introdotta in 2009 come progetto open source, i driver Microsoft per PHP per SQL Server continuano a essere migliorati e gestiti. Per le informazioni più aggiornate, incluso il download del driver PHP, vedere [driver Microsoft per php per SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver Microsoft per node. js per SQL Server

Il driver Microsoft per node. js per SQL Server consente alle applicazioni node. js in Microsoft Windows e Microsoft Windows Azure di accedere Microsoft SQL Server e il database SQL di Microsoft Azure. Le attività di sviluppo non sono più incentrate su questo driver. Non è consigliabile creare nuove applicazioni usando il driver Microsoft per node. js per SQL Server.

Per ulteriori informazioni sul driver Microsoft per node. js per SQL Server, vedere [WindowsAzure/node-SqlServer](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Noioso

Attualmente Microsoft contribuisce a e supporta il modulo Open Source noioso in node. js per la connettività ai SQL Server tramite JavaScript. Per altre informazioni, vedere [driver node. js per SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft o Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) vengono forniti con e supportati da Windows per la compatibilità con le versioni precedenti e non fanno parte dello stack di tecnologie SQL Server corrente. Non verranno aggiunte nuove funzionalità ai componenti in MDAC/WDAC e non è consigliabile usarle per lo sviluppo di nuove applicazioni.

Ai fini di questo documento, è possibile dividere lo stack MDAC/WDAC nei componenti seguenti, in base alla tecnologia e ai prodotti:

* **ADO** (inclusi ADOMD e ADOX)
* **OLE DB** (inclusi OLE DB servizi di base, provider di OLE DB SQL Server, provider di OLE DB Oracle, provider OLE DB per driver ODBC, provider di forme dati e provider di dati remoto)
* **ODBC** (inclusi gestione driver ODBC, driver ODBC SQL e driver ODBC Oracle)

### <a name="mdacwdac-components"></a>Componenti MDAC/WDAC

MDAC/WDAC include i componenti seguenti:

* **ODBC:** L'interfaccia Microsoft Open Database Connectivity (ODBC) è un'interfaccia del linguaggio di programmazione C che consente alle applicazioni di accedere ai dati da un'ampia gamma di sistemi di gestione di database (DBMS). Le applicazioni che utilizzano questa API sono limitate all'accesso solo alle origini dati relazionali.
* **OLE DB:** OLE DB è un set di interfacce COM per l'accesso ai dati in un'ampia gamma di archivi dati. Sono disponibili provider OLE DB per l'accesso ai dati in database, file System, archivi di messaggi, servizi directory, flussi di lavoro e archivi documenti.
* **ADO:** ActiveX Data Objects (ADO) fornisce un modello di programmazione di alto livello. Sebbene un po' meno efficiente rispetto alla codifica per OLE DB o ODBC direttamente, ADO è semplice da apprendere e usare. Può essere utilizzato da linguaggi di script, ad esempio Microsoft Visual Basic Scripting Edition (VBScript) o Microsoft JScript.
* **ADOMD:** ADO Multidimensional (ADOMD) deve essere utilizzato con i provider di dati multidimensionali, ad esempio il provider Microsoft OLAP, noto anche come provider Microsoft Analysis Services. Non sono stati apportati miglioramenti alle funzionalità principali rispetto a MDAC 2,0.
* **ADOX:** Le estensioni ADO per DDL e Security (ADOX) consentono di creare e modificare le definizioni di un database, una tabella, un indice o un stored procedure. È possibile usare ADOX con qualsiasi provider. Il provider di OLE DB Microsoft Jet fornisce supporto completo per ADOX, mentre il provider di OLE DB Microsoft SQL Server fornisce supporto limitato.
* **Microsoft SQL Server librerie di rete:** Le librerie di rete SQL Server consentono a SQLOLEDB e SQLODBC di comunicare con il database di SQL Server. Le seguenti SQL Server librerie di rete sono state deprecate nelle versioni MDAC/WDAC: Banyan VINES, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC. TCP/IP e named pipe continueranno a essere supportati e saranno disponibili nel sistema operativo Windows a 64 bit.
* **MSDASQL:** Microsoft OLE DB provider per ODBC (MSDASQL) consente alle applicazioni basate su OLE DB e ADO (che utilizza OLEDB internamente) di accedere alle origini dati tramite un driver ODBC. MSDASQL è un provider OLEDB che si connette a ODBC, anziché a un database. È concepita come un Bridge da OLE DB a un driver ODBC quando non esiste alcun provider di OLE DB diretto per un'origine dati. MSDASQL viene fornito con il sistema operativo Windows e Windows Server 2008 e Vista SP1 sono stati le prime versioni di Windows per includere una versione a 64 bit della tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componenti di MDAC/WDAC deprecati

Questi componenti sono ancora supportati nella versione corrente di MDAC/WDAC, ma potrebbero essere rimossi nelle versioni future. Quando si sviluppano nuove applicazioni, Microsoft consiglia di evitare di utilizzare questi componenti. Inoltre, quando si aggiornano o si modificano applicazioni esistenti, rimuovere tutte le dipendenze da tali componenti.

* **SQLOLEDB:** Il Provider Microsoft OLE DB per SQL Server (SQLOLEDB), che supporta l'accesso a Microsoft SQL Server, è stato deprecato. La connettività alle versioni future di SQL Server potrebbe non essere supportata. La possibilità di connettersi alle versioni precedenti a SQL Server 7 verrà rimossa dal sistema operativo dopo Windows 7. Le nuove applicazioni devono usare il driver Microsoft OLE DB per SQL Server (MSOLEDBSQL), che supporta nuove funzionalità di SQL Server. È consigliabile eseguire la migrazione delle applicazioni esistenti al driver Microsoft OLE DB per SQL Server, nonché per migliorare le prestazioni, l'affidabilità e il supporto. Per ulteriori informazioni, vedere [aggiornamento di un'applicazione al Driver OLE DB per SQL Server da MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** Il driver ODBC di Microsoft SQL Server (SQLODBC), che supporta l'accesso a Microsoft SQL Server, è stato deprecato. La connettività alle versioni future di SQL Server potrebbe non essere supportata. La possibilità di connettersi alle versioni precedenti a SQL Server 7 verrà rimossa dal sistema operativo dopo Windows 7. Le nuove applicazioni devono usare il Microsoft ODBC Driver for SQL Server in Windows, che supporta nuove funzionalità di SQL Server. È necessario eseguire la migrazione delle applicazioni esistenti anche al Microsoft ODBC Driver for SQL Server per migliorare le prestazioni, l'affidabilità e il supporto. Per informazioni rilevanti, vedere [aggiornamento di un'applicazione a SQL Server Native Client da MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Microsoft Jet motore di database 4,0:** A partire dalla versione 2,6, MDAC non contiene più componenti Jet. In altre parole, MDAC 2,6, 2,7 e 2,8 non contengono Microsoft Jet, il provider di OLE DB Microsoft Jet, i driver del database desktop di ODBC o DAO (Jet Data Access Objects). 

  Non esiste una versione a 64 bit del motore di database Jet, il driver di Jet OLEDB, i driver ODBC Jet o Jet DAO disponibili. Per altre informazioni, vedere l'[articolo della Knowledge Base 957570](https://support.microsoft.com/kb/957570). Nelle versioni a 64 bit di Windows, Jet a 32 bit viene eseguito nel sottosistema Windows WOW64. Per ulteriori informazioni su WOW64, vedere la [documentazione di WOW64 per MSDN](/windows/desktop/WinProg64/wow64-implementation-details). Le applicazioni native a 64 bit non possono comunicare con i driver Jet a 32 bit in esecuzione in WOW64.

  Anziché Microsoft Jet, Microsoft consiglia di usare [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) per lo sviluppo di nuove applicazioni non Microsoft Access che richiedono un archivio dati relazionale. Queste applicazioni Jet nuove o convertite possono continuare a usare Jet con l'intenzione di usare Microsoft Office 2003 e i file precedenti (. mdb e. xls) per l'archiviazione di dati non primari. Tuttavia, per queste applicazioni, è consigliabile pianificare la migrazione da Jet a Microsoft Access motore di database. È possibile [scaricare il motore di database di Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), che consente di leggere e scrivere file pre-esistenti nei formati di Office 2003 (file con estensione mdb e xls) o di Office 2007 (con estensione accdb, xlsm, xlsx e xlsb).

  > [!IMPORTANT]
  > Leggere il contratto di licenza con l'utente finale di Office System 2007 per limitazioni di utilizzo specifiche.

  > [!NOTE]
  > SQL Server applicazioni possono accedere anche a 2007 Office System e versioni precedenti, oltre a file da SQL Server le funzionalità di connettività dei dati eterogenei e Integrations Services, tramite il driver di Office System 2007. Inoltre, le applicazioni SQL Server a 64 bit possono accedere ai file di Office System a 32 bit e 2007 usando SQL Server Integration Services a 32 bit (SSIS) in Windows a 64 bit.

* **MSDADS:** Con il provider Microsoft OLE DB per data shaping (MSDADS), è possibile creare relazioni gerarchiche tra chiavi, campi o set di righe in un'applicazione. Non sono stati apportati miglioramenti alle funzionalità principali rispetto a MDAC 2,1. Questo provider è stato deprecato. Microsoft consiglia di utilizzare XML anziché MSDADS.
* **Oracle ODBC e oracle OLE DB:** Microsoft Oracle ODBC driver (Oracle ODBC) e provider Microsoft OLE DB per Oracle (Oracle OLE DB) forniscono l'accesso ai server di database Oracle. Vengono compilati usando Oracle Call Interface (OCI) versione 7 e offrono il supporto completo per Oracle 7. Inoltre, utilizza l'emulazione di Oracle 7 per fornire supporto limitato per i database Oracle 8. Oracle non supporta più le applicazioni che utilizzano le chiamate OCI versione 7. Queste tecnologie sono deprecate. Se si utilizzano origini dati Oracle, è necessario eseguire la migrazione al driver e al provider forniti da Oracle.
* **RDS:** SERVIZIO DATI DI RIFERIMENTO Servizi dati remoto (RDS) è un meccanismo proprietario di Microsoft per l'accesso a oggetti Recordset ADO remoti in Internet o Intranet. RDS è deprecato; non sono stati apportati miglioramenti importanti alle funzionalità di Servizi Desktop remoto da MDAC 2,1. Microsoft ha rilasciato il .NET Framework, che dispone di funzionalità SOAP complete e sostituisce i componenti Servizi Desktop remoto. Tutti i componenti server RDS verranno rimossi dal sistema operativo dopo Windows 7.
* **JRO:** Gli oggetti di replica Jet (JRO) sono deprecati. JRO viene utilizzato all'interno di ADO con*i database Jet (MDB) per creare e comprimere i database Jet (con estensione mdb) ed eseguire la gestione della replica Jet. MDAC 2,7 sarà l'ultima versione. JRO non sarà disponibile nel sistema operativo Windows a 64 bit. JRO non è supportato nel formato di file Microsoft Access 2007 (* con estensione accdb).
* **supporto ODBC a 16 bit:** Se si utilizzano applicazioni a 16 bit, è necessario eseguire la migrazione a un'applicazione a 32 bit. la funzionalità a 16 bit è deprecata ed è stata rimossa dai sistemi operativi a 64 bit. Per altre informazioni, vedere l'[articolo 896458 della Knowledge Base](https://support.microsoft.com/kb/896458).
* **Provider semplice OLEDB (MSDAOSP):** Il provider semplice OLEDB offre un Framework per la creazione rapida di provider di OLE DB su dati semplici. MSDAOSP è deprecato.
* **Libreria di cursori ODBC:** La libreria di cursori ODBC (ODBCCR32. dll) fornisce cursori dati lato client limitati. La libreria di cursori ODBC è stata deprecata. l'applicazione può utilizzare le implementazioni del cursore sul lato server come sostituzione.
* **OLE DB la comunicazione remota dell'interfaccia out-of-process:** La comunicazione remota dell'interfaccia OLEDB (msdaps. dll) è stata un tentativo di consentire ai provider di OLE DB di esaurirsi il processo. La comunicazione remota dell'interfaccia OLEDB out-of-process è deprecata.
* **Librerie di rete SQL di AppleTalk e Banyan VINES:** Le librerie di rete Banyan VINES, AppleTalk, ServerNet, IPX/SPX, Giganet e RPC SQL sono deprecate. Se si utilizza una di queste tecnologie, è necessario modificare le applicazioni in modo che utilizzino una delle altre librerie di rete, ad esempio TCP/IP e named pipe.

### <a name="mdacwdac-releases"></a>Versioni MDAC/WDAC

Di seguito è riportato un elenco degli scenari di supporto delle versioni precedenti di MDAC/WDAC, a partire dal meno recente.

* **Mdac 1,5, mdac 2,0 e mdac 2,1:** Queste versioni di MDAC erano versioni indipendenti rilasciate tramite l'opzione Pack di Microsoft Windows NT, Microsoft Windows Platform SDK o il sito Web MDAC. Queste versioni di MDAC non sono più supportate.
* **MDAC 2,5:** Questa versione di MDAC era inclusa nel sistema operativo Windows 2000. I Service Pack di MDAC 2,5 sono stati inclusi con i Service Pack di Windows 2000 corrispondenti.
* **MDAC 2,6:** MDAC 2,6 RTM, SP1 e SP2 sono stati inclusi rispettivamente con Microsoft SQL Server 2000 RTM, SP1 e SP2. Inoltre, questi Service Pack MDAC sono stati rilasciati nel sito Web MDAC in conformità alla pianificazione del rilascio del Service Pack Microsoft SQL Server 2000. È possibile installare questa versione di MDAC e i relativi Service Pack nelle piattaforme Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Questa versione di MDAC non è più supportata.
* **MDAC 2,7:** Questa versione di MDAC è stata inclusa nei sistemi operativi Microsoft Windows XP RTM e SP1. È possibile installare questa versione di MDAC e i relativi Service Pack in piattaforme Windows 2000, Windows Millennium, Windows NT e Windows 98. È possibile installare questa versione nella piattaforma Windows XP solo tramite il sistema operativo o i relativi Service Pack. Questa versione di MDAC non è più supportata.
* **MDAC 2,8:** Questa versione di MDAC è stata inclusa in Windows Server 2003 e Windows XP SP2 e versioni successive. È inoltre possibile installare questa versione di MDAC e i relativi Service Pack in Windows 2000.

  * Anche la versione a 32 bit di MDAC 2,8 è stata rilasciata al sito Web MDAC nello stesso momento in cui Windows Server 2003 è stato rilasciato al cliente.
  * La versione a 64 bit di MDAC 2,8 è stata rilasciata con la versione a 64 bit di Windows Server 2003 e Windows XP.

* **Windows Data Access Components (WDAC):** Il nome di MDAC è stato modificato in WDAC-"Windows Data Access Components" a partire da Windows Vista e Windows Server 2008. WDAC è incluso come parte del sistema operativo e non è disponibile separatamente per la ridistribuzione. Il servizio di WDAC è soggetto al ciclo di vita del sistema operativo.

  le versioni a 32 e 64 bit di WDAC vengono rilasciate rispettivamente con le versioni a 32 bit e a 64 bit dei sistemi operativi Windows.

## <a name="obsolete-data-access-technologies"></a>Tecnologie di accesso ai dati obsolete

Le tecnologie obsolete sono tecnologie che non sono state migliorate o aggiornate in diverse versioni del prodotto e che verranno escluse dalle versioni future del prodotto. Non utilizzare queste tecnologie quando si scrivono nuove applicazioni. Quando si modificano le applicazioni esistenti scritte tramite queste tecnologie, è consigliabile eseguire la migrazione di tali applicazioni a ADO.NET o a un'altra tecnologia corrente.

I componenti seguenti sono considerati obsoleti:

* **DB-Library:** DB-Library è un modello di programmazione specifiche di SQL Server che include le API C. Non sono stati apportati miglioramenti alla funzionalità per DB-Library a partire da SQL Server 6,5. La versione finale era con SQL Server 2000 e non verrà trasferita al sistema operativo Windows a 64 bit.
* **SQL embedded (E-SQL):** E-SQL è un modello di programmazione specifico per SQL Server che consente di incorporare istruzioni Transact-SQL nel codice Visual C. Non sono stati apportati miglioramenti alle funzionalità di E-SQL dalla SQL Server 6,5. La versione finale era con SQL Server 2000 e non verrà trasferita al sistema operativo Windows a 64 bit.
* **DAO (Data Access Objects):** DAO consente di accedere ai database JET (Access). Questa API può essere utilizzata da Microsoft Visual Basic, Microsoft Visual C++e linguaggi di scripting. È stata inclusa con Microsoft Office 2000 e Office XP. DAO 3,6 è la versione finale di questa tecnologia. Non sarà disponibile nel sistema operativo Windows a 64 bit.
* **Remote Data Objects (RDO):** RDO è stato progettato specificamente per accedere a origini dati relazionali ODBC remote e semplifica l'utilizzo di ODBC senza codice dell'applicazione complesso. È stata inclusa in Microsoft Visual Basic versioni 4, 5 e 6. La versione RDO 2,0 è stata la versione finale di questa tecnologia.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
