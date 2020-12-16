---
title: Eliminare una stored procedure | Microsoft Docs
description: Informazioni su come eliminare una stored procedure in SQL Server 2019 (15.x) usando SQL Server Management Studio o Transact-SQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 742b0e7f3631f5cf262ff6e20bdc64f1ba7bea7f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475312"
---
# <a name="delete-a-stored-procedure"></a>Eliminare una stored procedure
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
    
##  <a name="this-topic-describes-how-to-delete-a-stored-procedure-in-sscurrent-by-using-ssmanstudiofull-or-tsql"></a><a name="Top"></a> In questo argomento viene descritto come eliminare una stored procedure in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#Restrictions), [Sicurezza](#Security)  
  
-   **Per eliminare una stored procedure usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 L'eliminazione di una stored procedure può causare errori negli oggetti e script dipendenti quando questi non vengono aggiornati per riflettere la rimozione della stored procedure. Tuttavia, se si crea una nuova stored procedure con lo stesso nome e gli stessi parametri per sostituire quella eliminata, gli altri oggetti che fanno riferimento ancora alla stored procedure verranno elaborati correttamente. Per altre informazioni, vedere [Visualizzare le dipendenze di una stored procedure](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per lo schema a cui appartiene la stored procedure oppure l'autorizzazione CONTROL per la stored procedure.  
  
##  <a name="how-to-delete-a-stored-procedure"></a><a name="Procedures"></a> Modalità di eliminazione di una stored procedure  
 È possibile usare uno dei seguenti elementi:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per eliminare una stored procedure in Esplora oggetti**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, espandere il database a cui appartiene la stored procedure, quindi espandere **Programmabilità**.  
  
3.  Espandere **Stored procedure**, fare clic con il pulsante destro del mouse sulla stored procedure da rimuovere e scegliere **Elimina**.  
  
4.  Per visualizzare gli oggetti dipendenti dalla stored procedure, fare clic su **Mostra dipendenze**.  
  
5.  Confermare che è stata selezionata la stored procedure corretta, quindi scegliere **OK**.  
  
6.  Rimuovere i riferimenti alla stored procedure da tutti gli oggetti e script dipendenti.  

###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per eliminare una stored procedure nell'editor di query**  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database** ed espandere il database a cui appartiene la stored procedure. In alternativa, dalla barra degli strumenti selezionare il database dall'elenco di database disponibili.  
  
3.  Scegliere **Nuova query** dal menu File.  
  
4.  Ottenere il nome della stored procedure da rimuovere nel database corrente. Da Esplora oggetti espandere **Programmabilità** , quindi espandere **Stored procedure**. In alternativa, nell'editor di query eseguire l'istruzione riportata di seguito.  
  
    ```sql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  Copiare e incollare l'esempio seguente nell'editor di query e inserire il nome di una stored procedure da eliminare dal database corrente.  
  
    ```sql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  Rimuovere i riferimenti alla stored procedure da tutti gli oggetti e script dipendenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificare una stored procedure](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Rinominare una stored procedure](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Visualizzare la definizione di una stored procedure](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Visualizzare le dipendenze di una stored procedure](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
