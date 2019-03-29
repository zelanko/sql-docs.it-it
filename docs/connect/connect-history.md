---
title: Cronologia di driver per Microsoft SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: craigg
ms.openlocfilehash: e6656b2df8eb635686dd5702d9b60a644a04e29b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511618"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Cronologia di driver per Microsoft SQL Server

Questa pagina descrive i dati cronologici connessione le tecnologie Microsoft per la connessione a SQL Server.

## <a name="odbc"></a>ODBC

Sono disponibili tre generazioni distinte dei driver Microsoft ODBC per SQL Server. Il driver ODBC di "SQL Server" primo viene ancora fornito come parte della [Windows Data Access Components](#microsoft-or-windows-data-access-components). Non è consigliabile usare il driver per i nuovi sviluppi. A partire da SQL Server 2005, il [SQL Server Native Client](#sql-server-native-client) include un'interfaccia ODBC e il driver ODBC fornito con SQL Server 2005 tramite SQL Server 2012. Non è consigliabile usare il driver per i nuovi sviluppi. Dopo SQL Server 2012, il [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) è il driver che viene aggiornato con le funzionalità server più recenti in futuro.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client è una libreria autonoma che viene usata per OLE DB e ODBC. SQL Server Native Client (SNAC spesso abbreviata) è stato incluso in SQL Server 2005-2012. SQL Server Native Client può essere utilizzato per le applicazioni che devono usufruire delle nuove funzionalità introdotte in SQL Server 2005 tramite SQL Server 2012. (Microsoft/Windows Data Access Components non aggiornati per queste nuove funzionalità di SQL Server). Per le nuove funzionalità oltre a SQL Server 2012, SQL Server Native Client non verrà aggiornato. Passare a Microsoft ODBC Driver per SQL Server o il Driver OLE DB Microsoft per SQL Server se si vuole sfruttare i vantaggi delle nuove funzionalità di SQL Server in futuro.

Per una documentazione completa di SQL Server Native Client, vedere la [documentazione di SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md).

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

Dopo SQL Server 2012, sviluppati e rilasciati come Microsoft ODBC Driver for SQL Server primaria ODBC driver for SQL Server. Per altre informazioni, vedere la [Microsoft ODBC Driver per la documentazione di SQL Server](./odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="ole-db"></a>OLE DB

Sono disponibili tre generazioni distinte di provider Microsoft OLE DB per SQL Server. Il primo "Microsoft OLE DB Provider per SQL Server" (SQLOLEDB) viene ancora fornito come parte della [Windows Data Access Components](#microsoft-or-windows-data-access-components). Questo provider non verrà aggiornato con le nuove funzionalità e non è consigliabile usare il driver per i nuovi sviluppi. A partire da SQL Server 2005, il [SQL Server Native Client](#sql-server-native-client) include un'interfaccia di provider OLE DB (SQLNCLI) ed è il provider OLE DB fornito con SQL Server 2005 tramite SQL Server 2017. Era [annunciate come deprecate nel 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e non è consigliabile usare il driver per i nuovi sviluppi. Nel 2017, tecnologia di accesso ai dati di OLE DB è stata successivamente [deprecata ed è stata annunciata una nuova versione pianificata](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) per il 2018. Il nuovo provider OLE DB viene chiamato il "Microsoft OLE DB Driver per SQL Server" (MSOLEDBSQL) e attualmente è gestito e supportato.

## <a name="adonet"></a>ADO.NET

ADO.NET è stata introdotta con Microsoft .NET Framework e continua a essere migliorato e gestito. È un componente essenziale di Microsoft .NET Framework. Per altre informazioni, vedere [Microsoft ADO.NET per SQL Server](ado-net/microsoft-ado-net-for-sql-server.md).

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver per SQL Server

Introdotto nel 2000, Microsoft JDBC Driver per SQL Server continua a essere migliorato e gestito. È stato reso open source nel 2016. Per informazioni più recenti, tra cui come scaricare il driver, vedere [Panoramica del Driver JDBC](./jdbc/overview-of-the-jdbc-driver.md).

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Driver Microsoft per PHP per SQL Server

Introdotto nel 2009 come progetto open source, Microsoft Drivers per PHP per SQL Server continuano a essere migliorato e gestito. Per informazioni più recenti, tra cui come scaricare il driver PHP, vedere [Microsoft Drivers per PHP per SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Driver Microsoft per Node. js per SQL Server

Il Driver Microsoft per Node. js per SQL Server consente alle applicazioni Node. js in Microsoft Windows e Microsoft Windows Azure di accedere a Microsoft SQL Server e Database SQL di Microsoft Windows Azure. Attività di sviluppo sono in corso smette di questo driver. È consigliabile non creare nuove applicazioni usando il Driver Microsoft per Node. js per SQL Server.

Per altre informazioni sul Driver Microsoft per Node. js per SQL Server, vedere [WindowsAzure / nodo-sqlserver](https://github.com/Azure/node-sqlserver).

### <a name="tedious"></a>Tedious

Microsoft contribuisce a attualmente e supporta il modulo tedious open source in Node. js per la connettività a SQL Server usando JavaScript. Per altre informazioni, vedere [Driver Node. js per SQL Server](./node-js/node-js-driver-for-sql-server.md).

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft o Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) vengono forniti con e supportati da Windows per applicazioni con le versioni precedenti la compatibilità e non fanno parte dello stack di tecnologie SQL Server corrente. Non verrà aggiunto ai componenti MDAC/WDAC nuove funzionalità e non è consigliabile usarli per lo sviluppo di nuove applicazioni.

Ai fini di questo documento, è possibile suddividere lo stack MDAC/WDAC nei componenti seguenti, basati sulla tecnologia e i prodotti:

* **ADO** (inclusi ADOMD e ADOX)
* **OLE DB** (inclusi i servizi principali OLE DB, il Provider SQL Server OLE DB, Provider OLE DB Oracle, Provider OLE DB per ODBC driver e Provider Data Shape Provider di dati remoto)
* **ODBC** (incluso Gestione Driver ODBC, Driver ODBC di SQL e Driver ODBC per Oracle)

### <a name="mdacwdac-components"></a>Componenti MDAC/WDAC

MDAC/WDAC include questi componenti:

* **ODBC:** l'interfaccia di Microsoft Open Database Connectivity (ODBC) è un'interfaccia di linguaggio di programmazione C che consente alle applicazioni di accedere ai dati da un'ampia gamma di sistemi DBMS (Database Management). Le applicazioni che usano questa API sono limitate alla possibilità di accedere solo alle origini dati relazionali.
* **OLE DB:** OLE DB è un set di interfacce COM per l'accesso ai dati in un'ampia gamma di archivi dati. Provider OLE DB sono disponibili per l'accesso ai dati nel database, file System, archivi di messaggi, servizi di directory, del flusso di lavoro e archivi di documenti.
* **ADO:** ActiveX Data Objects (ADO) fornisce un modello di programmazione di alto livello. Sebbene un po' meno efficiente rispetto alla scrittura del codice direttamente per OLE DB o ODBC, ADO è semplice da capire e utilizzare. Può essere utilizzato dai linguaggi di script, ad esempio Microsoft Visual Basic, Scripting Edition (VBScript) o Microsoft JScript.
* **ADOMD:** multidimensionale ADO (ADOMD) deve essere utilizzato con i provider di dati multidimensionali, ad esempio Provider di Microsoft OLAP, nota anche come Provider di servizi di analisi Microsoft. Nessun miglioramenti delle funzionalità principali sono stati apportati a esso MDAC 2.0.
* **ADOX:** estensioni ADO per DDL e protezione (ADOX) consentono la creazione e modifica delle definizioni di un database, tabelle, indici o stored procedure. È possibile usare ADOX con qualsiasi provider. Il Provider OLE DB Microsoft Jet fornisce supporto completo per ADOX, mentre il Provider OLE DB Microsoft SQL Server offre un supporto limitato.
* **Librerie di rete di Microsoft SQL Server:** le librerie di rete SQL Server consentono di SQLOLEDB e SQLODBC comunicare con il database di SQL Server. Le seguenti librerie di rete SQL Server sono state deprecate nelle versioni MDAC/WDAC: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, tecnologia Giganet e RPC. TCP/IP e Named Pipes continuerà a essere supportato e sono disponibili nel sistema operativo Windows a 64 bit.
* **MSDASQL:** il Provider Microsoft OLE DB per ODBC (MSDASQL) consente alle applicazioni basate su OLE DB e ADO (che usa OLE DB internamente) per accedere alle origini dati tramite un driver ODBC. MSDASQL è un provider OLE DB che si connette a ODBC, invece di un database. È destinato che funge da ponte da OLE DB a un driver ODBC quando è presente alcun provider OLE DB diretto per un'origine dati. MSDASQL viene fornito con il sistema operativo Windows e Windows Server 2008 e Vista SP1 sono stati che il primo Windows rilascia in modo da includere una versione a 64 bit della tecnologia.

### <a name="deprecated-mdacwdac-components"></a>Componenti MDAC/WDAC deprecati

Questi componenti sono ancora supportati nella versione di MDAC/WDAC corrente, ma potrebbe essere rimosso nelle versioni future. Quando si sviluppano nuove applicazioni, è consigliabile evitare di utilizzare questi componenti. Inoltre, quando si aggiorna o si modificano applicazioni esistenti, rimuovere qualsiasi dipendenza in questi componenti.

* **SQLOLEDB:** Il Provider Microsoft OLE DB per SQL Server (SQLOLEDB), che supporta l'accesso a Microsoft SQL Server, è stato deprecato. La connettività a future versioni di SQL Server potrebbe non essere supportata. La possibilità di connettersi a versioni precedenti a SQL Server 7 verrà rimosso dal sistema operativo dopo Windows 7. Nuove applicazioni devono utilizzare il Driver OLE DB Microsoft per SQL Server (MSOLEDBSQL), che supporta le nuove funzionalità di SQL Server. Le applicazioni esistenti devono essere migrati per Driver OLE DB Microsoft per SQL Server nonché per migliori prestazioni, affidabilità e supporto. Per altre informazioni, vedere [aggiornamento di un'applicazione al Driver OLE DB per SQL Server da MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** di Microsoft SQL Server ODBC Driver (SQLODBC), che supporta l'accesso a Microsoft SQL Server, è stato deprecato. La connettività a future versioni di SQL Server potrebbe non essere supportata. La possibilità di connettersi a versioni precedenti a SQL Server 7 verrà rimosso dal sistema operativo dopo Windows 7. Nuove applicazioni devono utilizzare Microsoft ODBC Driver for SQL Server in Windows, che supporta le nuove funzionalità di SQL Server. Le applicazioni esistenti devono essere migrati a Microsoft ODBC Driver for SQL Server anche per migliori prestazioni, affidabilità e supporto. Per informazioni rilevanti, vedere [l'aggiornamento di un'applicazione da MDAC a SQL Server Native Client](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Motore di Database Microsoft Jet 4.0:** a partire dalla versione 2.6, MDAC non contiene più componenti di Jet. In altre parole, MDAC 2.6 2.7 e 2.8 non contengono Microsoft Jet, il Provider OLE DB Microsoft Jet, il driver di Database Desktop ODBC o Jet oggetti DAO (Data Access). 

  Non è disponibile alcuna versione a 64 bit del motore di Database Jet, il Driver OLE DB per Jet, i driver Jet ODBC o DAO Jet. Per altre informazioni, vedere l'[articolo della Knowledge Base 957570](https://support.microsoft.com/kb/957570). Nelle versioni a 64 bit di Windows, a 32 bit Jet viene eseguito con il sottosistema WOW64 Windows. Per altre informazioni su WOW64, vedere la [documentazione di MSDN WOW64](/windows/desktop/WinProg64/wow64-implementation-details). Le applicazioni native a 64 bit non possono comunicare con i driver Jet 32 bit in esecuzione in WOW64.

  Invece di Microsoft Jet, Microsoft consiglia di usare [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) durante lo sviluppo di nuove, le applicazioni non Microsoft Access che richiedono un archivio dati relazionale. Queste applicazioni di Jet nuove o convertite possono continuare a usare Jet con l'intenzione di utilizzo di Microsoft Office 2003 e versioni precedenti (con estensione mdb e file con estensione xls) per archiviare i dati non primaria. Tuttavia, per queste applicazioni, è consigliabile pianificare la migrazione da Jet al motore di Database Microsoft Access. È possibile [scaricare il motore di database di Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920), che consente di leggere e scrivere file pre-esistenti nei formati di Office 2003 (file con estensione mdb e xls) o di Office 2007 (con estensione accdb, xlsm, xlsx e xlsb).

  > [!IMPORTANT]
  > Leggere il contratto di licenza 2007 Office System utente finale per le limitazioni di utilizzo specifici.

  > [!NOTE]
  > Applicazioni di SQL Server possono inoltre accedere a Office System 2007 e in precedenza, i file dalla connettività di SQL Server dei dati eterogenee e Integrations Services, nonché le funzionalità tramite il Driver di Office System 2007. Inoltre, a 64 bit SQL Server applicazioni possono accedere a 32 bit Jet e file di Office System 2007 con 32 bit SQL Server Integration Services (SSIS) in Windows a 64 bit.

* **MSDADS:** con Provider Microsoft OLE DB per Data Shaping (MSDADS), è possibile creare relazioni gerarchiche tra le chiavi, campi o i set di righe in un'applicazione. Nessun miglioramenti delle funzionalità principali sono stati apportati 2.1 MDAC. Questo Provider è stato deprecato. Microsoft consiglia di usare codice XML, anziché MSDADS.
* **Oracle ODBC e OLE DB Oracle:** Microsoft Oracle ODBC Driver (Oracle ODBC) e il Provider Microsoft OLE DB per Oracle (Oracle OLE DB) forniscono l'accesso ai server di database Oracle. Che vengono compilati utilizzando Oracle Call Interface (OCI) versione 7 e forniscono il supporto completo per Oracle 7. Inoltre, Usa l'emulazione di Oracle 7 per fornire un supporto limitato per i database Oracle 8. Oracle non supporta più applicazioni che usano le chiamate OCI versione 7. Queste tecnologie sono deprecate. Se si usano Origini dati Oracle, è necessario eseguire la migrazione al provider e driver fornito da Oracle.
* **RDS:** SERVIZIO DATI DI RIFERIMENTO Servizi dati remoto (RDS) è un meccanismo proprietario di Microsoft per l'accesso a oggetti Recordset ADO remoti in Internet o Intranet. Servizi Desktop remoto è deprecato. Nessun miglioramenti delle funzionalità principali sono stati apportati a Servizi Desktop remoto 2.1 MDAC. Microsoft ha rilasciato .NET Framework, che dispone di numerose funzionalità di SOAP e sostituisce i componenti Servizi Desktop remoto. Tutti i componenti server di servizi desktop remoto vengono rimosse dal sistema operativo dopo Windows 7.
* **JRO:** Jet replica oggetti (JRO) è deprecato. JRO viene usato all'interno di ADO con Jet (*con estensione mdb) i database per creare e comprimere il database Jet (mdb) ed eseguire la gestione delle repliche Jet. MDAC 2.7 sarà l'ultima versione. JRO non sarà disponibili nel sistema operativo Windows a 64 bit. JRO non è supportato nel formato di file di Microsoft Access 2007 (* accdb).
* **Supporto di ODBC 16 bit:** se si usa applicazioni a 16 bit, è necessario eseguire la migrazione a un'applicazione a 32 bit. la funzionalità di 16 bit è deprecata ed è stato rimosso dai sistemi operativi a 64 bit. Per altre informazioni, vedere l'[articolo 896458 della Knowledge Base](https://support.microsoft.com/kb/896458).
* **Provider OLE DB semplici (MSDAOSP):** OLEDB Provider semplice offre un framework per creare rapidamente i provider OLE DB su dati semplici. MSDAOSP è deprecata.
* **Libreria di cursori ODBC:** libreria di cursori ODBC (Odbccr32) fornisce i cursori dati lato client limitati. Libreria di cursori ODBC è deprecata. l'applicazione può usare le implementazioni di cursore lato server come una sostituzione.
* **.NET Remoting interfaccia Out-of-Process di OLE DB:** remoting interfaccia OLE DB (msdaps.dll) è un tentativo di consentire ai provider OLE DB per l'esecuzione fuori del processo. Servizi remoti Out-of-Process interfaccia OLE DB sono deprecato.
* **AppleTalk e librerie di rete Banyan Vines SQL:** The Banyan Vines, AppleTalk, ServerNet, IPX/SPX, tecnologia Giganet e RPC SQL librerie di rete sono deprecate. Se si usa uno qualsiasi di queste tecnologie, è necessario modificare le applicazioni affinché utilizzino una delle altre librerie di rete, ad esempio TCP/IP e Named Pipe.

### <a name="mdacwdac-releases"></a>Versioni MDAC/WDAC

Ecco un elenco degli scenari di supporto delle versioni precedenti di MDAC/WDAC, partire dal meno recente.

* **1.5 di MDAC, MDAC 2.0 e 2.1 MDAC:** queste versioni di MDAC sono versioni indipendenti che sono state rilasciate tramite Microsoft Windows NT Option Pack, il SDK della piattaforma Microsoft Windows o il sito Web di MDAC. Queste versioni di MDAC non sono più supportate.
* **MDAC 2.5:** questa versione di MDAC è stata fornita con il sistema operativo Windows 2000. Service Pack di MDAC 2.5 sono state incluse con Windows 2000 service Pack corrispondente.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 e SP2 fornite con la versione RTM di Microsoft SQL Server 2000 SP1 e SP2, rispettivamente. Inoltre, i service pack MDAC sono state rilasciate al sito Web di MDAC conforme alla pianificazione di rilascio di service pack di Microsoft SQL Server 2000. È possibile installare questa versione di MDAC e i relativi service pack su piattaforme Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 e Windows 98. Questa versione di MDAC non è non è più supportata.
* **MDAC 2.7:** questa versione di MDAC è stata inclusa con i sistemi operativi Microsoft Windows XP RTM e SP1. È possibile installare questa versione di MDAC e i relativi service pack su piattaforme Windows 2000, Windows Millennium, Windows NT e Windows 98. È possibile installare questa versione della piattaforma Windows XP solo tramite il sistema operativo o i relativi pacchetti di servizi. Questa versione di MDAC non è non è più supportata.
* **MDAC 2.8:** questa versione di MDAC era incluso in Windows Server 2003 e Windows XP SP2 e versioni successive. È anche possibile installare questa versione di MDAC e i relativi service pack in Windows 2000.

  * La versione a 32 bit di MDAC 2.8 è stato anche rilasciata al sito Web di MDAC allo stesso tempo che Windows Server 2003 è stato rilasciato al cliente.
  * La versione a 64 bit di MDAC 2.8 è stata rilasciata con la versione a 64 bit di Windows Server 2003 e Windows XP.

* **Windows Data Access Components (WDAC):** MDAC cambiato nome in WDAC - "Windows Data Access Components" a partire da Windows Vista e Windows Server 2008. WDAC è incluso come parte del sistema operativo e non è disponibile separatamente per la ridistribuzione. Facilità di manutenzione per WDAC è soggetto al ciclo di vita del sistema operativo.

  versioni a 32 e 64 bit di WDAC vengono rilasciate con le versioni a 32 e 64 bit dei sistemi operativi Windows, rispettivamente.

## <a name="obsolete-data-access-technologies"></a>Tecnologie di accesso ai dati obsoleto

Tecnologie obsolete sono le tecnologie che non sono stati avanzati o aggiornate nelle diverse versioni di prodotto e che verranno esclusi dalla versioni future del prodotto. Non usare queste tecnologie quando si scrivono nuove applicazioni. Quando si modificano applicazioni esistenti in cui vengono scritti utilizzando queste tecnologie, prendere in considerazione la migrazione di tali applicazioni ADO.NET o un'altra tecnologia corrente.

I componenti seguenti sono considerati obsoleti:

* **DB-Library:** DB-Library è un modello di programmazione specifiche di SQL Server che include le API C. Sono non stati apportati alcuna modifica in DB-Library dopo SQL Server 6.5. Rilascio della versione finale è stato effettuato con SQL Server 2000 e verrà non essere trasferita al sistema operativo Windows a 64 bit.
* **Embedded SQL (E-SQL):** E-SQL è un modello di programmazione specifiche di SQL Server che consente di istruzioni Transact-SQL per essere incorporati nel codice Visual C#. Miglioramenti della funzionalità non sono stati apportati alle istruzioni SQL E SQL Server 6.5. Rilascio della versione finale è stato effettuato con SQL Server 2000 e verrà non essere trasferita al sistema operativo Windows a 64 bit.
* **Data Access Objects (DAO):** DAO fornisce l'accesso ai database JET (accesso). Questa API può essere usata da Microsoft Visual Basic, Microsoft Visual C++ e linguaggi di scripting. È stato incluso in Microsoft Office 2000 e Office XP. 3.6 DAO è la versione finale di questa tecnologia. Non sarà disponibile nel sistema operativo Windows a 64 bit.
* **Oggetti dati remoti (RDO):** RDO è stato progettato specificamente per l'accesso remoto alle origini dati relazionali ODBC e ancora più facile utilizzare ODBC senza codice di applicazione complesse. È stato incluso con Microsoft Visual Basic le versioni 4, 5 e 6. RDO versione 2.0 è la versione finale di questa tecnologia.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
