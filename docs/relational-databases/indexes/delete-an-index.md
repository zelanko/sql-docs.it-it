---
title: Eliminare un indice | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7337617c8c6bc2e904d5b258fec1d666f63a0ded
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107199"
---
# <a name="delete-an-index"></a>Eliminare un indice
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In questo argomento si descrive come eliminare (rimuovere) un indice in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per eliminare un indice utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Gli indici creati come risultato di un vincolo PRIMARY KEY o UNIQUE non possono essere eliminati mediante questa procedura. È infatti necessario eliminare il vincolo. Per rimuovere il vincolo e l'indice corrispondente, utilizzare [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) con la clausola DROP CONSTRAINT in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per altre informazioni, vedere [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per la tabella o la vista. Questa autorizzazione viene concessa per impostazione predefinita al ruolo predefinito del server **sysadmin** e ai ruoli predefiniti del database **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>Per eliminare un indice utilizzando Esplora oggetti  
  
1.  In Esplora oggetti espandere il database contenente la tabella in cui si desidera eliminare un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella contenente l'indice che si desidera eliminare.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice che si desidera eliminare e scegliere **Elimina**.  
  
6.  Nella finestra di dialogo **Elimina oggetto** verificare che nella griglia **Oggetto da eliminare** sia presente l'indice corretto e fare clic su **OK**.  
  
#### <a name="to-delete-an-index-using-table-designer"></a>Per eliminare un indice utilizzando Progettazione tabelle.  
  
1.  In Esplora oggetti espandere il database contenente la tabella in cui si desidera eliminare un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella contenente l'indice da eliminare e scegliere Progetta.  
  
4.  Scegliere **Indici/chiavi** nel menu **Progettazione tabelle**.  
  
5.  Nella finestra di dialogo **Indici/chiavi** selezionare l'indice da eliminare.  
  
6.  Fare clic su **Elimina**.  
  
7.  Scegliere **Chiudi**.  
  
8.  Nel menu **File** selezionare **Salva**_nome_tabella_.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-delete-an-index"></a>Per eliminare un indice  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 Per altre informazioni, vedere [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md).  
  
  
