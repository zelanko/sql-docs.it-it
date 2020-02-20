---
title: Oggetti di SQL Server 2012 nel progetto
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c9ea326bc37d4843b6cb7e3bc4e21fa356af5435
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244247"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>Procedura: Usare oggetti di Microsoft SQL Server 2012 nel progetto

In questo esempio, si aggiungerà un oggetto Sequence a un progetto di database per Microsoft SQL Server 2012.  
  
Le sequenze sono state introdotte in Microsoft SQL Server 2012. Una sequenza è un oggetto associato a schema definito dall'utente che genera una sequenza di valori numerici in base alla specifica con la quale è stata creata la sequenza. La sequenza di valori numerici viene generata in ordine crescente o decrescente a un intervallo definito e può essere ripetuta (ciclicamente) in base alle esigenze.  Per altre informazioni sugli oggetti Sequence, vedere [Numeri di sequenza](htttp://msdn.microsoft.com/library/ff878058(SQL.110).aspx). Per informazioni sulle novità introdotte in Microsoft SQL Server 2012, vedere [Novità di SQL Server 2012](https://msdn.microsoft.com/library/bb500435(SQL.110).aspx).  
  
> [!WARNING]  
> Nelle procedure seguenti vengono usate entità create nelle procedure precedenti nelle sezioni [Sviluppo del database connesso](../ssdt/connected-database-development.md) e [Sviluppo di database offline orientato ai progetti](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>Per aggiungere un nuovo oggetto Sequence al progetto  
  
1.  Fare clic con il pulsante destro del mouse sul progetto di database **TradeDev** in **Esplora soluzioni**, selezionare **Aggiungi**, quindi **Nuovo elemento**.  
  
2.  Fare clic su **Programmazione** nel riquadro sinistro e selezionare **Sequenza**. Scegliere **Aggiungi** per aggiungere il nuovo oggetto al progetto.  
  
3.  Sostituire il codice predefinito con il codice seguente.  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  Se la piattaforma di destinazione del progetto non è impostata su Microsoft SQL Server 2012, nell'**Elenco errori** verrà visualizzato un errore di sintassi per l'istruzione `CREATE SEQUENCE`. Per correggerlo, seguire l'argomento [Procedura: Modifica della piattaforma di destinazione e pubblicazione di un progetto di database](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) per cambiare la piattaforma di destinazione di conseguenza.  
  
5.  Seguire l'argomento [Procedura: Cambiare la piattaforma di destinazione e pubblicare un progetto di database](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) per pubblicare il progetto in un database nel server Microsoft SQL Server 2012 connesso.  
  
### <a name="to-use-the-new-sequence-object"></a>Per utilizzare il nuovo oggetto Sequence  
  
1.  In Esplora oggetti di SQL Server fare clic con il pulsante destro del mouse sul database pubblicato nella procedura precedente e selezionare **Nuova query**.  
  
2.  Incollare il codice seguente nella finestra Query.  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  Premere il pulsante **Esegui query**.  
  
4.  In **Esplora oggetti di SQL Server** passare alla tabella **Products** nel database. Fare clic con il pulsante destro del mouse e scegliere **Visualizza dati** per esaminare le righe appena aggiunte.  
  
