---
title: Raccolte di connessioni per database Microsoft SQL | Microsoft Docs
description: Indica collegamenti per il download di moduli che consentono la connessione a Microsoft SQL Server e a database SQL di Azure da una gamma di linguaggi di programmazione client.
author: RothJa
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 03/05/2020
ms.author: JRoth
ms.openlocfilehash: eb842769490b521b248ed4114953b8d828fa80d3
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866407"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Moduli di connessione per i database Microsoft SQL

Questo articolo offre i collegamenti per il download di moduli di connessione o *driver* che i programmi client possono usare per interagire con [Microsoft SQL Server](../relational-databases/database-features.md) e con il suo gemello nel cloud, il [database SQL di Azure](https://docs.microsoft.com/azure/sql-database/). I driver sono disponibili per un'ampia gamma di linguaggi di programmazione, in esecuzione nei sistemi operativi seguenti:

- Linux
- MacOS
- Windows

**Mancata corrispondenza OOP-relazionale:**

*Relazionale*: I programmi client scritti in un linguaggio di programmazione orientata a oggetti (OOP) usano spesso driver SQL che restituiscono i dati sottoposti a query in un formato più relazionale che orientato a oggetti. L'uso di ADO.NET in C# è un esempio. La mancata corrispondenza di formato tra relazionale e OOP a volte rende più difficile la scrittura e la comprensione del codice OOP.

*ORM*: Altri driver o framework restituiscono i dati sottoposti a query nel formato OOP, evitando la mancata corrispondenza. Questi driver funzionano in base al presupposto che le classi siano state definite in modo da corrispondere alle colonne di dati di determinate tabelle SQL. Il driver esegue quindi il *mapping relazionale a oggetti* (ORM) per restituire i dati sottoposti a query come istanza di una classe. Entity Framework (EF) di Microsoft per C# e Hibernate per Java sono due esempi.

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
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core per: Linux-Ubuntu, macOS, Windows](https://dotnet.microsoft.com/download) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Driver Node.js, istruzioni di installazione](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, istruzioni di installazione](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Scaricare ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Driver Ruby, istruzioni di installazione](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Pagina di download di Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br/> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Driver per l'accesso ORM

Nella tabella seguente sono elencati esempi di framework ORM (Object Relational Mapping) usati dalle applicazioni client per la connessione ai database Microsoft SQL.

| Linguaggio | Download del driver ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x o versione successiva)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM, incluso nell'installazione di Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |
| &nbsp; | <br/> |

<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Pagine Web di compilazione app
**[https://aka.ms/sqldev](https://aka.ms/sqldev)** consente di accedere a una serie di pagine Web *di compilazione app*. Le pagine Web offrono informazioni su numerose combinazioni di linguaggio di programmazione, sistema operativo e driver di connessione SQL. Tra le informazioni contenute nelle pagine Web di compilazione app sono disponibili gli elementi seguenti:

- Informazioni dettagliate su come procedere fin dall'inizio, per ogni combinazione di linguaggio + sistema operativo + driver.
    - Istruzioni per l'installazione dei driver di connessione SQL più recenti.
- Esempi di codice per ognuno degli elementi seguenti:
    - Esempi di codice relazionale a oggetti.
    - Esempi di codice ORM.
    - Dimostrazioni di indice columnstore per ottenere prestazioni molto più veloci.

**Pagine Web di compilazione app, prima pagina:**  
![Pagine Web di compilazione app, screenshot prima pagina](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png)

**Menu per Java - Ubuntu, pagine Web di compilazione app**  
![Pagine Web di compilazione app, menu Java Ubuntu](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png)

&nbsp;

## <a name="related-links"></a>Collegamenti correlati
- [Esempi di codice per la connessione al database SQL di Azure nel cloud con Java e altri linguaggi](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!--
Image references, **obsolete** markdown syntax alternative:

![Build-an-app webpages, first page screenshot][image-ref-163-buildanapp-webpages-first-page]
![Build-an-app webpages, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
-->
