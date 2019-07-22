---
title: Connessione e recupero di dati | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7e642879c095dd4d9dca4f51a936ab72c523e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956880"
---
# <a name="connecting-and-retrieving-data"></a>Connessione e recupero dei dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando si utilizza [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], sono disponibili due metodi principali per stabilire una connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il primo metodo consente di impostare le proprietà di connessione nell'URL della connessione, quindi di chiamare il metodo getConnection della classe DriverManager per restituire un oggetto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
> Per un elenco delle proprietà di connessione supportate dal driver JDBC, vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
Il secondo metodo consente di impostare le proprietà di connessione mediante i metodi setter della classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) e quindi di chiamare il metodo [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) per restituire un oggetto SQLServerConnection.  
  
Gli argomenti in questa sezione descrivono le diverse modalità di connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e vengono inoltre illustrate le diverse tecniche per il recupero dei dati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                | Descrizione                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Esempio di URL di connessione](../../connect/jdbc/connection-url-sample.md) | Viene descritto come usare un URL di connessione per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi usare un'istruzione SQL per il recupero dei dati. |
| [Esempio di origine dati](../../connect/jdbc/data-source-sample.md)       | Viene descritto come utilizzare un'origine dati per connettersi a SQL Server e quindi utilizzare una stored procedure per il recupero dei dati.                                                 |
  
## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
