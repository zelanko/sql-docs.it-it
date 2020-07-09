---
title: DROP DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 917b6aa6dc76a949d5880c14a5c4bb9498f3ae44
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899810"
---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove dal database corrente uno o più valori predefiniti creati dall'utente.  
  
> [!IMPORTANT]
>  L'istruzione DROP DEFAULT verrà rimossa a partire dalla prossima versione di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non utilizzare DROP DEFAULT in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni che attualmente la utilizzano. In alternativa, usare le definizioni di valori predefiniti che è possibile creare con la parola chiave DEFAULT dell'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *IF EXISTS*  
 **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Rimuove in modo condizionale l'impostazione predefinita solo se esiste già.  
  
 *schema_name*  
 Nome dello schema a cui appartiene il valore predefinito.  
  
 *default_name*  
 Nome di un valore predefinito esistente. Per visualizzare un elenco dei valori predefiniti esistenti, eseguire **sp_help**. I valori predefiniti devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md). Il nome dello schema predefinito è facoltativo.  
  
## <a name="remarks"></a>Osservazioni  
 Prima di eliminare un valore predefinito associato a una colonna o un tipo di dati alias, è necessario annullarne l'associazione eseguendo **sp_unbindefault**.  
  
 Se si aggiungono nuove righe senza specificare in modo esplicito un valore dopo avere eliminato un valore predefinito da una colonna che ammette valori Null, in tale posizione verrà inserita la stringa NULL. Se si aggiungono nuove righe senza specificare in modo esplicito un valore dopo avere eliminato un valore predefinito da una colonna NOT NULL, verrà visualizzato un messaggio di errore. Queste righe vengono aggiunte successivamente durante la normale esecuzione dell'istruzione INSERT.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire l'istruzione DROP DEFAULT, è necessario disporre almeno dell'autorizzazione ALTER per lo schema a cui appartiene il valore predefinito.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-dropping-a-default"></a>R. Eliminazione di un valore predefinito  
 Se un valore predefinito non è associato a una colonna o un tipo di dati alias, è possibile eliminarlo semplicemente tramite l'istruzione DROP DEFAULT. Nell'esempio seguente viene rimosso il valore predefinito `datedflt` creato dall'utente.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] è possibile usare la sintassi seguente.  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. Eliminazione di un valore predefinito associato a una colonna  
 Nell'esempio seguente viene disassociato e quindi eliminato il valore predefinito `EmergencyContactPhone` associato alla colonna `Contact` della tabella `phonedflt`.  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
