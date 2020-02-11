---
title: Eseguire la migrazione dei database Sybase ASE a SQL Server-database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3735e03e3196f899ab33ca152364244e3331ac5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028853"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrazione dei database SAP ASE a SQL Server-database SQL di Azure (SybaseToSQL)
SQL Server Migration Assistant (SSMA) per SAP Adaptive Server Enterprise (ASE) è un ambiente completo che consente di eseguire rapidamente la migrazione dei database SAP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE a o al database SQL di Azure. Con SSMA per SAP ASE è possibile esaminare gli oggetti e i dati di database, valutare i database per la migrazione, eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la migrazione di oggetti di database al database SQL di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure e quindi migrare i dati in un database SQL di Azure o.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per eseguire correttamente la migrazione di oggetti e dati dai database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SAP ASE a o al database SQL di Azure, usare il processo seguente:  
  
1.  [Creare un nuovo progetto SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Dopo aver creato il progetto, è possibile impostare le opzioni di conversione del progetto, migrazione e mapping dei tipi. Per informazioni sulle impostazioni del progetto, vedere [impostazione delle opzioni del progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Per informazioni sulla personalizzazione dei mapping dei tipi di dati, vedere [mapping dei tipi di dati di Sybase ASE e SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Connettersi al server di database SAP ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Connettersi a un'istanza SQL Server](connecting-to-sql-server-sybasetosql.md) o [connettersi a un'istanza del database SQL di Azure](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Eseguire il mapping degli schemi di database SAP ASE a SQL Server/schemi di database di database SQL di Azure](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Facoltativamente, [creare rapporti di valutazione](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) per valutare gli oggetti di database per la conversione e stimare il tempo di conversione.  
  
6.  [Convertire gli schemi di database SAP ASE in SQL Server/schemi del database SQL di Azure](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server/database SQL di Azure](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Salvare uno script ed eseguirlo in o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database SQL di Azure oppure sincronizzare gli oggetti di database.  
  
8.  [Eseguire la migrazione dei dati a SQL Server/database SQL di Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessario, aggiornare le applicazioni di database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introduzione con SSMA per SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
