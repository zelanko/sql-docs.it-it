---
title: Creare indici con colonne incluse | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index size [SQL Server]
- index keys [SQL Server]
- index columns [SQL Server]
- size [SQL Server], indexes
- key columns [SQL Server]
- included columns
- nonclustered indexes [SQL Server], included columns
- designing indexes [SQL Server], included columns
- nonkey columns
ms.assetid: d198648d-fea5-416d-9f30-f9d4aebbf4ec
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c0c6449082f1c5ca016cfdb0a0f18430cf74731
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124436"
---
# <a name="create-indexes-with-included-columns"></a>Creare indici con colonne incluse
  In questo argomento si illustra come aggiungere colonne incluse (o non chiave) per estendere la funzionalità di indici non cluster in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'inclusione di colonne non chiave è possibile creare indici non cluster in grado di coprire più query. Ciò è possibile perché le colonne non chiave presentano i vantaggi seguenti:  
  
-   Possono essere tipi di dati che non sono consentiti come colonne chiave indice.  
  
-   Non vengono prese in esame dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] durante il calcolo del numero di colonne chiave indice o della dimensione delle chiavi di indice.  
  
 Con un indice con colonne non chiave è possibile aumentare significativamente le prestazioni delle query quando tutte le relative colonne sono incluse nell'indice come colonne chiave o non chiave. I vantaggi nelle prestazioni si ottengono poiché Query Optimizer può individuare tutti i valori delle colonne all'interno dell'indice. In questo modo, la quantità di operazioni di I/O su disco è inferiore dato che non viene eseguito alcun accesso ai dati delle tabelle o degli indici cluster.  
  
> [!NOTE]  
>  Quando in un indice sono contenute tutte le colonne a cui fa riferimento una query, viene generalmente indicato come *copertura della query*.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni sulla progettazione](#DesignRecs)  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un indice con colonne non chiave utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="DesignRecs"></a> Indicazioni sulla progettazione  
  
-   Progettare nuovamente gli indici non cluster con chiavi di indice dalle dimensioni elevate in modo da utilizzare come colonne chiave solo le colonne utilizzate per le ricerche. Modificare in colonne non chiave tutte le altre colonne che coprono la query. In questo modo si avranno tutte le colonne necessarie per coprire la query, contenendo al tempo stesso le dimensioni della chiave dell'indice e mantenendone l'efficienza.  
  
-   Includere colonne non chiave in un indice non cluster per evitare il superamento delle limitazioni di dimensione correnti degli indici (numero massimo di colonne chiave pari a 16 e dimensione massima delle chiavi di indice pari a 900 byte). Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non prende in esame le colonne non chiave durante il calcolo del numero di colonne chiave indice o della dimensione delle chiavi di indice.  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le colonne non chiave possono essere definite solo negli indici non cluster.  
  
-   È possibile utilizzare come colonne non chiave tutti i tipi di dati eccetto `text`, `ntext` e `image`.  
  
-   Le colonne calcolate deterministiche, precise o imprecise, possono essere colonne non chiave. Per altre informazioni, vedere [Indici per le colonne calcolate](indexes-on-computed-columns.md).  
  
-   Le colonne calcolate derivate dai tipi di dati `image`, `ntext` e `text` possono essere colonne non chiave purché il tipo di dati della colonna calcolata sia consentito come colonna non chiave dell'indice.  
  
-   Non è possibile rimuovere da una tabella le colonne non chiave se non si è prima eliminato l'indice di questa tabella.  
  
-   Non è possibile modificare le colonne non chiave se non per eseguire le operazioni seguenti:  
  
    -   Modifica del supporto di valori NULL della colonna da NOT NULL a NULL.  
  
    -   Aumento della lunghezza di colonne `varchar`, `nvarchar` o `varbinary`.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per la tabella o la vista. L'utente deve essere un membro del ruolo predefinito del server **sysadmin** o dei ruoli predefiniti del database **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Per creare un indice con colonne non chiave  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il database contenente la tabella in cui si desidera creare un indice con colonne non chiave.  
  
2.  Fare clic sul segno più per espandere la cartella **Tabelle** .  
  
3.  Fare clic sul segno più per espandere la tabella in cui si desidera creare un indice con colonne non chiave.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Indici**, scegliere **Nuovo indice**e selezionare **Indice non cluster**.  
  
5.  Nella pagina **Generale** della finestra di dialogo **Nuovo indice** immettere il nome del nuovo indice nella casella **Nome indice** .  
  
6.  Nella scheda **Colonne chiave indice** scegliere **Aggiungi**.  
  
7.  Nella finestra di dialogo **Seleziona colonne da**_table_name_ selezionare le caselle di controllo delle colonne della tabella da aggiungere all'indice.  
  
8.  Fare clic su **OK**.  
  
9. Nella scheda **Colonne incluse** scegliere **Aggiungi**.  
  
10. Nella finestra di dialogo **Seleziona colonne da**_table_name_ selezionare le caselle di controllo delle colonne di tabella da aggiungere all'indice come colonne non chiave.  
  
11. Fare clic su **OK**.  
  
12. Nella finestra di dialogo **Nuovo indice** fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-an-index-with-nonkey-columns"></a>Per creare un indice con colonne non chiave  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Creates a nonclustered index on the Person.Address table with four included (nonkey) columns.   
    -- index key column is PostalCode and the nonkey columns are  
    -- AddressLine1, AddressLine2, City, and StateProvinceID.  
    CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
  
