---
title: La migrazione dei dati di accesso a SQL Server - Azure SQL database (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d15d7608879d9116832e083654cc07717c72e23e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453489"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>La migrazione dei dati di accesso a SQL Server - Azure SQL database (AccessToSQL)
Dopo avere creato gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile migrare i dati da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
## <a name="setting-migration-options"></a>Impostazione delle opzioni di migrazione  
Prima della migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, esaminare le opzioni di migrazione del progetto nella **impostazioni di progetto** nella finestra di dialogo. Nella finestra di dialogo, è possibile impostare la dimensione del batch di migrazione, blocco di tabella, vincolo controllo, i trigger di inserimento generazione, identità e il valore null, la gestione e su come gestire date fuori il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervallo. Per altre informazioni, vedere [impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>La migrazione dei dati  
Eseguire la migrazione dei dati sono un'operazione di caricamento bulk che sposta le righe di dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure nelle transazioni. Il numero di righe da caricare nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure in ogni transazione è configurato nelle impostazioni del progetto.  
  
Per visualizzare i messaggi di migrazione, verificare che il riquadro di Output è visibile. Se non lo è, nel **View** dal menu **Output**.  
  
**Per eseguire la migrazione dei dati**  
  
1.  Assicurarsi che sono stati caricati gli oggetti di database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
2.  Nel Visualizzatore metadati di accesso, selezionare gli oggetti che contengono i dati che si desidera eseguire la migrazione:  
  
    -   Per eseguire la migrazione dei dati per un intero database, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per eseguire la migrazione dei dati da singole tabelle, espandere il database, espandere **tabelle**e quindi selezionare la casella di controllo accanto alla tabella. Per omettere i dati da singole tabelle, deselezionare la casella di controllo.  
  
3.  Fare doppio clic su **database** e quindi selezionare **Migrate Data**.  
  
È anche possibile eseguire la migrazione dei dati all'esterno di SSMA usando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** utilità della riga di comando o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Per altre informazioni su questi strumenti, vedere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="next-step"></a>Passaggio successivo  
Se si dispone di accedere alle applicazioni di database che si desidera continuare a usare dopo la migrazione, collegare le tabelle di database di Access per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure. Per altre informazioni, vedere [collegamento di accesso alle applicazioni di SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Impostazione conversione e le opzioni di migrazione](setting-conversion-and-migration-options-accesstosql.md)  
  
