---
title: Home page per SQL client programming | Microsoft Docs
description: Pagina hub con annotazioni collegamenti ai download e documentazione per le combinazioni di numerosi linguaggi e sistemi operativi, per la connessione a SQL Server o Database SQL di Azure.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: d773e05a3ed953e5210c0ade3226b4a32e82aeab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182238"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Home page per la programmazione client per Microsoft SQL Server


Benvenuti al nostro home page sul client per interagire con Microsoft SQL Server e Database SQL di Azure nel cloud di programmazione. Questo articolo fornisce le informazioni seguenti:

- Vengono elencate e descritte le combinazioni di lingua e il driver disponibili.
    - Vengono fornite informazioni per i sistemi operativi Windows, MacOS e Linux (Ubuntu e altri).
- Vengono forniti collegamenti alla documentazione dettagliata per ogni combinazione.
- Consente di visualizzare le aree e le aree secondarie della documentazione gerarchica per determinate lingue, laddove appropriato.


#### <a name="azure-sql-database"></a>Database SQL di Azure

In qualsiasi lingua, il codice che si connette a SQL Server è quasi identico al codice per la connessione al Database SQL di Azure.

Per informazioni dettagliate sulle stringhe di connessione per la connessione al Database SQL di Azure, vedere:

- [Usare .NET Core (c#) per eseguire query su un database SQL di Azure](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Gli altri Database SQL di Azure che sono vicine l'articolo precedente della tabella dei contenuti, informazioni sulle altre lingue. Ad esempio, vedere [usare PHP per eseguire query su un database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Pagine Web di un'app compilata

Nostri *un'app compilata* pagine Web vengono illustrati esempi di codice, insieme alle informazioni di configurazione, in un formato alternativo. Per altre informazioni, vedere più avanti in questo articolo il [sezione con etichettata *sito Web di un'app compilata*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Linguaggi e i driver per i programmi client


Nella tabella seguente, ogni immagine language è un collegamento a informazioni dettagliate sull'utilizzo del linguaggio con SQL Server. Ogni collegamento consente di passare a una sezione più avanti in questo articolo.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![Logo di c#][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![Entity Framework ORM, di .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Logo di Java][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Logo di Node. js][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![Logo PHP][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Logo Python][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Logo di Ruby][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Scarica e installa automaticamente

Il seguente articolo è dedicato per il download e installare i driver di connessione SQL diverse, per l'utilizzo dai linguaggi di programmazione:

- [Driver di SQL Server](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![Logo di c#][image-ref-320-csharp] In c# tramite ADO.NET

I linguaggi .NET gestito, quali c# e Visual Basic, sono gli utenti più comuni di ADO.NET. *ADO.NET* è un nome casuale per un subset di classi .NET Framework.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite ADO.NET](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | Un esempio di codice piccoli con stato attivo sulla connessione e l'esecuzione di query SQL Server. |
| [Connettersi in modo resiliente a SQL con ADO.NET](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | Logica di ripetizione tentativi in un esempio di codice, poiché le connessioni in alcuni casi possono verificarsi momenti di perdita di connettività.<br /><br />Per la logica di ripetizione dei tentativi si applica anche alle connessioni gestite tramite internet in qualsiasi database cloud, ad esempio al Database SQL di Azure. |
| [Database SQL di Azure: Dimostrazione di come usare .NET Core su Windows/Linux/macOS per creare un programma c#, connettersi ed eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Esempio di Database SQL di Azure. |
| [Compilazione un'app: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

|||
| :-- | :-- |
| [In c# tramite ADO.NET](./ado-net/index.md)| Radice della nostra documentazione. |
| [Namespace: System. Data](https://docs.microsoft.com/dotnet/api/system.data) | Un set di classi utilizzate per ADO.NET. |
| [Spazio dei nomi: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | Il set di classi che sono più direttamente il centro di ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Logo di Entity Framework][image-ref-333-ef] Entity Framework (EF) con C&#x23;

Entity Framework (EF) fornisce Object-Relational Mapping (ORM). ORM rende più semplice per il codice sorgente di programmazione orientata a oggetti (OOP) modificare i dati recuperati da un database SQL relazionale.

Entity Framework ha relazioni dirette o indirette con le tecnologie seguenti:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), o [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Miglioramenti della sintassi del linguaggio, ad esempio la **=>** operatore nel linguaggio c#.
- Programmi utili che generano codice sorgente per le classi che eseguono il mapping alle tabelle nel database SQL. Ad esempio, [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>Entity Framework originale e nuovo Entity Framework

Il [pagina iniziale per Entity Framework](https://docs.microsoft.com/ef/) introduce Entity Framework con una descrizione simile al seguente:

- Entity Framework è un mapper relazionale a oggetti (O/RM) che consente agli sviluppatori .NET di usare un database con oggetti .NET. Elimina la necessità per la maggior parte del codice sorgente accesso ai dati che gli sviluppatori in genere necessario scrivere.

*Entity Framework* è un nome condiviso da due diramazioni del codice sorgente. Un ramo di Entity Framework è meno recente e il relativo codice sorgente può essere ora gestito da parte del pubblico. L'altro Entity Framework è una novità. I due EFs sono descritte di seguito:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Prima di tutto, Microsoft ha rilasciato EF in agosto 2008. Nel mese di marzo 2015 Microsoft ha annunciato che EF 6.x era la versione finale che Microsoft sviluppa. Microsoft ha rilasciato il codice sorgente nel dominio pubblico.<br /><br />Entity Framework inizialmente faceva parte di .NET Framework. Ma Entity Framework 6.x è stato rimosso da .NET Framework.<br /><br />[Codice di Entity Framework 6.x sorgente su Github nel repository *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft ha rilasciato la concezione di Entity Framework Core a giugno 2016. EF Core è progettato per una migliore flessibilità e portabilità. EF Core eseguibili nei sistemi operativi oltre appena Microsoft Windows. Ed EF Core può interagire con altri database relazionali e database oltre oltre a Microsoft SQL Server.<br /><br />**C&#x23; esempi di codice:**<br />[Introduzione a Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Introduzione a EF Core in .NET Framework con un Database esistente](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

Entity Framework e tecnologie correlate sono potenti e sono molto da imparare per gli sviluppatori che desiderano master l'intera area.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Logo di Java][image-ref-330-java] Java e JDBC

Microsoft offre un driver Java Database Connectivity (JDBC) per l'uso con SQL Server (o con Database SQL di Azure, ovviamente). Si tratta di un driver JDBC di tipo 4 che offre connettività di database tramite le interfacce API (Application Program Interface) JDBC standard.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Esempi di codice](./jdbc/code-samples/index.md) | Esempi di codice che indicano a tipi di dati, set di risultati e dati di grandi dimensioni. |
| [Esempio di URL di connessione](./jdbc/connection-url-sample.md) | Viene descritto come utilizzare un URL di connessione per connettersi a SQL Server. Quindi usarlo per utilizzare un'istruzione SQL per recuperare i dati. |
| [Esempio di origine dati](./jdbc/data-source-sample.md) | Viene descritto come utilizzare un'origine dati per la connessione a SQL Server. Usare quindi una stored procedure per recuperare i dati. |
| [Usare Java per eseguire query su un database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Esempio di Database SQL di Azure. |
| [Creare App Java con SQL Server in Ubuntu](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

La documentazione di JDBC include le aree principali seguenti:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Radice della nostra documentazione JDBC. |
| [Riferimento](./jdbc/reference/index.md) | Le interfacce, classi e membri. |
| [Guida di programmazione per il driver PHP per SQL](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Logo di Node. js][image-ref-340-node] Node.js

Con Node. js è possibile connettersi a SQL Server da Windows, Linux o Mac. È la radice della nostra documentazione di Node. js [qui](./node-js/index.md).

Il driver di connessione di Node. js per SQL Server viene implementato in JavaScript. Il driver Usa il protocollo TDS, supportato da tutte le versioni moderne di SQL Server. Il driver è un progetto open source [disponibile in Github](https://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite Node.js](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Vasta gamma codice sorgente per la connessione a SQL Server ed eseguendo una query. |
| [Database SQL di Azure: usare Node. js per eseguire query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Esempio per il Database SQL di Azure nel cloud. |
| [Creare App Node. js per l'uso di SQL Server in macOS](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>Microsoft ODBC per C++ 

![Logo ODBC][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

(ODBC) Open database connectivity è stato sviluppato nel 1990s e anticipa .NET Framework. ODBC è progettato per essere indipendente da qualsiasi sistema di database specifico e indipendente dal sistema operativo.

Nel corso degli anni numerosi driver ODBC sono stati creati e rilasciati dai gruppi all'interno e all'esterno di Microsoft. L'intervallo dei driver prevedono diversi linguaggi di programmazione client. L'elenco delle destinazioni dei dati va ben oltre SQL Server.

Alcuni altri driver di connettività usano ODBC internamente.

#### <a name="code-example"></a>Esempio di codice

- [Esempio di codice C++ che usa ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Struttura di documentazione

Il contenuto ODBC in questa sezione è incentrata sull'accesso a SQL Server o Database SQL di Azure da C++. La tabella seguente elenca un contorno approssimativo della documentazione principale per ODBC.


| Area | Area secondaria | Descrizione |
| :--- | :------ | :---------- |
| [Microsoft ODBC per C++](./odbc/index.md) | Radice della nostra documentazione. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Informazioni sull'utilizzo di ODBC nei sistemi operativi Linux o MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informazioni sull'utilizzo di ODBC sul sistema operativo Windows. |
| [Amministrazione](../odbc/admin/index.md) | &nbsp; | Lo strumento di amministrazione per la gestione di origini dati ODBC. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Driver ODBC diversi che vengono creati e fornito da Microsoft. |
| [Concettuale e riferimento](../odbc/reference/index.md) | &nbsp; | Informazioni concettuali sull'interfaccia ODBC, oltre a riferimento tradizionale. |
| &nbsp; " | [Appendici](../odbc/reference/appendixes/index.md)    | Tabelle di transizioni di stato, libreria di cursori ODBC e altro ancora. |
| &nbsp; " | [Sviluppare app](../odbc/reference/develop-app/index.md)  | Le funzioni, gli handle e molto altro ancora. |
| &nbsp; " | [Sviluppare driver](../odbc/reference/develop-driver/index.md) | Come sviluppare il proprio driver ODBC, se si dispone di un'origine dati specializzata. |
| &nbsp; " | [Installazione](../odbc/reference/install/index.md) | Installazione di ODBC, sottochiavi e altro ancora. |
| &nbsp; " | [Sintassi](../odbc/reference/syntax/index.md)   | API per il programma di installazione, programma di installazione, la conversione e i dati di accesso. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![Logo PHP][image-ref-360-php] PHP

È possibile usare PHP per interagire con SQL Server. È la radice della nostra documentazione di PHP [qui](./php/index.md).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite PHP](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Un esempio di codice piccoli con stato attivo sulla connessione e l'esecuzione di query SQL Server. |
| [Connettere in modo resiliente a SQL con PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Logica di ripetizione tentativi in un esempio di codice, poiché le connessioni tramite Internet e nel cloud in alcuni casi possono verificarsi momenti di perdita di connettività. |
| [Database SQL di Azure: usare PHP per query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Esempio di Database SQL di Azure. |
| [Creare le app PHP per l'utilizzo di SQL Server in RHEL](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Logo di Python][image-ref-370-python] Python


È possibile usare Python per interagire con SQL Server.

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite Python con pyodbc](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Un esempio di codice piccoli con stato attivo sulla connessione e l'esecuzione di query SQL Server. |
| [Database SQL di Azure: usare Python per query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Esempio di Database SQL di Azure. |
| [Creare le app PHP per l'utilizzo di SQL Server in SLES](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Documentazione

| Area | Descrizione |
| :--- | :---------- |
| [Python per SQL Server](./python/index.md) | Radice della nostra documentazione. |
| [driver pymssql](./python/pymssql/index.md) | Microsoft non mantenere o testare il driver pymssql.<br /><br />Il driver di connessione pymssql è una semplice interfaccia per i database SQL, per l'uso nei programmi di Python. Pymssql si basa su FreeTDS per fornire un'interfaccia di DB-API per Python (PEP-249) a Microsoft SQL Server. |
| [driver pyodbc](./python/pyodbc/index.md)   | Il driver di connessione pyodbc è un modulo Python open source che semplifica l'accesso a database ODBC. Implementa la specifica API DB 2.0, ma è dotato di ragioni di praticità Python. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Logo di Ruby][image-ref-380-ruby] Ruby

È possibile usare Ruby per interagire con SQL Server. È la radice della nostra documentazione Ruby [qui](./ruby/index.md).

#### <a name="code-examples"></a>Esempi di codice

|||
| :-- | :-- |
| [Modello di verifica per la connessione a SQL tramite Ruby](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Un esempio di codice piccoli con stato attivo sulla connessione e l'esecuzione di query SQL Server. |
| [Database SQL di Azure: usare Ruby per query](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Esempio di Database SQL di Azure. |
| [Creare App Ruby per utilizzare SQL Server in MacOS](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informazioni di configurazione, insieme a esempi di codice. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Sito Web di un'app compilata, per lo sviluppo di SQL client](https://www.microsoft.com/sql-server/developer-get-started/)


Nel nostro [ *un'app compilata* ](https://www.microsoft.com/sql-server/developer-get-started/) pagine Web è possibile scegliere tra un lungo elenco di programmazione le lingue per la connessione a SQL Server. E il programma client può eseguire una vasta gamma di sistemi operativi.

*Un'app compilata* privilegia la semplicità e completezza per lo sviluppatore che è appena agli inizi. Vengono descritte le attività seguenti:

1. Come installare Microsoft SQL Server
2. Come scaricare e installare gli strumenti e driver.
3. Esecuzione di tutte le configurazioni necessarie, a seconda del sistema operativo scelto.
4. Come compilare il codice sorgente fornito.
5. Come eseguire il programma.

Successivamente vengono un paio contorni approssimative dei dettagli forniti nel sito Web:

#### <a name="java-on-ubuntu"></a>Java in Ubuntu:

1. Configurare l'ambiente
    - Passaggio 1.1 installare SQL Server
    - Passaggio 1.2 installare Java
    - Passaggio 1.3 installare Java Development Kit (JDK)
    - Passaggio 1.4 installare Maven
2. Creare l'applicazione Java con SQL Server
    - Passaggio 2.1: creazione di un'app Java che si connette a SQL Server ed esegue query
    - Passaggio 2.2: creazione di un'app Java che si connette a SQL Server usando il framework più diffusi di ibernazione
3. Rendere l'app Java fino a 100 volte più veloce
    - Passaggio 3.1: creazione di un'app Java per illustrare gli indici Columnstore

#### <a name="python-on-windows"></a>Python in Windows:

1. Configurare l'ambiente
    - Passaggio 1.1 installare SQL Server
    - Passaggio 1.2 installare Python
    - Passaggio 1.3 installare il Driver ODBC e utilità della riga di comando SQL per SQL Server
2. Creare l'applicazione Python con SQL Server
    - Passaggio 2.1 installare il driver Python per SQL Server
    - Passaggio 2.2: creazione di un database per l'applicazione
    - Passaggio 2.3: creazione di un'app Python che si connette a SQL Server ed esegue query
3. Rendere l'app Python fino a 100 volte più veloce
    - Passaggio 3.1: creazione di una nuova tabella con 5 milioni di utilizzo di sqlcmd
    - Passaggio 3.2: creazione di un'app Python che esegue una query in questa tabella e misura il tempo impiegato
    - Passaggio 3.3 misurare il tempo necessario per eseguire la query
    - Passaggio 3.4 aggiungere un indice columnstore nella tabella
    - Passaggio 3.5 misurare il tempo necessario per eseguire la query con un indice columnstore

Gli screenshot seguenti dare un'idea di come appare il nostro sito Web documentazione di sviluppo SQL.

#### <a name="choose-a-language"></a>Scegliere una lingua:

![Sito Web di sviluppo SQL, introduzione][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Scegliere un sistema operativo:

![Sito Web di sviluppo SQL Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Altro tipo di sviluppo


In questa sezione vengono forniti collegamenti sulle altre opzioni di sviluppo. Questi includono l'uso di queste stesse lingue per lo sviluppo di Azure in generale. Le informazioni va oltre la destinazione è semplicemente il Database SQL di Azure e Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Hub per sviluppatori per Azure

- [Hub per sviluppatori per Azure](https://docs.microsoft.com/azure/)
- [Azure per sviluppatori .NET](https://docs.microsoft.com/dotnet/azure/)
- [Azure per sviluppatori Java](https://docs.microsoft.com/java/azure/)
- [Azure per sviluppatori Node. js](https://docs.microsoft.com/nodejs/azure/)
- [Azure per sviluppatori Python](https://docs.microsoft.com/python/azure/)
- [Creare un'app web PHP in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Altri linguaggi

- [Creare le app Go con SQL Server in Windows](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

