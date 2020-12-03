---
description: Trigger DDL
title: Trigger DDL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e4e723b2ef95fa3b1916d972a5b911dda5201a3d
ms.sourcegitcommit: 644223c40af7168f9d618526e9f4cd24e115d1db
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328061"
---
# <a name="ddl-triggers"></a>Trigger DDL
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  I trigger DDL vengono eseguiti in risposta a vari eventi DDL (Data Definition Language), Questi eventi corrispondono principalmente a istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che iniziano con le parole chiave CREATE, ALTER, DROP, GRANT, DENY, REVOKE o UPDATE STATISTICS. Alcune stored procedure di sistema che eseguono operazioni di tipo DDL possono inoltre attivare trigger DDL.  
  
 Utilizzare trigger DDL nei casi seguenti:  
  
-   Impedire modifiche specifiche nello schema di database.  
  
-   Fare in modo che nel database si verifichi un cambiamento in risposta a una modifica nello schema di database.  
  
-   Registrare modifiche o eventi nello schema di database.  
  
> [!IMPORTANT]  
>  Testare i trigger DDL per determinarne la risposta alle stored procedure di sistema eseguite. Sia l'istruzione CREATE TYPE che la stored procedure **sp_addtype** , ad esempio, attivano un trigger DDL creato in un evento CREATE_TYPE.  
  
## <a name="types-of-ddl-triggers"></a>Tipi di trigger DDL  
 ### <a name="transact-sql-ddl-trigger"></a>Trigger DDL di Transact-SQL  
 Un tipo speciale di stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] che esegue una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] in risposta a un evento con ambito server o con ambito database. Ad esempio, è possibile che un trigger DDL si attivi se viene eseguita un'istruzione come ALTER SERVER CONFIGURATION o se una tabella viene eliminata tramite DROP TABLE.  
  
 ### <a name="clr-ddl-trigger"></a>Trigger CLR DDL  
 Anziché eseguire una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] , un trigger CLR consente di eseguire uno o più metodi scritti in codice gestito che sono membri di un assembly creato in .NET Framework e caricato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I trigger DDL vengono attivati solo in seguito all'esecuzione delle istruzioni DDL che li hanno generati I trigger DDL non possono essere utilizzati come trigger INSTEAD OF. I trigger DDL non vengono attivati in risposta a eventi che interessano stored procedure e tabelle temporanee globali o locali.  
  
 I trigger DDL non creano le tabelle **inserted** e **deleted** .  
  
 Le informazioni relative a un evento che attiva un trigger DDL e le successive modifiche provocate dal trigger vengono acquisite mediante la funzione EVENTDATA.  
  
 Più trigger da creare per ogni evento DDL.  
  
 Diversamente dai trigger DML, i trigger DDL non sono definiti a livello di ambito di schema. Pertanto, non è possibile utilizzare funzioni quali OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY e OBJECTPROPERTYEX durante l'esecuzione di query sui metadati relativi ai trigger DDL. Utilizzare in alternativa le viste del catalogo.  
  
 I trigger DDL con ambito server sono disponibili in Esplora oggetti di SQL Server Management Studio nella cartella **Trigger** all'interno della cartella **Oggetti server** . I trigger DDL con ambito database sono disponibili nella cartella **Trigger database** all'interno della cartella **Programmabilità** del database corrispondente.  
  
> [!IMPORTANT]  
>  L'innalzamento di livello dei privilegi consente l'esecuzione di malware all'interno dei trigger. Per altre informazioni su come limitare tale minaccia, vedere [Gestione della sicurezza dei trigger](../../relational-databases/triggers/manage-trigger-security.md).  
  
