---
title: Traduzione automatica dei dati dei caratteri Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297881"
---
# <a name="autotranslation-of-character-data"></a>Conversione automatica dei dati di tipo carattere
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  I dati di tipo carattere, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le variabili di carattere ANSI dichiarate con SQL_C_CHAR o i dati archiviati in utilizzando i tipi di dati **char**, **varchar**o **text** , possono rappresentare solo un numero limitato di caratteri. I dati di tipo carattere archiviati utilizzando un byte per carattere possono rappresentare solo 256 caratteri. I valori archiviati nelle variabili SQL_C_CHAR vengono interpretati mediante la tabella codici ANSI (ACP) del computer client. I valori archiviati utilizzando tipi di dati **char**, **varchar**o **text** sul server vengono valutati utilizzando i dati ACP del server.  
  
 Se sia il server che il client hanno lo stesso ACP, non hanno problemi nell'interpretare i valori archiviati in SQL_C_CHAR, **char**, **varchar**o oggetti **di testo.** Se il server e il client hanno aCP diversi, SQL_C_CHAR dati dal client possono essere interpretati come un carattere diverso sul server se vengono utilizzati in **char**, **varchar**o colonne di **testo,** variabili o parametri. Ad esempio, un byte di carattere contenente il valore 0xA5 viene interpretato come il carattere , in un computer che utilizza la tabella codici 437, e viene interpretato come il simbolo dello yen (-) su un computer che esegue la tabella codici 1252.  
  
 I dati Unicode vengono archiviati utilizzando due byte per carattere. Poiché tutti i caratteri estesi sono inclusi nella specifica Unicode, tutti i caratteri Unicode vengono interpretati allo stesso modo da tutti i computer.  
  
 La funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] traduzione automatica del driver ODBC Native Client tenta di ridurre al minimo i problemi nello spostamento di dati di tipo carattere tra un client e un server che dispongono di tabelle codici diverse. AutoTranslate può essere impostato nella stringa di connessione di [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), nella stringa di configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)o durante la configurazione di origini dati per il driver ODBC Native Client utilizzando l'Amministratore ODBC.  
  
 Quando AutoTranslate è impostato su "no", non vengono eseguite conversioni sui dati spostati tra SQL_C_CHAR variabili sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client **e**char , **varchar**o colonne di **testo,** variabili o parametri in un database. Se i dati contengono caratteri estesi e i due computer dispongono di tabelle codici diverse, gli schemi di bit potrebbero essere interpretati in modo diverso sui computer client e server. I dati verranno interpretati nello stesso modo se entrambi computer dispongono della stessa tabella codici.  
  
 Quando AutoTranslate è impostato su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "yes", il driver ODBC Native Client utilizza Unicode per convertire i dati spostati tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_C_CHAR variabili nel client e **char**, **varchar**o colonne di **testo,** variabili o parametri in un database:  
  
-   Quando i dati vengono inviati da una variabile SQL_C_CHAR sul client a una **colonna,** una variabile o un parametro di testo char , **varchar**o **text** in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, il driver ODBC converte prima da SQL_C_CHAR in Unicode utilizzando l'ACP del client, quindi da Unicode a carattere utilizzando l'ACP del server.  
  
-   Quando i dati vengono inviati da una colonna **char**, **varchar**o da una colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di **testo,** una variabile o un parametro di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database a una variabile SQL_C_CHAR sul client, il driver ODBC Native Client converte prima da carattere a Unicode utilizzando l'ACP del server, quindi da Unicode a SQL_C_CHAR utilizzando l'ACP del client.  
  
 Poiché tutte queste conversioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono eseguite dal driver ODBC Native Client in esecuzione sul client, il server ACP deve essere una delle tabelle codici installate nel computer client.  
  
 L'utilizzo di Unicode consente di eseguire la conversione più appropriata di tutti i caratteri presenti in entrambe le tabelle codici. Se tuttavia un carattere esiste in una tabella codici ma non in un'altra, non può essere rappresentato nella tabella codici di destinazione. Il simbolo del marchio registrato (®), ad esempio, è presente nella tabella codici 1252, ma non nella tabella codici 437.  
  
 L'impostazione di AutoTranslate non ha effetto sulle conversioni seguenti:  
  
-   Spostamento dei dati tra le variabili client di SQL_C_CHAR carattere e le colonne, variabili o i parametri Unicode **nchar**, **nvarchar**o **ntext** nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
-   Lo spostamento di dati tra Unicode SQL_C_WCHAR variabili client e **caratteri char**, **varchar**o colonne di **testo,** variabili o parametri nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
 I dati devono essere sempre convertiti nel passaggio da carattere a Unicode.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBCProcessing Results &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
