---
title: Librerie di connessione per i database Microsoft SQL | Microsoft Docs
description: Fornisce collegamenti di download per i moduli che consentono la connessione a Microsoft SQL Server e al database SQL di Azure, da un'ampia gamma di linguaggi di programmazione client.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632810"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Moduli di connessione per i database Microsoft SQL

Questo articolo fornisce collegamenti di download ai moduli di connessione o ai *driver* che i programmi client possono usare per interagire con [Microsoft SQL Server](../relational-databases/database-features.md)e con il suo gemello nel [database SQL di Azure](https://docs.microsoft.com/azure/sql-database/)cloud. I driver sono disponibili per un'ampia gamma di linguaggi di programmazione, in esecuzione nei sistemi operativi seguenti:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Mancata corrispondenza da OOP a relazionale

*Relazionali*: i programmi client scritti in un linguaggio di programmazione orientata a oggetti utilizzano spesso driver SQL che restituiscono dati sottoposti a query in un formato più relazionale rispetto a quello orientato agli oggetti. C#l'uso di ADO.NET è un esempio. La mancata corrispondenza del formato relazionale OOP a volte rende più difficile la scrittura e la comprensione del codice OOP.

*ORM*: altri driver o Framework restituiscono dati sottoposti a query nel formato OOP, evitando la mancata corrispondenza. Questi driver funzionano prevedendo che le classi siano state definite in modo da corrispondere alle colonne di dati di determinate tabelle SQL. Il driver esegue quindi il *mapping relazionale a oggetti* (ORM) per restituire i dati sottoposti a query come istanza di una classe. Gli Entity Framework Microsoft (EF) per C#e Hibernate per Java sono due esempi.

Il presente articolo dedica sezioni separate a questi due tipi di driver di connessione.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Driver per l'accesso relazionale


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Linguaggio | Scaricare il driver SQL |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core, per Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, per MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET Core, per Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Driver node. js, istruzioni di installazione](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, istruzioni di installazione](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Scarica ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Driver Ruby, istruzioni di installazione](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Pagina di download di Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Driver per l'accesso ORM


Nella tabella seguente sono elencati esempi di framework ORM (Object Relational Mapping) usati dalle applicazioni client per la connessione ai database Microsoft SQL.


| Linguaggio | Download driver ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6. x o versione successiva)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [ORM eloquente, incluso nell'installazione di Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Pagine Web di compilazione-app
[https://aka.ms/sqldev](https://aka.ms/sqldev) porta a un set di pagine Web di *compilazione-app* . Le pagine Web forniscono informazioni su numerose combinazioni di linguaggio di programmazione, sistema operativo e driver di connessione SQL. Tra le informazioni fornite dalle pagine web Build-an-app sono disponibili gli elementi seguenti:

- Informazioni dettagliate su come iniziare fin dall'inizio, per ogni combinazione di linguaggio + sistema operativo + driver.
    - Istruzioni per l'installazione dei driver di connessione SQL più recenti.
- Esempi di codice per ognuno degli elementi seguenti:
    - Esempi di codice relazionale a oggetti.
    - Esempi di codice ORM.
    - Dimostrazioni sugli indici columnstore per ottenere prestazioni molto più veloci.

#### <a name="first-page-of-build-an-app-webpages"></a>Prima pagina, di pagine Web di compilazione-a-app
![Pagine Web di compilazione-app, schermata iniziale][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menu per Java-Ubuntu, di pagine Web di compilazione-a-app
![Pagine Web di compilazione-app, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Collegamenti correlati
- [Esempi di codice per la connessione al database SQL di Azure nel cloud con Java e altri linguaggi](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
