---
title: Sviluppare applicazioni usando Always Encrypted | Microsoft Docs
description: Informazioni sulla tecnologia lato client Always Encrypted che assicura che i dati riservati non vengano mai rivelati a SQL Server o al database SQL di Azure.
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f348cf050941a06b2e0be6c37993a7f7458cb6a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627566"
---
# <a name="develop-applications-using-always-encrypted"></a>Sviluppare applicazioni usando Always Encrypted
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) è una tecnologia di crittografia lato client che assicura che i dati riservati e le chiavi di crittografia associate non vengano mai rivelati a SQL Server o al database SQL di Azure. Con Always Encrypted, un driver client crittografa in modo trasparente i dati sensibili prima di passarli al motore di database e decrittografa in modo trasparente i dati recuperati da colonne di database crittografate.

Per informazioni dettagliate sullo sviluppo di applicazioni che usano database protetti da Always Encrypted e sui driver client e sulle versioni dei driver che supportano Always Encrypted, vedere:

- [Using Always Encrypted with .NET Framework Data Provider for SQL Server (Uso di Always Encrypted con il provider di dati .NET Framework per SQL Server)](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Utilizzo di Always Encrypted con il JDBC Driver](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [Using Always Encrypted with the ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Utilizzo di Always Encrypted con il driver ODBC)
- [Usare Always Encrypted con i driver PHP](../../../connect/php/using-always-encrypted-php-drivers.md)
- [Uso di Always Encrypted con il provider di dati Microsoft .NET per SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
