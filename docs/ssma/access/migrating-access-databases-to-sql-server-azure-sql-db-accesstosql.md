---
title: Eseguire la migrazione dei database di Access a SQL Server-database SQL di Azure | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 959af9bcb1879dc19d2bfb99253b4c40d637fd1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68260241"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrazione dei database di Access a SQL Server-database SQL di Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) è uno strumento che fornisce un ambiente completo che consente di eseguire rapidamente la migrazione dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a o SQL Azure. Utilizzando SSMA, è possibile esaminare l'accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure oggetti di database, valutare il database di Access per la migrazione, convertire gli oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di Access, caricarli in o SQL Azure, quindi migrare i dati.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per eseguire la migrazione degli oggetti e dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dall'accesso a o SQL Azure, utilizzare il processo seguente:  
  
1.  [Creare un nuovo progetto SSMA](creating-and-managing-projects-accesstosql.md). Dopo aver creato il progetto, è possibile [impostare le opzioni del progetto](setting-conversion-and-migration-options-accesstosql.md), incluse le opzioni di conversione, le opzioni di migrazione e i mapping dei tipi di dati.  
  
2.  [Aggiungere i file di database di Access](adding-and-removing-access-database-files-accesstosql.md) al progetto.  
  
    È possibile aggiungere singoli file, inclusi i file presenti nel computer o nella rete.  
  
3.  [Connettersi all'istanza di destinazione di SQL Server](connecting-to-sql-server-accesstosql.md) o [connettersi all'istanza di destinazione di SQL Azure](connecting-to-azure-sql-db-accesstosql.md).  
  
    È possibile connettersi a SQL Server o SQL Azure.  
  
4.  Per personalizzare il mapping tra uno o più database di Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o SQL Azure schemi, [eseguire il mapping dei database di origine e di destinazione](mapping-source-and-target-databases-accesstosql.md).  
  
5.  Facoltativamente, è possibile [creare un report di valutazione](assessing-access-database-objects-for-conversion-accesstosql.md) per determinare se gli oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access possono essere convertiti o SQL Azure correttamente.  
  
6.  [Converte gli oggetti](converting-access-database-objects-accesstosql.md) di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di Access in o SQL Azure le definizioni degli oggetti.  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
    È possibile caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure tramite SSMA oppure è possibile salvare [!INCLUDE[tsql](../../includes/tsql-md.md)] gli script.  
  
8.  [Eseguire la migrazione dei dati di accesso in SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > È possibile convertire, caricare ed eseguire la migrazione di schemi e dati in un unico passaggio. Per eseguire una migrazione con un clic, fare clic sul pulsante **Converti, carica ed Esegui migrazione** .  
  
9. Se si desidera che le applicazioni di accesso utilizzino i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati in o SQL Azure, utilizzare [collegare le tabelle di accesso alle tabelle di SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
Per eseguire questa procedura, è inoltre possibile utilizzare la migrazione guidata. Per ulteriori informazioni, vedere [migrazione guidata](migration-wizard-accesstosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione con SQL Server Migration Assistant per l'accesso](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)
