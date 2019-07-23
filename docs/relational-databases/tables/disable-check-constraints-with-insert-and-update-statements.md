---
title: Disabilitare i vincoli CHECK con le istruzioni INSERT e UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a25909bfcfb6e8bbc228af03a608c416ab55bd3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016383"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>Disabilitazione di vincoli CHECK con le istruzioni INSERT e UPDATE
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  È possibile disabilitare un vincolo CHECK per transazioni INSERT e UPDATE in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Dopo aver disabilitato i vincoli CHECK, gli inserimenti o gli aggiornamenti successivi della colonna non saranno convalidati in base alle condizioni del vincolo. Usare questa opzione se si è sicuri che i nuovi dati violeranno il vincolo esistente o se il vincolo si applica solo ai dati già presenti nel database.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per disabilitare un vincolo CHECK per le istruzioni INSERT e UPDATE:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Per disabilitare un vincolo CHECK per le istruzioni INSERT e UPDATE  
  
1.  In **Esplora oggetti**, espandere la tabella contenente il vincolo che si desidera modificare, quindi espandere la cartella **Vincoli** .  
  
2.  Fare clic con il pulsante destro del mouse sul vincolo e scegliere **Modifica**.  
  
3.  Nella griglia, in **Progettazione tabelle**, fare clic su **Attiva per istruzioni INSERTs e UPDATEs** , quindi scegliere **No** dal menu a discesa.  
  
4.  Scegliere **Chiudi**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Per disabilitare un vincolo CHECK per le istruzioni INSERT e UPDATE  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare gli esempi seguenti nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
