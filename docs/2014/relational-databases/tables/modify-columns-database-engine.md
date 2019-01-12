---
title: Modificare colonne (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23567accc051e72ede3b8ed079b22411de6bc7c6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126091"
---
# <a name="modify-columns-database-engine"></a>Modificare colonne (motore di database)
  È possibile modificare il tipo di dati di una colonna in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  La modifica del tipo di dati di una colonna in cui sono già contenuti dati può comportare la perdita definitiva di tali dati al momento della conversione. È possibile inoltre che si verifichino errori nel codice e nelle applicazioni che dipendono dalla colonna modificata, incluse query, viste, stored procedure, funzioni definite dall'utente e applicazioni client. Tali errori inoltre tendono a propagarsi a cascata. Possono ad esempio verificarsi errori in una stored procedure che chiama una funzione definita dall'utente che dipende dalla colonna modificata. È pertanto opportuno valutare seriamente ogni eventuale modifica da apportare a una colonna prima di procedere.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per modificare il tipo di dati di una colonna:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Per modificare il tipo di dati di una colonna  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulle colonne della tabella di cui modificare la scala e scegliere **Progetta**.  
  
2.  Selezionare la colonna per la quale si desidera modificare il tipo di dati.  
  
3.  Nella scheda **Proprietà colonne** fare clic sulla cella della griglia relativa alla proprietà **Tipo di dati** , quindi selezionare un nuovo tipo di dati dall'elenco a discesa.  
  
4.  Nel menu **File** scegliere **Salva**_table name_.  
  
> [!NOTE]  
>  Quando si modifica il tipo di dati di una colonna, in Progettazione tabelle verrà applicata la lunghezza predefinita del tipo di dati selezionato, anche se ne è stata già specificata un'altra. È pertanto opportuno impostare sempre la lunghezza del tipo di dati per il valore desiderato dopo avere specificato il tipo di dati.  
  
> [!WARNING]  
>  Se si tenta di modificare il tipo di dati di una colonna correlata alle altre tabelle, Progettazione tabelle chiede all'utente di confermare anche la modifica da apportare alle colonne nelle altre tabelle.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Per modificare il tipo di dati di una colonna  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
