---
description: Profilatura delle prestazioni del driver ODBC (ODBC)
title: Profiling delle prestazioni del driver ODBC
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09c5dff41c7865f02c508acbbf718b81cafa932a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469532"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>Profilatura delle prestazioni del driver ODBC (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Sono disponibili due opzioni specifiche che possono essere utilizzate dal driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'analisi delle prestazioni del driver.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può registrare statistiche sulle prestazioni nei file. Il file di log delle statistiche è un file delimitato da tabulazioni che può essere analizzato in qualsiasi foglio di calcolo in grado di supportare i file delimitati da tabulazioni, come Microsoft Excel.  
  
 Il driver può registrare anche query con esecuzione prolungata (query che non ottengono una risposta dal server entro un periodo di tempo specificato). Tali query possono essere analizzate in un secondo momento da programmatori e amministratori del database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Dati sulle prestazioni del driver del profilo &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [Query di log Long-Running &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per l'utilizzo di ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
