---
title: Eseguire il debug di stored procedure
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.EXECUTESTOREDPROCEDURE.DIALOG
ms.assetid: e3c8707f-0f6b-4265-8a5a-81f079330b52
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: efd64369a6a8e666d67f2c277df62dc9af9c4e99
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241436"
---
# <a name="how-to-debug-stored-procedures"></a>Procedura: Eseguire il debug di stored procedure

Il debugger Transact\-SQL consente di eseguire il debug di stored procedure in modo interattivo visualizzando lo stack di chiamate SQL, i parametri e le variabili locali per la stored procedure SQL. Come accade per l'esecuzione del debug in altri linguaggi di programmazione, è possibile visualizzare e modificare parametri e variabili locali, visualizzare variabili globali, nonché controllare e gestire punti di interruzione durante l'esecuzione del debug dello script Transact\-SQL.  
  
In questo esempio viene illustrato come creare ed eseguire il debug di una stored procedure Transact\-SQL eseguendo istruzioni.  
  
> [!WARNING]  
> Nella procedura seguente vengono usate entità create nelle procedure nelle sezioni [Sviluppo del database connesso](../ssdt/connected-database-development.md) e [Sviluppo di database offline orientato ai progetti](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-debug-stored-procedures"></a>Per eseguire il debug di stored procedure  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **TradeDev** e selezionare **Aggiungi**, quindi **Stored procedure**. Denominare questa nuova stored procedure **AddProduct** e fare clic su **Aggiungi**.  
  
2.  Incollare il codice seguente nella stored procedure.  
  
    ```  
    CREATE PROCEDURE [dbo].[AddProduct]  
    @id int,  
    @name nvarchar(128)  
    AS  
    INSERT INTO [dbo].[Product] (Id, Name) VALUES (@id, @name)  
    ```  
  
3.  Premere F5 per compilare e distribuire il progetto.  
  
4.  Nel nodo **Locale** in Esplora oggetti di SQL Server fare clic con il pulsante destro del mouse sul database **TradeDev** e selezionare **Nuova query**.  
  
5.  Incollare il codice seguente nella finestra Query.  
  
    ```  
    EXEC [dbo].[AddProduct] 50, N'Contoso';  
    GO  
    ```  
  
6.  Fare clic sul margine sinistro della finestra per aggiungere un punto di interruzione all'istruzione `EXEC`.  
  
7.  Premere la freccia a discesa sul pulsante freccia verde nella barra degli strumenti dell'Editor Transact\-SQL e selezionare **Esegui con debugger** per eseguire la query contestualmente al debug.  
  
8.  In alternativa, è possibile avviare il debug da Esplora oggetti di SQL Server. Fare clic con il pulsante destro del mouse sulla stored procedure **AddProduct** (all'interno di **Locale** ->  database **TradeDev** -> **Programmazione** -> **Stored procedure**). Selezionare **Debug procedura...** . Se per l'oggetto vengono richiesti parametri, verrà visualizzata la finestra di dialogo **Debug procedura** con una tabella contenente una riga per ogni parametro. In ogni riga della tabella sono presenti due colonne: una per il nome del parametro e un'altra per il relativo valore. Immettere i valori per ogni parametro e fare clic su OK.  
  
9. Verificare che la finestra **Variabili locali** sia aperta. In caso contrario, scegliere **Finestre** dal menu **Debug**, quindi **Locale**.  
  
10. Premere F11 per eseguire istruzioni sulla query. Si noti che i parametri della stored procedure e i rispettivi valori vengono visualizzati nella finestra **Variabili locali**. In alternativa, passare il mouse sul parametro `@name` nella clausola `INSERT` per visualizzarne il valore **Contoso** assegnato.  
  
11. Fare clic su **Contoso** nella casella degli strumenti. Digitare **Fabrikam** e premere INVIO per modificare il valore della variabile `name` durante l'esecuzione del debug. È inoltre possibile modificare il relativo valore nella finestra **Variabili locali**. Si noti che il valore del parametro viene ora visualizzato in rosso, indicando che è stato modificato.  
  
12. Premere F10 per eseguire istruzioni sul codice rimanente.  
  
13. In Esplora oggetti di SQL Server aggiornare il nodo del database **TradeDev** per visualizzare i nuovi contenuti nella vista dati della tabella **Product**.  
  
14. In Esplora oggetti di SQL Server nel nodo **Locale** individuare la tabella **Product** del database **TradeDev**.  
  
15. Fare clic con il pulsante destro del mouse sulla tabella **Product** e selezionare **Visualizza dati**. Si noti che la nuova riga è stata aggiunta alla tabella.  
  
