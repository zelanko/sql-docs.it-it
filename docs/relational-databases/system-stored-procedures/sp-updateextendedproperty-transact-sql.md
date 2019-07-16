---
title: sp_updateextendedproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2f1c1c856cadbb4f005a99d5a5d49dc0c1280a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898422"
---
# <a name="spupdateextendedproperty-transact-sql"></a>sp_updateextendedproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aggiorna il valore di una proprietà estesa esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @name=] {'*property_name*'}  
 Nome della proprietà da aggiornare. *property_name* viene **sysname**, e non può essere NULL.  
  
 [ @value=] {'*valore*'}  
 Valore associato alla proprietà. *valore* viene **sql_variant**, con un valore predefinito è NULL. Il valore pari *valore* potrebbe non essere maggiori di 7.500 byte.  
  
 [ @level0type=] {'*level0_object_type*'}  
 Utente o tipo definito dall'utente. *level0_object_type* viene **varchar(128)** , con un valore predefinito è NULL. I possibili valori sono ASSEMBLY, contratto, EVENT NOTIFICATION, FILEGROUP, tipo di messaggio, funzione di partizione, lo schema di partizione, Guida di piano, REMOTE SERVICE BINDING, ROUTE, SCHEMA, servizio, utente, TRIGGER, tipo e NULL.  
  
> [!IMPORTANT]  
>  I tipi USER e TYPE come tipi di livello 0 verranno rimossi in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate. Utilizzare SCHEMA come tipo di livello 0 anziché USER. Per TYPE utilizzare SCHEMA come tipo di livello 0 e TYPE come tipo di livello 1.  
  
 [ @level0name=] {'*level0_object_name*'}  
 Nome del tipo di oggetto di livello 1 specificato. *level0_object_name* viene **sysname** con valore predefinito è NULL.  
  
 [ @level1type=] {'*level1_object_type*'}  
 Tipo di oggetto di livello 1. *level1_object_type* viene **varchar(128)** con valore predefinito è NULL. I possibili valori sono AGGREGATE, DEFAULT, FUNCTION, LOGICAL FILE NAME, PROCEDURE, QUEUE, RULE, SYNONYM, TABLE, TABLE_TYPE, TYPE, VIEW, XML SCHEMA COLLECTION e NULL.  
  
 [ @level1name=] {'*level1_object_name*'}  
 Nome del tipo di oggetto di livello 1 specificato. *level1_object_name* viene **sysname** con valore predefinito è NULL.  
  
 [ @level2type=] {'*level2_object_type*'}  
 Tipo di oggetto di livello 2. *level2_object_type* viene **varchar(128)** con valore predefinito è NULL. I possibili valori sono COLUMN, CONSTRAINT, EVENT NOTIFICATION, INDEX, PARAMETER, TRIGGER e NULL.  
  
 [ @level2name=] {'*level2_object_name*'}  
 Nome del tipo di oggetto di livello 2 specificato. *level2_object_name* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Ai fini della definizione delle proprietà estese, gli oggetti inclusi in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono classificati in base a tre livelli, ovvero 0, 1 e 2. Il livello 0 è il livello più alto e viene definito come oggetti inclusi nell'ambito del database. Gli oggetti di livello 1 sono inclusi nell'ambito di uno schema o utente, mentre gli oggetti di livello 2 sono contenuti dagli oggetti di livello 1. È possibile definire le proprietà estese per gli oggetti di qualsiasi livello. È necessario qualificare i riferimenti a un oggetto in un livello mediante i nomi degli oggetti proprietari di livello superiore o che li contengono.  
  
 Un valore valido *property_name* e *valore*, se tutti i tipi di oggetto e i nomi sono null, la proprietà aggiornata appartiene al database corrente.  
  
## <a name="permissions"></a>Permissions  
 I membri dei ruoli predefiniti del database db_owner e db_ddladmin possono aggiornare le proprietà estese di qualsiasi oggetto, anche se il ruolo db_ddladmin non può aggiungere proprietà al database stesso oppure a utenti o ruoli.  
  
 Gli utenti possono aggiornare le proprietà estese degli oggetti di cui sono proprietari oppure per i quali dispongono delle autorizzazioni ALTER o CONTROL.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>R. Aggiornamento di una proprietà estesa in una colonna  
 Nell'esempio seguente viene aggiornato il valore della proprietà `Caption` nella colonna `ID` della tabella `T1`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. Aggiornamento di una proprietà estesa in un database  
 Nell'esempio seguente viene innanzitutto creata una proprietà estesa nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e quindi il valore di tale proprietà viene aggiornato.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.fn_listextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sys.extended_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
