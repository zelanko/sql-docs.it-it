---
title: Creare indici non cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], nonclustered indexes
- nonclustered indexes [SQL Server], creating
- nonclustered indexes [SQL Server], UNIQUE constraint
- indexes [SQL Server], nonclustered
- nonclustered indexes [SQL Server], PRIMARY KEY constraint
ms.assetid: 9402029a-1227-46c4-93aa-c2122eb1b943
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 932bd340e84e352eb6de2bd714508135328024d1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533060"
---
# <a name="create-nonclustered-indexes"></a>Creare indici non cluster
  È possibile creare indici non cluster in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un indice non cluster è una struttura di indice separata dai dati archiviati in una tabella che riordina una o più colonne selezionate. Spesso gli indici non cluster consentono di trovare i dati più rapidamente rispetto alla ricerca nella tabella sottostante. Le query talvolta possono ottenere risposta unicamente mediante i dati presenti nell'indice non cluster oppure l'indice non cluster può puntare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle righe nella tabella sottostante. Gli indici non cluster vengono creati generalmente per migliorare le prestazioni delle query di utilizzo frequente non coperte dall'indice cluster oppure per individuare le righe in una tabella senza un indice cluster (denominato heap). In una vista tabella o indicizzata è possibile creare più indici non cluster.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Modalità di implementazione tipiche](#Implementations)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un indice non cluster tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Implementations"></a> Modalità di implementazione tipiche  
 Gli indici non cluster vengono implementati nei modi seguenti:  
  
-   **Vincoli UNIQUE**  
  
     Quando si crea un vincolo UNIQUE, viene creato un indice non cluster univoco per applicare un vincolo UNIQUE per impostazione predefinita. È possibile specificare un indice cluster univoco se nella tabella non ne esiste già uno. Per altre informazioni, vedere [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
-   **Indice indipendente da un vincolo**  
  
     Per impostazione predefinita, viene creato un indice non cluster se non è stato specificato l'indice cluster. Il numero massimo di indici non cluster che è possibile creare per tabella è 999. Sono inclusi gli indici creati tramite i vincoli PRIMARY KEY o UNIQUE, ma non gli indici XML.  
  
-   **Indice non cluster su una vista indicizzata**  
  
     Dopo la creazione di un indice cluster univoco su una vista, è possibile creare indici non cluster. Per altre informazioni, vedere [Creare viste indicizzate](../views/views.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione ALTER per la tabella o la vista. L'utente deve essere un membro del ruolo predefinito del server **sysadmin** o dei ruoli predefiniti del database **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-nonclustered-index-by-using-the-table-designer"></a>Per creare un indice non cluster tramite Progettazione tabelle  
  
1.  In Esplora oggetti espandere il database contenente la tabella in cui si desidera creare un indice non cluster.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella in cui creare un indice non cluster e selezionare **Progetta**.  
  
4.  Scegliere **Indici/chiavi** nel menu **Progettazione tabelle**.  
  
5.  Nella finestra di dialogo **Indici/chiavi** fare clic su **Aggiungi**.  
  
6.  Selezionare il nuovo indice dalla casella di testo **Chiave o indice primario/univoco selezionato** .  
  
7.  Nella griglia selezionare **Crea come CLUSTERED**, quindi scegliere **No** dall'elenco a discesa a destra della proprietà.  
  
8.  Scegliere **Chiudi**.  
  
9. Scegliere **Salva***nome_tabella* dal menu **File**.  
  
#### <a name="to-create-a-nonclustered-index-by-using-object-explorer"></a>Per creare un indice non cluster tramite Esplora oggetti  
  
1.  In Esplora oggetti espandere il database contenente la tabella in cui si desidera creare un indice non cluster.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella in cui si desidera creare un indice non cluster.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Indici**, scegliere **Nuovo indice**e selezionare **Indice non cluster**.  
  
5.  Nella pagina **Generale** della finestra di dialogo **Nuovo indice** immettere il nome del nuovo indice nella casella **Nome indice** .  
  
6.  In **Colonne chiave indice**fare clic su **Aggiungi**.  
  
7.  Nella finestra di dialogo **Seleziona colonne da***nome_tabella* selezionare le caselle di controllo delle colonne di tabella da aggiungere all'indice non cluster.  
  
8.  Fare clic su **OK**.  
  
9. Nella finestra di dialogo **Nuovo indice** fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-nonclustered-index-on-a-table"></a>Per creare un indice non cluster in una tabella  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
  
