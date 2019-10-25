---
title: Home page per la programmazione client SQL | Microsoft Docs
description: Pagina Hub con collegamenti annotati a download e documentazione per diverse combinazioni di linguaggi e sistemi operativi, per la connessione a SQL Server o al database SQL di Azure.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451858"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page per la programmazione client per Microsoft SQL Server


Benvenuti nella Home page sulla programmazione client per interagire con Microsoft SQL Server e con il database SQL di Azure nel cloud. Questo articolo contiene le informazioni seguenti:

- Elenca e descrive le combinazioni di lingua e driver disponibili.
    - Vengono fornite informazioni per i sistemi operativi di Linux (Ubuntu e altri), MacOS e Windows.
- Fornisce collegamenti alla documentazione dettagliata per ogni combinazione.
- Consente di visualizzare le aree e le sottoaree della documentazione gerarchica per determinate lingue, ove appropriato.


#### <a name="azure-sql-database"></a>Database SQL di Azure

In qualsiasi linguaggio specifico, il codice che si connette a SQL Server è quasi identico al codice per la connessione al database SQL di Azure.

Per informazioni dettagliate sulle stringhe di connessione per la connessione al database SQL di Azure, vedere:

- [Usare .NET Core (C#) per eseguire query su un database SQL di Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Altro database SQL di Azure che si trova nelle vicinanze dell'articolo precedente nel sommario, sulle altre lingue. Vedere, ad esempio, [usare php per eseguire query su un database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Pagine Web di compilazione-app

Le pagine Web di *compilazione di un'app* presentano esempi di codice, insieme alle informazioni di configurazione, in un formato alternativo. Per ulteriori informazioni, vedere più avanti in questo articolo la [sezione denominata *Build-an-app website*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Linguaggi e driver per i programmi client


Nella tabella seguente, ogni immagine della lingua è un collegamento a dettagli sull'utilizzo della lingua con SQL Server. Ogni collegamento passa a una sezione successiva di questo articolo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| [logo ![C# ][image-ref-320-csharp]](#an-110-ado-net-docu) &nbsp; | &nbsp; [![ORM Entity Framework di .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logo di Java][image-ref-330-java]](#an-130-jdbc-docu) |
| [logo &nbsp; ![Node. js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | [logo ![PHP][image-ref-360-php]](#an-170-php-docu) &nbsp; |
| &nbsp; [![Logo Python][image-ref-370-python]](#an-180-python-docu) | [logo ![Ruby][image-ref-380-ruby]](#an-190-ruby-docu) &nbsp; | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Download e installazioni

L'articolo seguente è dedicato a scaricare e installare vari driver di connessione SQL per l'uso da parte dei linguaggi di programmazione:

- [Driver di SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#logo][image-ref-320-csharp] C#uso di ADO.NET

I linguaggi gestiti .NET, ad esempio C# e Visual Basic, sono gli utenti più comuni di ADO.NET. *ADO.NET* è un nome casuale per un subset di classi .NET Framework.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite ADO.NET](./ado-net/step-3-connect-sql-ado-net.md) | Un piccolo esempio di codice si concentra sulla connessione e sull'esecuzione di query SQL Server. |
| [Connettersi in modo resiliente a SQL con ADO.NET](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | Logica di ripetizione dei tentativi in un esempio di codice, poiché le connessioni possono occasionalmente riscontrare momenti di perdita della connettività.<br /><br />La logica di ripetizione dei tentativi si applica correttamente alle connessioni gestite tramite Internet in qualsiasi database cloud, ad esempio nel database SQL di Azure. |
| [Database SQL di Azure: dimostrazione di come usare .NET Core in Windows/Linux/macOS per creare un C# programma, connettersi ed eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Esempio di database SQL di Azure. |
| [Build-an-app: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

|||
| :-- | :-- |
| [C#uso di ADO.NET](./ado-net/index.md)| Radice della documentazione. |
| [Spazio dei nomi: System. Data](https://docs.microsoft.com/dotnet/api/system.data) | Set di classi utilizzato per ADO.NET. |
| [Spazio dei nomi: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | Il set di classi più direttamente al centro di ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logo di Entity Framework][image-ref-333-ef] Entity Framework (EF) con C&#x23;

Entity Framework (EF) fornisce il mapping relazionale a oggetti (ORM). ORM semplifica il codice sorgente di programmazione orientata a oggetti (OOP) per modificare i dati recuperati da un database SQL relazionale.

EF presenta relazioni dirette o indirette con le tecnologie seguenti:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)o [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Miglioramenti della sintassi del linguaggio, ad esempio l'operatore **=>** C#in.
- Programmi pratici che generano codice sorgente per le classi che vengono mappate alle tabelle nel database SQL. Ad esempio, [EdmGen. exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>EF originale e nuovo EF

La [pagina iniziale per Entity Framework](https://docs.microsoft.com/ef/) introduce EF con una descrizione simile alla seguente:

- Entity Framework è un mapper relazionale a oggetti (O/RM) che consente agli sviluppatori .NET di utilizzare un database tramite oggetti .NET. Elimina la necessità della maggior parte del codice sorgente di accesso ai dati che in genere gli sviluppatori devono scrivere.

*Entity Framework* è un nome condiviso da due rami di codice sorgente distinti. Un ramo EF è obsoleto e il relativo codice sorgente può ora essere gestito dal pubblico. L'altro EF è nuovo. I due EFs sono descritti di seguito:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft ha rilasciato il primo EF nel 2008 agosto. Nel marzo 2015 Microsoft ha annunciato che EF 6. x era la versione finale che Microsoft svilupperebbe. Microsoft ha rilasciato il codice sorgente nel dominio pubblico.<br /><br />Inizialmente EF faceva parte di .NET Framework. Tuttavia, EF 6. x è stato rimosso da .NET Framework.<br /><br />[Codice sorgente EF 6. x su GitHub, nel repository *ASPNET/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft ha rilasciato il EF Core appena sviluppato nel 2016 giugno. EF Core è progettato per offrire maggiore flessibilità e portabilità. EF Core possono essere eseguiti in sistemi operativi oltre a Microsoft Windows. E EF Core possono interagire con i database oltre a Microsoft SQL Server e altri database relazionali.<br /><br />**Esempi&#x23; di codice C:**<br />[Introduzione con Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introduzione a EF Core in .NET Framework con un database esistente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF e le tecnologie correlate sono potenti e sono molto utili per gli sviluppatori che desiderano padroneggiare l'intera area.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logo di Java][image-ref-330-java] Java e JDBC

Microsoft fornisce un driver Java Database Connectivity (JDBC) per l'uso con SQL Server (o con il database SQL di Azure, ovviamente). Si tratta di un driver JDBC di tipo 4 che offre connettività di database tramite le interfacce API (Application Program Interface) JDBC standard.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Esempi di codice](./jdbc/code-samples/index.md) | Esempi di codice che insegnano sui tipi di dati, i set di risultati e i dati di grandi dimensioni. |
| [Esempio di URL di connessione](./jdbc/connection-url-sample.md) | Viene descritto come utilizzare un URL di connessione per connettersi a SQL Server. Utilizzarlo quindi per utilizzare un'istruzione SQL per recuperare i dati. |
| [Esempio di origine dati](./jdbc/data-source-sample.md) | Viene descritto come utilizzare un'origine dati per connettersi a SQL Server. Usare quindi un stored procedure per recuperare i dati. |
| [Usare Java per eseguire query su un database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Esempio di database SQL di Azure. |
| [Crea app Java usando SQL Server in Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

La documentazione di JDBC include le aree principali seguenti:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Radice della documentazione di JDBC. |
| [Riferimento](./jdbc/reference/index.md) | Interfacce, classi e membri. |
| [Guida di programmazione per il driver PHP per SQL](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logo node. js][image-ref-340-node] Node.js

Con node. js è possibile connettersi a SQL Server da Windows, Linux o Mac. La radice della documentazione di node. js è disponibile [qui](./node-js/index.md).

Il driver della connessione node. js per SQL Server è implementato in JavaScript. Il driver usa il protocollo TDS, supportato da tutte le versioni moderne di SQL Server. Il driver è un progetto open source, [disponibile in GitHub](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Codice sorgente Bare Bones per la connessione a SQL Server e l'esecuzione di una query. |
| [Database SQL di Azure: usare node. js per eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Esempio per il database SQL di Azure nel cloud. |
| [Creare app node. js da usare SQL Server in macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC perC++ 

![Logo ODBC][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

Open Database Connectivity (ODBC) è stato sviluppato negli anni '90 e precede .NET Framework. ODBC è progettato per essere indipendente da un sistema di database particolare e indipendente dal sistema operativo.

Nel corso degli anni sono stati creati e rilasciati numerosi driver ODBC da gruppi all'interno e all'esterno di Microsoft. L'intervallo di driver implica diversi linguaggi di programmazione client. L'elenco di destinazioni di dati va oltre SQL Server.

Altri driver di connettività utilizzano ODBC internamente.

#### <a name="code-example"></a>Esempio di codice

- [Esempio di codice C++ che usa ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Struttura della documentazione

Il contenuto ODBC in questa sezione è incentrato sull'accesso a SQL Server o al database SQL di C++Azure, da. Nella tabella seguente sono elencati i profili approssimativi della documentazione principale per ODBC.


| Area | Area secondaria | Descrizione |
| :--- | :------ | :---------- |
| [ODBC perC++](./odbc/index.md) | Radice della documentazione. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Informazioni sull'uso di ODBC nei sistemi operativi Linux o MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informazioni sull'utilizzo di ODBC nel sistema operativo Windows. |
| [Amministrazione](../odbc/admin/index.md) | &nbsp; | Strumento di amministrazione per la gestione delle origini dati ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Diversi driver ODBC creati e forniti da Microsoft. |
| [Concettuale e riferimento](../odbc/reference/index.md) | &nbsp; | Informazioni concettuali sull'interfaccia ODBC, oltre ai riferimenti tradizionali. |
| &nbsp; " | [Appendici](../odbc/reference/appendixes/index.md)    | Tabelle di transizione di stato, libreria di cursori ODBC e altro ancora. |
| &nbsp; " | [Sviluppare un'app](../odbc/reference/develop-app/index.md)  | Funzioni, handle e molto altro ancora. |
| &nbsp; " | [Sviluppare driver](../odbc/reference/develop-driver/index.md) | Come sviluppare un driver ODBC personalizzato, se si dispone di un'origine dati specializzata. |
| &nbsp; " | [Installazione](../odbc/reference/install/index.md) | Installazione ODBC, sottochiavi e altro ancora. |
| &nbsp; " | [Sintassi](../odbc/reference/syntax/index.md)   | API per l'installazione, il programma di installazione, la conversione e l'accesso ai dati. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logo PHP][image-ref-360-php] PHP

È possibile utilizzare PHP per interagire con SQL Server. La radice della documentazione di PHP è disponibile [qui](./php/index.md).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Un piccolo esempio di codice si concentra sulla connessione e sull'esecuzione di query SQL Server. |
| [Connettere in modo resiliente a SQL con PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Logica di ripetizione dei tentativi in un esempio di codice, poiché le connessioni attraverso Internet e il cloud possono occasionalmente riscontrare momenti di perdita della connettività. |
| [Database SQL di Azure: usare PHP per eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Esempio di database SQL di Azure. |
| [Creare app PHP da usare SQL Server su RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logo di Python][image-ref-370-python] Python


È possibile usare Python per interagire con SQL Server.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica della connessione a SQL con Python con pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Un piccolo esempio di codice si concentra sulla connessione e sull'esecuzione di query SQL Server. |
| [Database SQL di Azure: usare Python per eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Esempio di database SQL di Azure. |
| [Creare app PHP da usare SQL Server su SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

| Area | Descrizione |
| :--- | :---------- |
| [Da Python a SQL Server](./python/index.md) | Radice della documentazione. |
| [driver pymssql](./python/pymssql/index.md) | Microsoft non gestisce né testa il driver pymssql.<br /><br />Il driver della connessione pymssql è un'interfaccia semplice per i database SQL, da usare nei programmi Python. Pymssql si basa su FreeTDS per fornire un'interfaccia di Python DB-API (PEP-249) per Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/index.md)   | Il driver della connessione pyodbc è un modulo Open Source di Python che semplifica l'accesso ai database ODBC. Implementa la specifica dell'API di database 2,0, ma è dotata di praticità ancora maggiore. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logo rubino][image-ref-380-ruby] Ruby

È possibile usare Ruby per interagire con SQL Server. La radice della documentazione di Ruby è disponibile [qui](./ruby/index.md).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Un piccolo esempio di codice si concentra sulla connessione e sull'esecuzione di query SQL Server. |
| [Database SQL di Azure: usare Ruby per eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Esempio di database SQL di Azure. |
| [Creare app Ruby per usare SQL Server in MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informazioni di configurazione, insieme ad esempi di codice. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Sito web Build-an-app per lo sviluppo di client SQL](https://www.microsoft.com/sql-server/developer-get-started/)


Nelle pagine Web di [*Build-a-app*](https://www.microsoft.com/sql-server/developer-get-started/) è possibile scegliere tra un lungo elenco di linguaggi di programmazione per la connessione a SQL Server. E il programma client può eseguire un'ampia gamma di sistemi operativi.

*Build-a-app* enfatizza la semplicità e la completezza per lo sviluppatore che sta appena iniziando. I passaggi illustrano le attività seguenti:

1. Come installare Microsoft SQL Server
2. Come scaricare e installare gli strumenti e i driver.
3. Come eseguire le configurazioni necessarie, a seconda del sistema operativo scelto.
4. Come compilare il codice sorgente fornito.
5. Come eseguire il programma.

Di seguito sono riportate alcune indicazioni approssimative dei dettagli disponibili sul sito Web:

#### <a name="java-on-ubuntu"></a>Java in Ubuntu:

1. Configurare l'ambiente
    - Passaggio 1.1 installare SQL Server
    - Passaggio 1,2 installare Java
    - Passaggio 1,3 installare Java Development Kit (JDK)
    - Passaggio 1,4 installare Maven
2. Creare un'applicazione Java con SQL Server
    - Passaggio 2,1 creare un'app Java che si connette a SQL Server ed esegue query
    - Passaggio 2,2 creare un'app Java che si connette a SQL Server usando il comune ibernazione del Framework
3. Rendere l'app java fino a 100 volte più veloce
    - Passaggio 3,1 creare un'app java per illustrare gli indici columnstore

#### <a name="python-on-windows"></a>Python in Windows:

1. Configurare l'ambiente
    - Passaggio 1.1 installare SQL Server
    - Passaggio 1,2 installare Python
    - Passaggio 1,3 installare il driver ODBC e l'utilità da riga di comando SQL per SQL Server
2. Creare un'applicazione Python con SQL Server
    - Passaggio 2,1 installare il driver Python per SQL Server
    - Passaggio 2,2 creare un database per l'applicazione
    - Passaggio 2,3 creare un'app Python che si connette a SQL Server ed esegue query
3. Rendere l'app Python fino a 100 volte più veloce
    - Passaggio 3,1 creare una nuova tabella con 5 milioni usando sqlcmd
    - Passaggio 3,2 creare un'app Python che esegue una query su questa tabella e misura il tempo impiegato
    - Passaggio 3,3 misurare il tempo necessario per eseguire la query
    - Passaggio 3,4 aggiungere un indice columnstore alla tabella
    - Passaggio 3,5 misurare il tempo necessario per eseguire la query con un indice columnstore

Gli screenshot seguenti forniscono un'idea dell'aspetto del sito Web della documentazione per lo sviluppo di SQL.

#### <a name="choose-a-language"></a>Scegliere una lingua:

![Sito Web di SQL dev, iniziare][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Scegliere un sistema operativo:

![Sito Web SQL dev, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Altre attività di sviluppo


In questa sezione vengono forniti collegamenti su altre opzioni di sviluppo. Sono inclusi l'uso di queste stesse lingue per lo sviluppo di Azure in generale. Le informazioni vanno oltre la destinazione solo del database SQL di Azure e Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub per sviluppatori per Azure

- [Hub per sviluppatori per Azure](https://docs.microsoft.com/azure/)
- [Azure per sviluppatori .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure per sviluppatori Java](https://docs.microsoft.com/java/azure/)
- [Azure per sviluppatori node. js](https://docs.microsoft.com/nodejs/azure/)
- [Azure per sviluppatori Python](https://docs.microsoft.com/python/azure/)
- [Creare un'app Web PHP in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Altri linguaggi

- [Crea app go usando SQL Server in Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

