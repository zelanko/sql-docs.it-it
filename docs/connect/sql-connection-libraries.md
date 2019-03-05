---
title: Raccolte connessioni per database di Microsoft SQL | Microsoft Docs
description: Fornisce i collegamenti ai download per i moduli che consentono la connessione a Microsoft SQL Server e Database SQL di Azure da un'ampia gamma di linguaggi di programmazione client.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 7f759dbe9022cff557461d900a35b3ccc91d2c4b
ms.sourcegitcommit: 0f452eca5cf0be621ded80fb105ba7e8df7ac528
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007574"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Moduli di connessione per i database SQL di Microsoft

Questo articolo fornisce i collegamenti ai download per i moduli di connessione oppure *driver* che i programmi client possono utilizzare per l'interazione con [Microsoft SQL Server](../relational-databases/database-features.md)e con il dispositivo gemello nel cloud [Azure Database SQL](https://docs.microsoft.com/azure/sql-database/). I driver sono disponibili per un'ampia gamma di linguaggi di programmazione, in esecuzione su sistemi operativi seguenti:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Mancata corrispondenza OOP-relazionale

*Relazionale*: usare nei programmi Client che vengono scritti in un linguaggio (OOP) programmazione orientata agli oggetti spesso i driver SQL che restituiscono dati sottoposti a query in un formato più relazionale più orientate a oggetti. Codice c# che utilizza ADO.NET è un esempio. La mancata corrispondenza tra formato relazionale OOP talvolta rende il codice OOP più difficili da scrivere e capire.

*ORM*: altri driver o un framework di restituiscono dati sottoposti a query nel formato OOP, evitando la mancata corrispondenza. Questi driver lavorare è previsto che le classi sono state definite in modo da corrispondere le colonne di dati delle tabelle SQL specifiche. Il driver esegue quindi il *mapping relazionale a oggetti* (ORM) per restituire dati sottoposti a query come un'istanza di una classe. Entity Framework (EF di Microsoft) per c# e ibernazione per Java, sono riportati due esempi.

Il presente articolo dedica sezioni separate per questi due tipi di driver di connessione.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Driver per un accesso relazionale


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
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[.NET core per Ubuntu Linux](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET core, per MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET core, per Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Driver Node. js, istruzioni di installazione](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, istruzioni di installazione](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Scaricare ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Driver Ruby, istruzioni di installazione](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Pagina di download Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Driver per l'accesso ORM


La tabella seguente elenca esempi di Framework ORM Object Relational Mapping () usata dalle applicazioni client per connettersi al database SQL di Microsoft.


| Linguaggio | Download del driver ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x o versione successiva)](https://docs.microsoft.com/ef/) |
| Java | [Stato di ibernazione ORM](https://hibernate.org/orm)|
| PHP | [ORM intuitivo, inclusa in installazione di Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Pagine Web di un'app compilata
[https://aka.ms/sqldev](https://aka.ms/sqldev) Consente di visualizzare un set di *un'app compilata* pagine Web. Le pagine Web forniscono informazioni sulle diverse combinazioni di linguaggio di programmazione, sistema operativo e i driver di connessione SQL. Tra le informazioni fornite da un'app compilata pagine Web sono gli elementi seguenti:

- Informazioni dettagliate su come iniziare a utilizzare sin dall'inizio, per ogni combinazione di lingua del sistema operativo + driver.
    - Istruzioni per installare i driver di connessione SQL più recenti.
- Esempi di codice per ognuno degli elementi seguenti:
    - Esempi di codice relazionale a oggetti.
    - Esempi di codice ORM.
    - Dimostrazioni di indice ColumnStore per ottenere migliori prestazioni.

#### <a name="first-page-of-build-an-app-webpages"></a>Prima pagina, delle pagine Web di un'app compilata
![Pagine Web di un'app compilata, prima schermata della pagina][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menu per Java - Ubuntu, delle pagine Web di un'app compilata
![Pagine Web di un'app compilata, menu Ubuntu Java][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Collegamenti correlati
- [Esempi di codice per la connessione al Database SQL di Azure nel cloud, con Java e altri linguaggi](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
