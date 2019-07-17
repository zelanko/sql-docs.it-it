---
title: Eseguire la migrazione di database di Access a SQL Server - database SQL di Azure | Microsoft Docs
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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260241"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrazione dei database di Access a SQL Server - database SQL di Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) è uno strumento che fornisce un ambiente completo che consente di rapidamente la migrazione di database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Tramite SSMA, è possibile verificare l'accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure gli oggetti di database, valutare il database di Access per la migrazione, convertire gli oggetti di database di Access, caricarli in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, quindi eseguire la migrazione dei dati.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per eseguire la migrazione oggetti e dati da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, procedere come segue:  
  
1.  [Creare un nuovo progetto SSMA](creating-and-managing-projects-accesstosql.md). Dopo aver creato il progetto, è possibile [impostare le opzioni del progetto](setting-conversion-and-migration-options-accesstosql.md), tra cui opzioni di conversione, le opzioni di migrazione e mapping dei tipi di dati.  
  
2.  [Aggiungere i file di database di Access](adding-and-removing-access-database-files-accesstosql.md) al progetto.  
  
    È possibile aggiungere singoli file, inclusi quelli che trova nel computer o rete.  
  
3.  [Connetti all'istanza di destinazione di SQL Server](connecting-to-sql-server-accesstosql.md) oppure [Connetti all'istanza di destinazione di SQL Azure](connecting-to-azure-sql-db-accesstosql.md).  
  
    È possibile connettersi a SQL Server o SQL Azure.  
  
4.  Per personalizzare il mapping tra uno o più database di Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi di SQL Azure, o [eseguire il mapping di database di origine e destinazione](mapping-source-and-target-databases-accesstosql.md).  
  
5.  Facoltativamente, è possibile [creare un report di valutazione](assessing-access-database-objects-for-conversion-accesstosql.md) per determinare se gli oggetti di database di Access possono essere convertiti correttamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
6.  [Convertire gli oggetti di database di Access](converting-access-database-objects-accesstosql.md) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o le definizioni degli oggetti di SQL Azure.  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
    È possibile caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure tramite SSMA, oppure è possibile salvare [!INCLUDE[tsql](../../includes/tsql-md.md)] script.  
  
8.  [Eseguire la migrazione di accesso ai dati in SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > È possibile convertire, caricare e la migrazione di schemi e dati in un unico passaggio. Per eseguire la migrazione di un solo clic, scegliere il **convertire, caricare ed eseguire la migrazione** pulsante.  
  
9. Se si desidera che le applicazioni di accesso per utilizzare i dati nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, usare [collegare le tabelle di accesso alle tabelle di SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
È inoltre possibile utilizzare la migrazione guidata per illustrano in dettaglio questo processo. Per altre informazioni, vedere [migrazione guidata](migration-wizard-accesstosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione a SQL Server Migration Assistant per Access](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)
