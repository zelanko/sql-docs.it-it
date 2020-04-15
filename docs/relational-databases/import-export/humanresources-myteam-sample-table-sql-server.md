---
title: Tabella di esempio HumanResources.myTeam (SQL Server) | Microsoft Docs
description: Per eseguire esempi di codice per l'importazione e l'esportazione bulk di dati in SQL Server, è necessario creare una tabella di test denominata myTeam nello schema HumanResources.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 73ec7e3d639d49fd12a0c0b6708278702a423f0e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980456"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Tabella di esempio HumanResources.myTeam (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Molti degli esempi di codice inclusi nell'argomento relativo all' [importazione ed esportazione di dati bulk](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) richiedono una tabella di prova speciale denominata **myTeam**. Prima che sia possibile eseguire gli esempi, è necessario creare la tabella **myTeam** nello schema **HumanResources** del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] è uno dei database di esempio disponibili in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Nella tabella **myTeam** sono incluse le colonne seguenti.  
  
|Colonna|Tipo di dati|Supporto di valori Null|Descrizione|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|Non Null|Chiave primaria per le righe. ID dipendente di un membro del team.|  
|**Nome**|**nvarchar(50)**|Non Null|Nome di un membro del team.|  
|**Titolo**|**nvarchar(50)**|Nullable|Titolo professionale del dipendente nel team.|  
|**Background**|**nvarchar(50)**|Non Null|Data e ora dell'ultimo aggiornamento della riga. Valore predefinito.|  
  
**Per creare HumanResources.myTeam**  
  
-   Utilizzare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**Per popolare HumanResources.myTeam**  
  
-   Eseguire le istruzioni `INSERT` seguenti per popolare la tabella con due righe:  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Queste istruzioni ignorano la quarta colonna, `Background`, che ha un valore predefinito. Ignorando la colonna, l'istruzione `INSERT` lascia la colonna vuota.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sull'importazione ed esportazione bulk di dati &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
