---
title: 'Esercitazione: Catene di proprietà e cambio di contesto'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1ae566345f722399982c909244e77c564abb7b53
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62524367"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
  In questa esercitazione viene utilizzato uno scenario per illustrare i concetti sulla sicurezza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] relativi a catene di proprietà e cambio di contesto utente.  
  
> [!NOTE]  
>  Per eseguire il codice dell'esercitazione deve essere configurata la sicurezza a modalità mista e deve essere installato il database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Per altre informazioni sulla sicurezza in modalità mista, vedere [Scegliere una modalità di autenticazione](security/choose-an-authentication-mode.md).  
  
## <a name="scenario"></a>Scenario  
 In questo scenario due utenti necessitano degli account per accedere ai dati relativi agli ordini di acquisto archiviati nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . È necessario soddisfare i requisiti seguenti:  
  
-   Il primo account (TestManagerUser) deve essere in grado di visualizzare tutti i dettagli di ogni ordine di acquisto.  
  
-   Il secondo account (TestEmployeeUser) deve essere in grado di visualizzare il numero dell'ordine di acquisto, la data dell'ordine, la data di spedizione, i numeri di serie dei prodotti e gli articoli ordinati e ricevuti per ordine di acquisto, in base al numero di ordine di acquisto, per gli articoli per i quali sono state eseguite spedizioni parziali.  
  
-   Tutti gli altri account devono mantenere le autorizzazioni correnti.  
  
 Per soddisfare i requisiti di questo scenario, l'esempio è suddiviso in quattro parti in cui vengono illustrati i concetti delle catene di proprietà e dello scambio di contesto:  
  
1.  Configurazione dell'ambiente.  
  
2.  Creazione di una stored procedure per l'accesso ai dati in base all'ordine di acquisto.  
  
3.  Accesso ai dati tramite la stored procedure.  
  
4.  Reimpostazione dell'ambiente.  
  
 Ogni blocco di codice dell'esempio è illustrato sulla stessa riga. Per copiare l'esempio completo, vedere [Esempio completo](#CompleteExample) alla fine dell'esercitazione.  
  
## <a name="1-configure-the-environment"></a>1. Configurazione dell'ambiente  
 Utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e il codice seguente per aprire il `AdventureWorks2012` database e utilizzare l' `CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] istruzione per verificare che l'utente dbo venga visualizzato come contesto.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
 Per altre informazioni sull'istruzione CURRENT_USER, vedere [CURRENT_USER &#40;Transact-SQL&#41;](/sql/t-sql/functions/current-user-transact-sql).  
  
 Utilizzare questo codice come utente dbo per creare due utenti nel server e nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
 Per altre informazioni sull'istruzione CREATE USER, vedere [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql). Per altre informazioni sull'istruzione CREATE LOGIN, vedere [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
 Utilizzare il codice seguente per modificare la proprietà dello schema `Purchasing` e impostarla sull'account `TestManagerUser` . In questo modo si consente all'account di utilizzare l'accesso completo alle istruzioni DML (Data Manipulation Language), ad esempio autorizzazioni `SELECT` e `INSERT` , sull'oggetto contenuto. 
  `TestManagerUser` viene inoltre concessa la possibilità di creare stored procedure.  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
 Per altre informazioni sull'istruzione GRANT, vedere [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql). Per altre informazioni sulle stored procedure, vedere [Stored procedure &#40;Motore di database&#41;](stored-procedures/stored-procedures-database-engine.md). Per un poster di tutte [!INCLUDE[ssDE](../includes/ssde-md.md)] le autorizzazioni, [https://go.microsoft.com/fwlink/?LinkId=229142](https://go.microsoft.com/fwlink/?LinkId=229142)vedere.  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2. Creazione di una stored procedure per l'accesso ai dati  
 Per cambiare contesto all'interno di un database, utilizzare l'istruzione EXECUTE AS. EXECUTE AS richiede autorizzazioni IMPERSONATE.  
  
 Utilizzare l'istruzione `EXECUTE AS` del codice seguente per cambiare il contesto impostandolo su `TestManagerUser` e creare una stored procedure in grado di visualizzare soltanto i dati necessari per `TestEmployeeUser`. Per soddisfare i requisiti, la stored procedure accetta una variabile per il numero dell'ordine di acquisto e non visualizza informazioni finanziarie. La clausola WHERE limita inoltre i risultati alle spedizioni parziali.  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
 
  `TestEmployeeUser` non dispone attualmente dell'accesso a qualsiasi oggetto di database. Il codice seguente, ancora nel contesto `TestManagerUser` , concede all'account utente la possibilità di eseguire query sulle informazioni delle tabelle di base tramite la stored procedure.  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
 La stored procedure appartiene allo schema `Purchasing` , nonostante non venga specificato esplicitamente uno schema, poiché `TestManagerUser` è assegnato per impostazione predefinita allo schema `Purchasing` . È possibile utilizzare le informazioni del catalogo di sistema per individuare gli oggetti, come illustrato nel codice seguente.  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
 Al termine di questa sezione dell'esempio, nel codice il contesto viene cambiato e nuovamente impostato su dbo mediante l'istruzione `REVERT`.  
  
```  
REVERT;  
GO  
```  
  
 Per altre informazioni sull'istruzione REVERT, vedere [REVERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/revert-transact-sql).  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3. Accesso ai dati tramite la stored procedure  
 
  `TestEmployeeUser` non dispone di autorizzazioni per gli oggetti di database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ad eccezione dell'accesso e dei diritti assegnati al ruolo di database public. Quando `TestEmployeeUser` tenta di accedere alle tabelle di base, il codice seguente restituisce un errore.  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
 Poiché gli oggetti a cui fa riferimento la stored procedure creata nell'ultima sezione sono di proprietà di `TestManagerUser` in virtù della proprietà dello schema `Purchasing` , `TestEmployeeUser` può accedere alle tabelle di base tramite la stored procedure. Nel codice seguente, in cui viene ancora utilizzato `TestEmployeeUser` come contesto, viene passato l'ordine di acquisto 952 come parametro.  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4. Reimpostazione dell'ambiente  
 Nel codice seguente viene utilizzato il comando `REVERT` per ripristinare `dbo`come contesto dell'account corrente e quindi viene reimpostato l'ambiente.  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
##  <a name="CompleteExample"></a>Esempio completo  
 In questa sezione è riportato il codice completo dell'esempio.  
  
> [!NOTE]  
>  Nel codice non sono inclusi i due errori previsti che dimostrano l'impossibilità per `TestEmployeeUser` di eseguire una selezione nelle tabelle di base.  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
