---
title: Modificare un indice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1da4462f3ba23d263cd30d222f7b9026285b1159
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63162375"
---
# <a name="modify-an-index"></a>Modificare un indice
  In questo argomento viene descritto come modificare un indice in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Gli indici creati come risultato di un vincolo PRIMARY KEY o UNIQUE non possono essere modificati con questo metodo. È necessario invece modificare il vincolo.  
  
 **Contenuto dell'articolo**  
  
-   **Per modificare un indice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-modify-an-index"></a>Per modificare un indice  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, espandere il database a cui appartiene la tabella e quindi espandere **Tabelle**.  
  
3.  Espandere la tabella a cui appartiene l'indice e quindi espandere **Indici**.  
  
4.  Fare clic con il pulsante destro del mouse sull'indice da modificare l'indice e scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo **Proprietà indice** apportare le modifiche desiderate. È ad esempio possibile aggiungere o rimuovere una colonna dalla chiave di indice o modificare l'impostazione di un'opzione di indice.  
  
#### <a name="to-modify-index-columns"></a>Per modificare le colonne indice  
  
1.  Per aggiungere, rimuovere o modificare la posizione di una colonna indice, selezionare la pagina **Generale** della finestra di dialogo **Proprietà indice** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-modify-an-index"></a>Per modificare un indice  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene eliminato e ricreato un indice esistente sulla colonna `ProductID` della tabella `Production.WorkOrder` tramite l'opzione `DROP_EXISTING` . Vengono inoltre impostate le opzioni `FILLFACTOR` e `PAD_INDEX` .  
  
     [!code-sql[IndexDDL#CreateIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/createindex.sql#createindex4)]  
  
     Nell'esempio seguente viene usato ALTER INDEX per impostare diverse opzioni sull'indice `AK_SalesOrderHeader_SalesOrderNumber`.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
#### <a name="to-modify-index-columns"></a>Per modificare le colonne indice  
  
1.  Per aggiungere, rimuovere o modificare la posizione di una colonna dell'indice, è necessario eliminare e ricreare l'indice.  
  
## <a name="see-also"></a>Vedi anche  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [INDEXPROPERTY &#40;&#41;Transact-SQL](/sql/t-sql/functions/indexproperty-transact-sql)   
 [sys. Indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)   
 [sys. index_columns &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)   
 [Impostare le opzioni per gli indici](set-index-options.md)   
 [Ridenominazione di indici](indexes.md)  
  
  
