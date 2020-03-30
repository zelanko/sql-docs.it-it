---
title: GO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GO
- GO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
author: rothja
ms.author: jroth
ms.openlocfilehash: 48bca691f10822176c5169cf6bf9a052d7675478
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68072301"
---
# <a name="sql-server-utilities-statements---go"></a>Istruzioni delle utilità SQL Server - GO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono forniti comandi che non rappresentano istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)], ma che vengono riconosciuti dalle utilità **sqlcmd** e **osql** e dall'editor del codice di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Questi comandi possono essere utilizzati per facilitare la leggibilità e l'esecuzione di batch e script.  
  
  GO contrassegna la fine di un batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] per le utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
GO [count]  
```  
  
## <a name="arguments"></a>Argomenti  
 *count*  
 Numero integer positivo. Il batch che precede GO verrà eseguito il numero specificato di volte.  
  
## <a name="remarks"></a>Osservazioni  
 GO non è un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)], ma un comando riconosciuto dalle utilità **sqlcmd** e **osql** e dall'editor del codice di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Il comando GO viene interpretato dalle utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come un segnale per l'invio del batch corrente di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il batch di istruzioni corrente è composto da tutte le istruzioni immesse dopo l'ultima esecuzione del comando GO oppure dopo l'avvio della sessione ad hoc o dello script se si tratta della prima esecuzione di GO.  
  
 Non è possibile specificare un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] nella stessa riga di un comando GO. La riga, tuttavia, può includere commenti.  
  
 Gli utenti devono seguire le regole per i batch. Per l'esecuzione di una stored procedure dopo la prima istruzione di un batch, ad esempio, è necessario includere la parola chiave EXECUTE. L'ambito delle variabili locali definite dall'utente è limitato a un batch e non è possibile fare riferimento a tali variabili dopo l'esecuzione del comando GO.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 Le applicazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono inviare più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] affinché vengano eseguite come batch. Le istruzioni del batch vengono quindi compilate in un unico piano di esecuzione. I programmatori che eseguono istruzioni ad hoc nelle utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure compilano script di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire tramite le utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano il comando GO per segnalare la fine di un batch.  
  
 Nelle applicazioni basate sulle API ODBC o OLE DB i tentativi di esecuzione del comando GO provocano un errore di sintassi. Le utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non inviano mai un comando GO al server.  
  
 Non usare un punto e virgola come carattere di terminazione dopo GO.
 
```
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```
  
## <a name="permissions"></a>Autorizzazioni  
 GO è un comando di utilità che non richiede autorizzazioni e può essere eseguito da qualsiasi utente.    
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono creati due batch. Il primo contiene solo un'istruzione `USE AdventureWorks2012` per l'impostazione del contesto del database. Nelle restanti istruzioni viene utilizzata una variabile locale. Pertanto, tutte le dichiarazioni della variabile locale devono essere raggruppate in un singolo batch. A tale scopo, è necessario inserire il comando `GO` solo dopo l'ultima istruzione che fa riferimento alla variabile.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 Nell'esempio seguente vengono eseguite due volte le istruzioni del batch.  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
