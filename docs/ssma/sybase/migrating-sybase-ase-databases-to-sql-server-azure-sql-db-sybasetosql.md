---
title: La migrazione dei database di Sybase ASE a SQL Server - database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 96ade7125c0d03963e8e012ed72bdb8fdef492cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705470"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>La migrazione dei database di SAP ASE a SQL Server - Database SQL di Azure (SybaseToSQL)
SQL Server Migration Assistant (SSMA) per SAP Adaptive Server Enterprise (ASE) è un ambiente completo che consente di rapidamente la migrazione dei database SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Tramite SSMA per ASE SAP, è possibile esaminare gli oggetti di database e i dati, valutare i database per la migrazione, eseguire la migrazione di oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure e quindi eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per completare la migrazione oggetti e i dati dal database SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure, procedere come segue:  
  
1.  [Creare un nuovo progetto SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Dopo aver creato il progetto, è possibile impostare conversione del progetto, la migrazione e le opzioni di mapping dei tipi. Per informazioni sulle impostazioni del progetto, vedere [impostazione delle opzioni progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Per informazioni sulla personalizzazione dei mapping dei tipi di dati, vedere [Mapping di Sybase ASE e SQL Server Data Types &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Connettersi al server di database SAP ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Connettersi a un'istanza di SQL Server](connecting-to-sql-server-sybasetosql.md) oppure [Connetti a un'istanza di Database SQL di Azure](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Eseguire il mapping di schemi di database SAP ASE a SQL Server / Database SQL di Azure degli schemi di database](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Facoltativamente [creazione di report di valutazione](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) per valutare gli oggetti di database per la conversione e stimare il tempo di conversione.  
  
6.  [Convertire gli schemi del database SAP ASE in SQL Server / schemi di Database SQL di Azure](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server / Database SQL di Azure](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Uno salvare uno script ed eseguirlo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure o sincronizzare gli oggetti di database.  
  
8.  [La migrazione dei dati a SQL Server / Database SQL di Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessario, aggiornare le applicazioni del database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introduzione a SSMA per ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
