---
title: La migrazione da Oracle database in SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 9e746d1df201349011d24fc0de007c74ba0073b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209797"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migrazione di database Oracle a SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per Oracle è un ambiente completo che consente di eseguire rapidamente la migrazione di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], database SQL di Azure o Azure SQL Data Warehouse. Tramite SSMA per Oracle, è possibile esaminare gli oggetti di database e i dati, valutare i database per la migrazione, eseguire la migrazione di oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], database SQL di Azure o Azure SQL Data Warehouse, quindi eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], database SQL di Azure o Azure SQL Data Data warehouse. Si noti che è possibile eseguire la migrazione di schemi SYS e di sistema Oracle.
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per completare la migrazione oggetti e i dati dal database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], database SQL di Azure o Azure SQL Data Warehouse, usare la procedura seguente:
  
1.  [Creare un nuovo progetto SSMA](working-with-ssma-projects-oracletosql.md).  
  
    Dopo aver creato il progetto, è possibile impostare conversione del progetto, la migrazione e le opzioni di mapping dei tipi. Per informazioni sulle impostazioni del progetto, vedere [impostazione delle opzioni progetto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Per informazioni su come personalizzare i mapping dei tipi di dati, vedere [Mapping di Oracle e SQL Server Data Types &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Connettersi al server di database Oracle](connecting-to-oracle-database-oracletosql.md).  
  
3.  [Connettersi a un'istanza di SQL Server](connecting-to-sql-server-oracletosql.md).  
  
4.  [Eseguire il mapping degli schemi di database Oracle a schemi di database di SQL Server](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
5.  Facoltativamente [creazione di report di valutazione](assessing-oracle-schemas-for-conversion-oracletosql.md) per valutare gli oggetti di database per la conversione e stimare il tempo di conversione.  
  
6.  [Convertire gli schemi del database Oracle in schemi di SQL Server](converting-oracle-schemas-oracletosql.md).  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
    È possibile eseguire questa operazione in uno dei modi seguenti:  
  
    -   Salvare uno script ed eseguirlo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronizzare gli oggetti di database.  
  
8.  [La migrazione dei dati a SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
9. Se necessario, aggiornare le applicazioni di database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introduzione a SSMA per Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
