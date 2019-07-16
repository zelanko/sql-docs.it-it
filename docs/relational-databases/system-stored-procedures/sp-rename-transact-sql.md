---
title: sp_rename (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs:
- TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 070c2a362a69fb6863cc263da3975efc66c7c9f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006937"
---
# <a name="sprename-transact-sql"></a>sp_rename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Consente di modificare il nome di un oggetto creato dall'utente nel database corrente. Questo oggetto può essere una tabella, indice, colonna, tipo di dati alias oppure [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] definite dall'utente tipo di common language runtime (CLR).  
  
> [!CAUTION]  
>  La modifica di una parte del nome di un oggetto potrebbe compromettere il funzionamento di script e stored procedure. È consigliabile evitare di utilizzare questa istruzione per rinominare stored procedure, trigger, funzioni definite dall'utente o viste. In alternativa, eliminare l'oggetto e ricrearlo con il nuovo nome.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [ @objname =] '*object_name*'  
 Nome corrente completo o non qualificato dell'oggetto utente o del tipo di dati. Se l'oggetto da rinominare è una colonna in una tabella, *object_name* deve essere nel formato *Table. Column* oppure *schema.table.column*. Se l'oggetto da rinominare è un indice *object_name* deve essere nel formato *Table. index* oppure *schema.table.index*. Se l'oggetto da rinominare è un vincolo *object_name* deve essere nel formato *schema.constraint*.  
  
 Le virgolette sono necessarie solo se viene specificato un nome di oggetto completo. Nel caso di un nome completo, ovvero contenente un nome di database, il nome del database deve corrispondere a quello del database corrente. *object_name* viene **nvarchar(776)** , non prevede alcun valore predefinito.  
  
 [ @newname =] '*new_name*'  
 Nuovo nome dell'oggetto specificato. *new_name* deve essere un nome composto da una parte e devono rispettare le regole per gli identificatori. *newname* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!NOTE]  
>  I nomi di trigger non possono iniziare con # o ##.  
  
 [ @objtype =] '*object_type*'  
 Tipo dell'oggetto da rinominare. *object_type* viene **varchar(13)** , con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|COLUMN|Colonna da rinominare.|  
|DATABASE|Database definito dall'utente. Quando si rinomina un database è necessario specificare questo tipo di oggetto.|  
|INDEX|Indice definito dall'utente. Se si rinomina un indice con statistiche, vengono automaticamente rinominate anche le statistiche.|  
|OBJECT|Un elemento di un tipo registrato in [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). È ad esempio possibile utilizzare OBJECT per rinominare oggetti che includono vincoli (CHECK, FOREIGN KEY, PRIMARY/UNIQUE KEY), tabelle utente e regole.|  
|STATISTICS|**Si applica a** : da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Statistiche create in modo esplicito da un utente o in modo implicito con un indice. Se si rinominano le statistiche di un indice, viene automaticamente rinominato anche l'indice.|  
|USERDATATYPE|Oggetto [i tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) aggiunti tramite l'istruzione [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) oppure [sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md).|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo)  
  
## <a name="remarks"></a>Note  
 È possibile modificare il nome di un oggetto o un tipo di dati solo nel database corrente. I nomi della maggior parte dei tipi di dati e degli oggetti di sistema non sono modificabili.  
  
 La stored procedure sp_rename rinomina automaticamente l'indice associato ogni volta che viene rinominato un vincolo PRIMARY KEY o UNIQUE. Se un indice rinominato è associato a un vincolo PRIMARY KEY, quando si esegue sp_rename viene rinominato automaticamente anche il vincolo PRIMARY KEY.  
  
 La stored procedure sp_rename può essere utilizzata per rinominare indici XML primari e secondari.  
  
 Ridenominazione di una stored procedure, funzione, vista o trigger non modificherà il nome dell'oggetto corrispondente nella colonna definition della [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista del catalogo o ottenuto usando la [Object DEFINIZIONE](../../t-sql/functions/object-definition-transact-sql.md) funzione predefinita. È pertanto consigliabile evitare di utilizzare sp_rename per rinominare questi tipi di oggetto. In alternativa, eliminare e ricreare l'oggetto con il nuovo nome.  
  
 La ridenominazione di un oggetto, ad esempio una tabella o una colonna, non aggiorna automaticamente i riferimenti a tale oggetto ed è necessario modificare manualmente tutti gli oggetti che fanno riferimento all'oggetto rinominato. Se, ad esempio, si rinomina una colonna di una tabella a cui viene fatto riferimento all'interno di un trigger, è necessario modificare il trigger in base al nuovo nome della colonna. Usare [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) per elencare le dipendenze dall'oggetto prima di rinominarlo.  
  
## <a name="permissions"></a>Permissions  
 Per rinominare oggetti, colonne e indici, è necessario disporre dell'autorizzazione ALTER per l'oggetto. Per rinominare tipi definiti dall'utente, è necessario disporre dell'autorizzazione CONTROL per il tipo. Per rinominare un database, è richiesta l'appartenenza al ruolo predefinito del server sysadmin o dbcreator.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-renaming-a-table"></a>R. Ridenominazione di una tabella  
 Nell'esempio seguente la tabella `SalesTerritory` viene rinominata in `SalesTerr` nello schema `Sales` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>B. Ridenominazione di una colonna  
 Nell'esempio seguente viene rinominato il `TerritoryID` colonna il `SalesTerritory` alla tabella `TerrID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. Ridenominazione di un indice  
 Nell'esempio seguente l'indice `IX_ProductVendor_VendorID` viene rinominato in `IX_VendorID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. Ridenominazione di un tipo di dati alias  
 Nell'esempio seguente il tipo di dati alias `Phone` viene rinominato in `Telephone`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. Ridenominazione dei vincoli  
 Negli esempi seguenti vengono rinominati un vincolo PRIMARY KEY, un vincolo CHECK e un vincolo FOREIGN KEY. Quando si rinomina un vincolo, è necessario specificare lo schema di appartenenza del vincolo.  
  
```  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. Ridenominazione delle statistiche  
 Nell'esempio seguente crea un oggetto statistiche denominato contactMail1 e successivamente vengono rinominate le statistiche al nuovo contatto tramite sp_rename. Quando si rinominano le statistiche, l'oggetto deve essere specificato nel formato schema.table.statistics_name.  
  
```  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
