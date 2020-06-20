---
title: Impostare o modificare le regole di confronto delle colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 05b8211569b6ce83faaec043e5eb527a60f0ddab
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970559"
---
# <a name="set-or-change-the-column-collation"></a>Impostare o modificare le regole di confronto delle colonne
  È possibile ignorare le regole di confronto del database per i dati `char`, `varchar`, `text`, `nchar`, `nvarchar` e `ntext` specificando regole di confronto diverse per una colonna specifica di una tabella e utilizzando uno degli elementi seguenti:  
  
-   Clausola COLLATE di [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) e [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql). Ad esempio:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Regole di confronto e supporto Unicode](collation-and-unicode-support.md).  
  
-   Utilizzo della `Column.Collation` Proprietà in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMO (Management Objects).  
  
 Non è possibile modificare le regole di confronto di una colonna a cui fa riferimento uno qualsiasi degli elementi seguenti:  
  
-   Una colonna calcolata  
  
-   Un indice  
  
-   Le statistiche di distribuzione, generate automaticamente o tramite l'istruzione CREATE STATISTICS  
  
-   Un vincolo CHECK  
  
-   Un vincolo FOREIGN KEY  
  
 Quando si usa il database **tempdb**, la clausola [COLLATE](/sql/t-sql/statements/collations) include un'opzione *database_default* per specificare che una colonna di una tabella temporanea utilizza le regole di confronto predefinite del database utente corrente per la connessione anziché quelle del database **tempdb**.  
  
## <a name="collations-and-text-columns"></a>Regole di confronto e colonne di tipo text  
 È possibile inserire o aggiornare valori in una colonna `text` le cui regole di confronto sono diverse dalla tabella codici delle regole di confronto predefinite del database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte in modo implicito i valori nelle regole di confronto della colonna.  
  
## <a name="collations-and-tempdb"></a>Regole di confronto e database tempdb  
 Il database **tempdb** viene compilato a ogni avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e presenta le stesse regole di confronto predefinite del database **model** . Queste sono generalmente le stesse regole di confronto predefinite dell'istanza. Se si crea un database utente e si specificano regole di confronto predefinite diverse da quelle del database **model**, il database utente utilizzerà regole di confronto predefinite diverse da quelle di **tempdb**. Tutte le stored procedure temporanee o le tabelle temporanee vengono create e archiviate in **tempdb**. Di conseguenza, tutte le colonne implicite delle tabelle temporanee e tutte le costanti, le variabili e i parametri a cui possono essere assegnati valori predefiniti e che si trovano in stored procedure temporanee, utilizzano regole di confronto diverse da quelle degli oggetti analoghi creati in tabelle e stored procedure permanenti.  
  
 Ciò può causare problemi derivanti da una non corrispondenza nelle regole di confronto tra i database definiti dall'utente e gli oggetti di database del sistema. Si supponga ad esempio che un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzi le regole di confronto Latin1_General_CS_AS e di eseguire le seguenti istruzioni:  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 In questo sistema nel database **tempdb** vengono utilizzate le regole di confronto Latin1_General_CS_AS con la tabella codici 1252, mentre in `TestDB` e `TestPermTab.Col1` vengono utilizzate le regole di confronto `Estonian_CS_AS` con la tabella codici 1257. Ad esempio:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Con l'esempio precedente, il database **tempdb** utilizza le regole di confronto Latin1_General_CS_AS, mentre `TestDB` e `TestTab.Col1` utilizzano le regole di confronto `Estonian_CS_AS` . Ad esempio:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Poiché **tempdb** utilizza le regole di confronto predefinite del server e `TestPermTab.Col1` utilizza regole di confronto diverse, in SQL Server viene restituito un errore in cui viene indicato che è impossibile risolvere il conflitto delle regole di confronto tra Latin1_General_CI_AS_KS_WS ed Estonian_CS_AS nell'operazione.  
  
 Per evitare l'errore è possibile utilizzare una delle alternative seguenti:  
  
-   Specificare che per la colonna della tabella temporanea siano utilizzate le regole di confronto predefinite del database utente, anziché quelle del database **tempdb**. Ciò consente alla tabella temporanea di utilizzare tabelle con formattazione simile in più database, se ciò è richiesto dal sistema.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Specificare le regole di confronto corrette per la colonna `#TestTempTab` :  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare o modificare le regole di confronto del server](set-or-change-the-server-collation.md)   
 [Impostare o modificare le regole di confronto del database](set-or-change-the-database-collation.md)   
 [Regole di confronto e supporto Unicode](collation-and-unicode-support.md)  
  
  
