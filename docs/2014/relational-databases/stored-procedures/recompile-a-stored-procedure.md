---
title: Ricompilare una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ae01b9173693370d5e422d4f26b6175101ff12
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536572"
---
# <a name="recompile-a-stored-procedure"></a>Ricompilare una stored procedure
  In questo argomento viene descritto come ricompilare una stored procedure in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esistono tre modi per eseguire questa operazione: `WITH RECOMPILE` option nella definizione della stored procedure o quando viene chiamata la procedura, il `RECOMPILE` hint per la query nelle singole istruzioni o utilizzando il `sp_recompile` stored procedure di sistema. Questo argomento illustra l'uso dell'opzione WITH RECOMPILE quando si crea una definizione di stored procedure e si esegue una stored procedure esistente. Descrive anche l'uso della stored procedure di sistema sp_recompile per ricompilare una stored procedure esistente.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per ricompilare una stored procedure tramite:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Quando una stored procedure viene compilata per la prima volta o viene ricompilata, il piano di query della stored procedure viene ottimizzato per lo stato corrente del database e dei relativi oggetti. Se i dati o la struttura di un database vengono modificati significativamente, con la ricompilazione di una stored procedure viene aggiornato e ottimizzato il piano di query della stored procedure per tali modifiche. Ciò può migliorare le prestazioni di elaborazione della stored procedure.  
  
-   In alcuni casi la ricompilazione della stored procedure deve essere forzata, in altri invece avviene automaticamente. La ricompilazione automatica ha luogo a ogni riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si verifica inoltre se vengono apportate modifiche alla progettazione fisica di una tabella sottostante a cui fa riferimento la stored procedure.  
  
-   È opportuno forzare la ricompilazione di una stored procedure anche per rispondere a un eventuale sniffing dei parametri riscontrato durante la compilazione. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le stored procedure, nella generazione del piano di query rientrano tutti i valori di parametri utilizzati dalla stored procedure durante la compilazione. Se tali valori rappresentano quelli standard utilizzati per le chiamate successive della stored procedure, questa beneficerà del piano di query a ogni compilazione ed esecuzione. Se i valori dei parametri della stored procedure sono spesso atipici, le prestazioni possono migliorare con la forzatura di una ricompilazione della stored procedure e un nuovo piano basato su valori dei parametri diversi.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenta la ricompilazione di stored procedure a livello di istruzione. Quando in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono ricompilate le stored procedure, in realtà viene compilata solo l'istruzione che ha causato la ricompilazione, anziché la stored procedure completa.  
  
-   Se determinate query in una stored procedure utilizzano regolarmente valori atipici o temporanei, le prestazioni della stored procedure possono migliorare tramite l'utilizzo dell'hint per la query RECOMPILE all'interno delle query stesse. Poiché vengono ricompilate solo le query che utilizzano l'hint per la query anziché la stored procedure completa, viene riprodotto il comportamento di ricompilazione a livello di istruzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Oltre all'utilizzo dei valori dei parametri correnti della stored procedure, l'hint per la query RECOMPILE utilizza i valori di qualsiasi variabile locale inclusa nella stored procedure quando si compila l'istruzione. Per altre informazioni, vedere [Hint per la query (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 `WITH RECOMPILE` Opzione  
 Se si utilizza questa opzione alla creazione della definizione della stored procedure, è necessario disporre dell'autorizzazione CREATE PROCEDURE per il database e dell'autorizzazione ALTER per lo schema in cui verrà creata la stored procedure.  
  
 Se questa opzione viene utilizzata in un'istruzione EXECUTE, richiede autorizzazioni EXECUTE sulla stored procedure. Le autorizzazioni non sono richieste per l'istruzione EXECUTE stessa, ma le autorizzazioni di esecuzione sono necessarie per la stored procedure a cui fa riferimento l'istruzione EXECUTE. Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
 `RECOMPILE` Hint per la query  
 Questa funzionalità viene usata quando si crea la stored procedure e si include l'hint nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] nella stored procedure. È pertanto necessario disporre dell'autorizzazione CREATE PROCEDURE per il database e dell'autorizzazione ALTER per lo schema in cui la stored procedure viene creata.  
  
 `sp_recompile` Stored Procedure di sistema  
 È richiesta l'autorizzazione ALTER per la stored procedure specificata.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>Per ricompilare una stored procedure utilizzando l'opzione WITH RECOMPILE  
  
1.  Connettersi al [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio seguente viene creata la definizione della stored procedure.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>Per ricompilare una stored procedure utilizzando l'opzione WITH RECOMPILE  
  
1.  Connettersi al [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene creata una stored procedure semplice tramite cui vengono restituiti tutti i dipendenti (per cui vengono indicati il nome e il cognome), le relative posizioni e i nomi dei reparti di appartenenza da una vista.  
  
     Successivamente, copiare e incollare il secondo esempio di codice nella finestra Query, quindi fare clic su **Esegui**. Verrà eseguita la stored procedure e verrà ricompilato il piano di query della stored procedure.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sprecompile"></a>Per ricompilare una stored procedure utilizzando sp_recompile  
  
1.  Connettersi al [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene creata una stored procedure semplice tramite cui vengono restituiti tutti i dipendenti (per cui vengono indicati il nome e il cognome), le relative posizioni e i nomi dei reparti di appartenenza da una vista.  
  
     Successivamente, copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. La stored procedure non verrà eseguita, ma contrassegnata per la ricompilazione in modo che il relativo piano di query venga aggiornata alla successiva esecuzione della stored procedure.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stored procedure](../stored-procedures/create-a-stored-procedure.md)   
 [Modificare una stored procedure](../stored-procedures/modify-a-stored-procedure.md)   
 [Rinominare una stored procedure](rename-a-stored-procedure.md)   
 [Visualizzare la definizione di una stored procedure](view-the-definition-of-a-stored-procedure.md)   
 [Visualizzare le dipendenze di una stored procedure](view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)  
  
  
