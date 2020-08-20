---
description: 'Esercitazione di T-SQL: Eliminare gli oggetti di database'
title: 'Esercitazione di T-SQL: Eliminare gli oggetti di database | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1a032737a39cf22e1b2d5516c615ced9d59dfc43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467530"
---
# <a name="lesson-3-delete-database-objects"></a>Lezione 3: Eliminare gli oggetti di database
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
In questa breve lezione viene illustrato come rimuovere gli oggetti creati nelle lezioni 1 e 2 e come procedere quindi all'eliminazione del database.  
  
Prima di eliminare gli oggetti, verificare di trovarsi nel database corretto:
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>Revocare autorizzazioni per le stored procedure
  
Utilizzare l'istruzione `REVOKE` per rimuovere l'autorizzazione di esecuzione per `Mary` sulla stored procedure:
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>Eliminare le autorizzazioni

1. Utilizzare l'istruzione `DROP` per rimuovere l'autorizzazione di accesso per `Mary` al database `TestData` :
  
   ```sql  
   DROP USER Mary;  
   GO  
   ```  


2. Utilizzare l'istruzione `DROP` per rimuovere l'autorizzazione di accesso per `Mary` all'istanza di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]:
  
   ```sql  
   DROP LOGIN [<computer_name>\Mary];  
   GO   
   ```  
  
3. Utilizzare l'istruzione `DROP` per rimuovere la stored procedure `pr_Names`:  
  
   ```sql  
   DROP PROC pr_Names;  
   GO   
   ```  
  
4. Utilizzare l'istruzione `DROP` per rimuovere la vista `vw_Names`:  
  
   ```sql  
   DROP VIEW vw_Names;  
   GO  
   ```  

## <a name="delete-table"></a>Eliminare la tabella
  
1. Utilizzare l'istruzione `DELETE` per rimuovere tutte le righe della tabella `Products` :  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  Utilizzare l'istruzione `DROP` per rimuovere la tabella `Products` :  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>Rimuovere il database
  
Non è possibile rimuovere il database `TestData` se è in uso. Passare pertanto a un altro database e quindi utilizzare l'istruzione `DROP` per rimuovere il database `TestData` :  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
In questo modo si conclude l'esercitazione per la scrittura di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] . Tenere presente che questa esercitazione rappresenta una breve panoramica in cui non vengono descritte tutte le opzioni delle istruzioni utilizzate. La progettazione e la creazione di una struttura di database efficiente e la configurazione dell'accesso sicuro ai dati richiede un database più complesso di quello illustrato in questa esercitazione.  

  
  
