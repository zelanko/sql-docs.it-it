---
title: Rinominare indici | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5925e277b6e1585612147918b469427e4aa92968
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395784"
---
# <a name="rename-indexes"></a>Ridenominazione di indici
  In questo argomento si descrive come rinominare un indice in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La ridenominazione di un indice consiste nel sostituire il nome attuale dell'indice con il nuovo nome specificato dall'utente. Il nome specificato deve essere univoco all'interno della tabella o della vista. Ad esempio, due tabelle possono avere un indice denominato **XPK_1**, ma la stessa tabella non può contenere due indici denominati **XPK_1**. Non è possibile creare un indice con lo stesso nome di un indice disabilitato esistente. La ridenominazione di un indice non ne causa la ricompilazione.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per rinominare un indice utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Quando si crea un vincolo PRIMARY KEY o UNIQUE in una tabella, viene automaticamente creato un indice per la tabella con lo stesso nome del vincolo. Poiché i nomi di indice di una tabella devono essere univoci, nella tabella non è possibile creare o rinominare un indice in modo che abbia lo stesso nome di un vincolo PRIMARY KEY o UNIQUE esistente.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per l'indice.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>Per rinominare un indice utilizzando Progettazione tabelle  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il database contenente la tabella in cui si desidera rinominare un indice.  
  
2.  Fare clic sul segno più per espandere la cartella **Tabelle** .  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella in cui si desidera rinominare un indice e selezionare **Progetta**.  
  
4.  Scegliere **Indici/chiavi** nel menu **Progettazione tabelle**.  
  
5.  Selezionare l'indice che si desidera rinominare nella casella di testo **Indice o chiave primari/univoci selezionati** .  
  
6.  Nella griglia fare clic su **Nome** e digitare un nuovo nome nella casella di testo.  
  
7.  Scegliere **Chiudi**.  
  
8.  Scegliere **Salva***nome_tabella* dal menu **File**.  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>Per rinominare un indice utilizzando Esplora oggetti  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il database contenente la tabella in cui si desidera rinominare un indice.  
  
2.  Fare clic sul segno più per espandere la cartella **Tabelle** .  
  
3.  Fare clic sul segno più per espandere la tabella in cui si desidera rinominare un indice.  
  
4.  Fare clic sul segno più per espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice che si desidera rinominare e scegliere **Rinomina**.  
  
6.  Digitare il nuovo nome dell'indice e premere INVIO.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-rename-an-index"></a>Per rinominare un indice  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql).  
  
  