## <a name="ddl-trigger-scope"></a>Ambito del trigger DDL  
 I trigger DDL vengono attivati in risposta a un evento [!INCLUDE[tsql](../../includes/tsql-md.md)] elaborato nel database o nel server corrente. L'ambito del trigger dipende dall'evento. Ad esempio, un trigger DDL creato in modo da essere attivato in risposta a un evento CREATE_TABLE può essere attivato ogni volta che nel database o nell'istanza del server si verifica un evento CREATE_TABLE. Un trigger DDL creato in modo da essere attivato in risposta a un evento CREATE_LOGIN può essere attivato solo quando si verifica un evento CREATE_LOGIN nell'istanza del server.  
  
 Nell'esempio seguente il trigger DDL `safety` viene attivato ogni volta che nel database si verifica un evento `DROP_TABLE` o `ALTER_TABLE` :  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 Nell'esempio seguente un trigger DDL consente di visualizzare un messaggio se nell'istanza corrente del server si verifica un evento `CREATE_DATABASE` . Nell'esempio viene utilizzata la funzione `EVENTDATA` per recuperare il testo dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente. Per altre informazioni sull'uso di EVENTDATA con i trigger DDL, vedere [Utilizzo della funzione EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 Per accedere agli elenchi in cui viene eseguito il mapping tra le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e gli ambiti che possono essere specificati per tali istruzioni, utilizzare i collegamenti disponibili nella sezione "Selezione di un'istruzione DDL specifica per l'attivazione di un trigger DDL" di seguito in questo argomento.  
  
 I trigger DDL definiti a livello di ambito di database sono archiviati come oggetti nel database in cui vengono creati. È possibile creare nel database **master** trigger DDL con un funzionamento analogo a quello dei trigger creati nei database progettati dall'utente. È possibile ottenere informazioni sui trigger DDL eseguendo una query sulla vista del catalogo **sys.triggers** . È possibile eseguire una query su **sys.triggers** nel contesto di database in cui vengono creati i trigger oppure specificando il nome del database come identificatore, ad esempio **master.sys.triggers**.  
  
 I trigger DDL definiti a livello di ambito di server sono archiviati come oggetti nel database **master** . È tuttavia possibile ottenere informazioni sui trigger DDL con ambito server eseguendo una query sulla vista del catalogo **sys.server_triggers** in qualsiasi contesto di database.  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>Specifica di un'istruzione o di un gruppo di istruzioni Transact-SQL  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>Selezione di un'istruzione DDL specifica per l'attivazione di un trigger DDL  
 È possibile progettare i trigger DDL in modo che vengano attivati dopo l'esecuzione di una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] specifiche. Nell'esempio precedente, il trigger `safety` viene attivato dopo un evento `DROP_TABLE` o `ALTER_TABLE` . Per un elenco delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che è possibile specificare per attivare un trigger e informazioni sull'ambito in cui ciascun trigger può essere attivato, vedere [Eventi DDL](../../relational-databases/triggers/ddl-events.md).  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>Selezione di un gruppo predefinito di istruzioni DDL per l'attivazione di un trigger DDL  
 Un trigger DDL può essere attivato dopo l'esecuzione di qualsiasi evento [!INCLUDE[tsql](../../includes/tsql-md.md)] appartenente a un raggruppamento predefinito di eventi simili. Se, ad esempio, si desidera che un trigger DDL venga attivato dopo l'esecuzione di qualsiasi istruzione CREATE TABLE, ALTER TABLE o DROP TABLE, è possibile specificare FOR DDL_TABLE_EVENTS nell'istruzione CREATE TRIGGER. Dopo l'esecuzione di CREATE TRIGGER, gli eventi inclusi in un gruppo di eventi verranno aggiunti alla vista del catalogo **sys.trigger_events** .  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]se un trigger viene creato in un gruppo di eventi, **sys.trigger_events** non include informazioni sul gruppo di eventi. In **sys.trigger_events** sono incluse solo informazioni sui singoli eventi inclusi nel gruppo in questione. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, **sys.trigger_events** rende persistenti i metadati relativi al gruppo di eventi nel quale sono creati i trigger, nonché quelli relativi ai singoli eventi inclusi nel gruppo di eventi. Le modifiche agli eventi inclusi nei gruppi di eventi in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive non vengono pertanto applicate ai trigger DDL creati in tali gruppi di eventi in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Per un elenco dei gruppi predefiniti di istruzioni DDL disponibili per i trigger DDL e per informazioni sulle istruzioni specifiche incluse nei gruppi di eventi e sugli ambiti in cui è possibile programmare tali gruppi, vedere [Gruppi di eventi DDL](../../relational-databases/triggers/ddl-event-groups.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Argomento|  
|----------|-----------|  
|Vengono descritte le procedure di creazione, modifica e disabilitazione dei trigger DDL.|[Implementare trigger DDL](../../relational-databases/triggers/implement-ddl-triggers.md)|  
|Viene illustrato come creare un trigger CLR DDL.|[Creazione di trigger CLR](../../relational-databases/triggers/create-clr-triggers.md)|  
|Viene descritto come restituire informazioni sui trigger DDL.|[Ottenere informazioni sui trigger DDL](../../relational-databases/triggers/get-information-about-ddl-triggers.md)|  
|Viene descritto come restituire informazioni relative a un evento che attiva un trigger DDL utilizzando la funzione EVENTDATA.|[Utilizzo della funzione EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md)|  
|Viene descritto come gestire la sicurezza dei trigger.|[Gestione della sicurezza dei trigger](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DML](../../relational-databases/triggers/dml-triggers.md)   
 [Trigger LOGON](../../relational-databases/triggers/logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
 [EVENT DATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
