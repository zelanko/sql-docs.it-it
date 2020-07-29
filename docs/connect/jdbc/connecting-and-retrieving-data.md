---
title: Connessione e recupero dei dati
description: Informazioni su come connettersi a un database SQL e recuperare dati usando Microsoft JDBC Driver per SQL Server e questi esempi di codice.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92565d42605b67f61d3ab5e3842e3fb9f110b626
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922887"
---
# <a name="connecting-and-retrieving-data"></a>Connessione e recupero dei dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si utilizza [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], sono disponibili due metodi principali per stabilire una connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il primo metodo consente di impostare le proprietà di connessione nell'URL della connessione, quindi di chiamare il metodo getConnection della classe DriverManager per restituire un oggetto [SQLServerConnection](reference/sqlserverconnection-class.md).

> [!NOTE]
> Per un elenco delle proprietà di connessione supportate dal driver JDBC, vedere [Impostazione delle proprietà delle connessioni](setting-the-connection-properties.md).

Il secondo metodo consente di impostare le proprietà di connessione mediante i metodi setter della classe [SQLServerDataSource](reference/sqlserverdatasource-class.md) e quindi di chiamare il metodo [getConnection](reference/getconnection-method-sqlserverdatasource.md) per restituire un oggetto SQLServerConnection.

Gli argomenti in questa sezione descrivono le diverse modalità di connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e vengono inoltre illustrate le diverse tecniche per il recupero dei dati.

## <a name="in-this-section"></a>Contenuto della sezione

| Argomento                                             | Descrizione                                                                                                                                                   |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Esempio di URL di connessione](connection-url-sample.md) | Viene descritto come usare un URL di connessione per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi usare un'istruzione SQL per il recupero dei dati. |
| [Esempio di origine dati](data-source-sample.md)       | Viene descritto come utilizzare un'origine dati per connettersi a SQL Server e quindi utilizzare una stored procedure per il recupero dei dati.                                                 |

## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](sample-jdbc-driver-applications.md)
