---
title: Usare la funzione EVENTDATA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a34a3e69e157894b29db48da19f44d1e35dad746
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405677"
---
# <a name="use-the-eventdata-function"></a>Utilizzo della funzione EVENTDATA
  La funzione EVENTDATA consente di acquisire le informazioni relative a un evento che attiva un trigger DDL. La funzione restituisce un valore `xml`. XML Schema include le informazioni relative a:  
  
-   Ora dell'evento.  
  
-   ID di processo di sistema (SPID) della connessione nel momento in cui è stato eseguito il trigger.  
  
-   Tipo di evento che ha attivato il trigger.  
  
 In base al tipo di evento, lo schema include informazioni aggiuntive quali il database nel quale è stato generato l'evento, l'oggetto per il quale è stato generato l'evento e l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] dell'evento. Per altre informazioni, vedere [Trigger DDL](ddl-triggers.md).  
  
 Si supponga che nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] venga creato il trigger DDL seguente:  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 Viene quindi eseguita l'istruzione `CREATE TABLE` seguente:  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 L'istruzione `EVENTDATA()` nel trigger DDL acquisisce il testo dell'istruzione `CREATE TABLE` , che non è consentita. Questo risultato viene ottenuto tramite un'istruzione XQuery sui `xml` i dati generati da EVENTDATA e viene recuperato il \<CommandText > elemento. Per altre informazioni, vedere [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server).  
  
> [!CAUTION]  
>  EVENTDATA acquisisce i dati degli eventi CREATE_SCHEMA e, se presente, il contenuto di <schema_element> della definizione CREATE SCHEMA corrispondente. Riconosce inoltre la definizione <schema_element> come evento separato. Un trigger DDL creato in un evento CREATE_SCHEMA e un evento rappresentato dal contenuto di <schema_element> della definizione CREATE SCHEMA possono pertanto restituire due volte gli stessi dati di evento, ad esempio i dati `TSQLCommand`. Si consideri ad esempio la creazione di un trigger DDL su entrambi gli eventi CREATE_SCHEMA e CREATE_TABLE e la successiva esecuzione del batch seguente:  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  È importante tenere presente che, se l'applicazione recupera i dati `TSQLCommand` dell'evento CREATE_TABLE, è possibile che i dati vengano visualizzati due volte: alla generazione dell'evento CREATE_SCHEMA e di nuovo alla generazione dell'evento CREATE_TABLE. Evitare di creare trigger DDL sia per gli eventi CREATE_SCHEMA che per i testi <schema_element> di qualsiasi definizione CREATE SCHEMA corrispondente oppure compilare nell'applicazione una logica che impedisca la doppia elaborazione dello stesso evento.  
  
## <a name="alter-table-and-alter-database-events"></a>Eventi ALTER TABLE e ALTER DATABASE  
 I dati degli eventi ALTER_TABLE e ALTER_DATABASE includono anche i nomi e i tipi degli altri oggetti interessati dall'istruzione DDL e dall'azione eseguita su questi oggetti. I dati degli eventi ALTER_TABLE includono i nomi delle colonne, dei vincoli o dei trigger interessati dall'istruzione ALTER TABLE e dall'azione (creazione, modifica, rimozione, abilitazione o disabilitazione) eseguita su tali oggetti. I dati degli eventi ALTER_DATABASE includono i nomi di tutti i file o i filegroup interessati dall'istruzione ALTER DATABASE e dall'azione (creazione, modifica o rimozione) eseguita su tali oggetti.  
  
 Creare, ad esempio, il trigger DDL seguente nel database di esempio AdventureWorks:  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 Eseguire quindi l'istruzione ALTER TABLE seguente che viola un vincolo:  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 L'istruzione EVENTDATA() nel trigger DDL acquisisce il testo dell'istruzione `ALTER TABLE` , che non è consentita.  
  
## <a name="example"></a>Esempio  
 È possibile utilizzare la funzione EVENTDATA per creazione di un log eventi. Nell'esempio seguente viene creata una tabella per l'archiviazione delle informazioni relative agli eventi. Viene quindi creato nel database corrente un trigger DDL che popola la tabella con le informazioni seguenti ogni volta che viene generato un evento DDL a livello del database:  
  
-   Ora dell'evento (tramite la funzione GETDATE).  
  
-   Utente del database che ha attivato la sessione durante la quale è stato generato l'evento (tramite la funzione CURRENT_USER).  
  
-   Tipo di evento.  
  
-   Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] inclusa nell'evento.  
  
 Anche in questo caso, per l'acquisizione degli ultimi due elementi viene utilizzato XQuery per i dati `xml` generati da EVENTDATA.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  Per la restituzione di dati sugli eventi è consigliabile utilizzare il metodo XQuery `value()` anziché il metodo `query()`. Il metodo `query()` restituisce output XML con le istanze CR/LF (ritorno a capo/avanzamento riga) trasformate con il carattere di escape e commerciale (&), mentre il metodo `value()` rende le istanze CR/LF invisibili nell'output.  
  
 Un esempio simile di trigger DDL è disponibile nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Per visualizzare l'esempio, individuare la cartella Trigger database utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Questa cartella si trova all'interno della cartella **Programmabilità** del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Fare doppio clic su **ddlDatabaseTriggerLog** e selezionare **crea Script per Trigger Database come**. Per impostazione predefinita, i trigger DDL **ddlDatabaseTriggerLog** è disabilitato.  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi DDL](../triggers/ddl-events.md)   
 [Gruppi di eventi DDL](../triggers/ddl-event-groups.md)  
  
  
