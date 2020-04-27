---
title: Migrazione dei dati di accesso in SQL Server-database SQL di Azure (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907139"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migrazione dei dati di accesso in SQL Server-database SQL di Azure (AccessToSQL)
Una volta creati correttamente gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile eseguire la migrazione dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Access a o SQL Azure.  
  
## <a name="setting-migration-options"></a>Impostazione delle opzioni di migrazione  
Prima di eseguire la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei dati in o SQL Azure, esaminare le opzioni di migrazione del progetto nella finestra di dialogo **Impostazioni progetto** . In questa finestra di dialogo è possibile impostare le dimensioni del batch di migrazione, il blocco della tabella, il controllo dei vincoli, l'attivazione del trigger di inserimento, la gestione delle identità e dei valori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] null e la modalità di gestione delle date non comprese nell'intervallo. Per ulteriori informazioni, vedere [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migrazione dei dati  
La migrazione dei dati è un'operazione di caricamento bulk che consente di spostare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] righe di dati in o SQL Azure nelle transazioni. Il numero di righe da caricare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure in ogni transazione viene configurato nelle impostazioni del progetto.  
  
Per visualizzare i messaggi di migrazione, verificare che il riquadro di output sia visibile. In caso contrario, scegliere **output**dal menu **Visualizza** .  
  
**Per eseguire la migrazione dei dati**  
  
1.  Assicurarsi di aver caricato gli oggetti di database di Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in o SQL Azure.  
  
2.  In Esplora metadati di Access selezionare gli oggetti che contengono i dati di cui si desidera eseguire la migrazione:  
  
    -   Per eseguire la migrazione dei dati per un intero database, selezionare la casella di controllo accanto al nome del database.  
  
    -   Per eseguire la migrazione dei dati da singole tabelle, espandere il database, espandere **tabelle**, quindi selezionare la casella di controllo accanto alla tabella. Per omettere i dati dalle singole tabelle, deselezionare la casella di controllo.  
  
3.  Fare clic con il pulsante destro del mouse su **database** , quindi selezionare **Migrate data**.  
  
È anche possibile eseguire la migrazione dei dati all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA usando l'utilità della riga [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]di comando **bcp** o. Per ulteriori informazioni su questi strumenti, vedere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la documentazione online.  
  
## <a name="next-step"></a>passaggio successivo  
Se si dispone di applicazioni di database di Access che si desidera continuare a utilizzare dopo la migrazione, collegare le tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a o SQL Azure tabelle. Per ulteriori informazioni, vedere [collegamento di applicazioni di accesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Vedi anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Impostazione delle opzioni di conversione e migrazione](setting-conversion-and-migration-options-accesstosql.md)  
  
