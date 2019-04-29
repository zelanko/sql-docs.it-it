---
title: Visualizzazione di informazioni sulle regole di confronto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9cb0f104d1555b18d18df38027c240a392d2ac66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918715"
---
# <a name="view-collation-information"></a>Visualizzazione di informazioni sulle regole di confronto
    
##  <a name="Top"></a> È possibile visualizzare le regole di confronto di un server, di un database o di una colonna in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando le opzioni di menu di Esplora oggetti oppure tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="Procedures"></a> Visualizzazione di un'impostazione relativa alle regole di confronto  
 È possibile usare uno dei seguenti elementi:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per visualizzare un'impostazione delle regole di confronto per un server (istanza di SQL Server) in Esplora oggetti**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sull'istanza e selezionare **Proprietà**.  
  
 **Per visualizzare un'impostazione delle regole di confronto per un database in Esplora oggetti**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, fare clic con il pulsante destro del mouse sul database e selezionare **Proprietà**.  
  
 **Per visualizzare un'impostazione delle regole di confronto per una colonna in Esplora oggetti**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, il database desiderato, quindi **Tabelle**.  
  
3.  Espandere la tabella che contiene la colonna, quindi espandere **Colonne**.  
  
4.  Fare clic con il pulsante destro del mouse sulla colonna e selezionare **Proprietà**. Se la proprietà di regola di confronto è vuota, la colonna non è un tipo di dati character.  
  
###  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per visualizzare l'impostazione delle regole di confronto di un server**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e nella barra degli strumenti fare clic su **Nuova query**.  
  
2.  Nella finestra Query, immettere l'istruzione seguente che usano la funzione di sistema SERVERPROPERTY.  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  In alternativa, è possibile usare la stored procedure di sistema sp_helpsort.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **Per visualizzare tutte le regole di confronto supportate da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e nella barra degli strumenti fare clic su **Nuova query**.  
  
2.  Nella finestra Query, immettere l'istruzione seguente che usano la funzione di sistema SERVERPROPERTY.  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **Per visualizzare l'impostazione delle regole di confronto di un database**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e nella barra degli strumenti fare clic su **Nuova query**.  
  
2.  Nella finestra Query, immettere l'istruzione seguente che usano la vista del catalogo sys.databases.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  In alternativa, è possibile usare la funzione di sistema DATABASEPROPERTYEX.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **Per visualizzare l'impostazione delle regole di confronto di una colonna**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e nella barra degli strumenti fare clic su **Nuova query**.  
  
2.  Nella finestra Query, immettere l'istruzione seguente che usano la vista del catalogo sys.columns.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [Precedenza delle regole di confronto &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [sp_helpsort &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsort-transact-sql)  
  
  
