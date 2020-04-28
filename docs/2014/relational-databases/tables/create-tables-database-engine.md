---
title: Creare tabelle (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table creation [SQL Server], Visual Database Tools
ms.assetid: 6f7c6ac5-e6d3-4dca-831e-b28442ba535b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 261aab8b0e8a5d80aed143d6b29e952243742917
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176819"
---
# <a name="create-tables-database-engine"></a>Creare tabelle (motore di database)
  È possibile creare una nuova tabella, assegnarle un nome e aggiungerla a un database esistente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!NOTE]
>  Se si è connessi a un database di SQL Azure, l'opzione Nuova tabella avvierà uno script modello per la creazione della tabella. Modificare i parametri, quindi eseguire lo script per creare una nuova tabella. Per ulteriori informazioni, vedere [SQL Azure Overview](https://microsoft.sharepoint.com/sites/infopedia_g01/pages/cards/azure-sql-database.aspx).

 **Contenuto dell'articolo**

-   **Prima di iniziare:**

     [Sicurezza](#Security)

-   **Per creare una tabella:**

     [SQL Server Management Studio](#SSMSProcedure)

     [Transact-SQL](#TsqlProcedure)

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare

###  <a name="security"></a><a name="Security"></a> Sicurezza

####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni
 Sono richieste l'autorizzazione CREATE TABLE per il database e l'autorizzazione ALTER per lo schema in cui viene creata la tabella.

 Se tutte le colonne nell'istruzione CREATE TABLE sono definite come tipo CLR definito dall'utente, è necessario che l'utente sia il proprietario del tipo o disponga dell'autorizzazione REFERENCES.

 Se a una colonna nell'istruzione CREATE TABLE è associata una raccolta di XML Schema, è necessario che l'utente sia il proprietario della raccolta di XML Schema o disponga dell'autorizzazione REFERENCES.

##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio

#### <a name="to-create-a-table-with-table-designer"></a>Per creare una tabella con Progettazione tabelle

1.  In **Esplora oggetti**connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] contenente il database da modificare.

2.  In **Esplora oggetti**espandere il nodo **Database** , quindi espandere il database in cui sarà contenuta la nuova tabella.

3.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nodo **Tabelle** del database, quindi su **Nuova tabella**.

4.  Digitare i nomi delle colonne, scegliere i tipi di dati e indicare se sono consentiti i valori Null per ogni colonna come mostrato nell'illustrazione riportata di seguito.

     ![AddColumnsinTableDesigner](../../database-engine/media/addcolumnsintabledesigner.gif "AddColumnsinTableDesigner")

5.  Per specificare più proprietà di una colonna, ad esempio i valori di colonna calcolata o Identity, fare clic sulla colonna e nella scheda delle proprietà delle colonne scegliere le proprietà appropriate. Per altre informazioni sulle proprietà delle colonne, vedere [Proprietà delle colonne delle tabelle &#40;SQL Server Management Studio&#41;](table-column-properties-sql-server-management-studio.md).

6.  Per specificare una colonna come chiave primaria, fare clic con il pulsante destro del mouse sulla colonna e selezionare **Imposta chiave primaria**. Per altre informazioni, vedere [Create Primary Keys](../tables/create-primary-keys.md).

7.  Per creare relazioni di chiave esterna, vincoli CHECK o indici, fare clic con il pulsante destro del mouse nel riquadro Progettazione tabelle e selezionare un oggetto nell'elenco come mostrato nell'illustrazione riportata di seguito.

     ![AddTableObjects](../../database-engine/media/addtableobjects.gif "AddTableObjects")

     Per ulteriori informazioni su questi oggetti, vedere [Create Foreign Key Relationships](../tables/create-foreign-key-relationships.md), [Create Check Constraints](../tables/create-check-constraints.md) e [Indexes](../indexes/indexes.md).

8.  Per impostazione predefinita, la tabella è inclusa nello schema **dbo** . Per specificare uno schema diverso per la tabella, fare clic con il pulsante destro del mouse nel riquadro Progettazione tabelle e selezionare **Proprietà** come mostrato nell'illustrazione riportata di seguito. Nell'elenco a discesa **Schema** selezionare lo schema appropriato.

     ![Specifyatableschema](../../database-engine/media/specifyatableschema.gif "Specifyatableschema")

     Per ulteriori informazioni sugli schemi, vedere [Create a Database Schema](../security/authentication-access/create-a-database-schema.md).

9. Scegliere **Salva** *nometabella* dal menu **File**.

10. Nella finestra di dialogo **Scegli nome** digitare un nome per la tabella, quindi fare clic su **OK**.

11. Per visualizzare la nuova tabella, in **Esplora oggetti**espandere il nodo **Tabelle** e premere **F5** per aggiornare l'elenco di oggetti. La nuova tabella viene visualizzata nell'elenco di tabelle.

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL

#### <a name="to-create-a-table-in-the-query-editor"></a>Per creare una tabella nell'editor di query

1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2.  Sulla barra Standard fare clic su **Nuova query**.

3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.

    ```
    CREATE TABLE dbo.PurchaseOrderDetail
    (
        PurchaseOrderID int NOT NULL
        ,LineNumber smallint NOT NULL
        ,ProductID int NULL
        ,UnitPrice money NULL
        ,OrderQty smallint NULL
        ,ReceivedQty float NULL
        ,RejectedQty float NULL
        ,DueDate datetime NULL
    );
    ```

 Per altri esempi, vedere [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).


