---
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 31329a2612e4744badcbe9605c22af4761e51cfe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783280"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>Profilatura delle prestazioni del driver ODBC (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Sono disponibili due opzioni specifiche che possono essere utilizzate dal driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'analisi delle prestazioni del driver.  
  
 Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può registrare statistiche sulle prestazioni nei file. Il file di log delle statistiche è un file delimitato da tabulazioni che può essere analizzato in qualsiasi foglio di calcolo in grado di supportare i file delimitati da tabulazioni, come Microsoft Excel.  
  
 Il driver può registrare anche query con esecuzione prolungata (query che non ottengono una risposta dal server entro un periodo di tempo specificato). Tali query possono essere analizzate in un secondo momento da programmatori e amministratori del database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Dati sulle prestazioni del driver del profilo &#40;&#41;ODBC](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [Registrare query con esecuzione prolungata &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per l'utilizzo di ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
