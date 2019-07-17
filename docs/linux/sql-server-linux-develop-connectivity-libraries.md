---
title: Framework e librerie di connettività
description: Elenca i driver di connettività che le app client possono usare da vari linguaggi per connettersi a Microsoft SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker e anche al Database SQL di Azure e Azure SQL Data Warehouse.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: dd2a70cefd0e094b53656dde99af81afca2894c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077463"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Librerie di connettività e Framework per Microsoft SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Consultare il [esercitazioni introduttive](https://aka.ms/sqldev) rapidamente iniziare a usare con linguaggi di programmazione quali c#, Java, Node. js, PHP e Python e creare un'app con SQL Server in Linux o Windows o Docker su macOS.

La tabella seguente elenca le librerie di connettività o *driver* che le applicazioni client possono usare da un'ampia gamma di linguaggi per connettersi e usare Microsoft SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker e anche il Database SQL di Azure e Azure SQL Data Warehouse. 

| Linguaggio | Piattaforma | Risorse aggiuntive | Scarica | Introduzione |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](https://msdn.microsoft.com/library/mt657768.aspx) | [Scarica](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver per SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [Scarica](https://go.microsoft.com/fwlink/?LinkId=245496) |  [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Driver SQL PHP per SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | Sistema operativo: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Driver Node.js per SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Driver SQL Python](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Driver Ruby per SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introduzione](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver per SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [Scarica](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

Nella tabella seguente elenca alcuni esempi di Framework ORM Object Relational Mapping () e i framework web utilizzabili dalle applicazioni client con Microsoft SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker e anche al Database SQL di Azure e Azure SQL Data Warehouse. 

| Linguaggio | Piattaforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Stato di ibernazione ORM](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (intuitivo)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>Collegamenti correlati
- [Driver di SQL Server](https://msdn.microsoft.com/library/mt654049.aspx) per la connessione dalle applicazioni client
