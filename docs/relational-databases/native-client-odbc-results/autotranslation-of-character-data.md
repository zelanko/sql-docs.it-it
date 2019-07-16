---
title: Unite dati di tipo carattere | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0e5ff3b73bfab224d21c35d1eff801df487b327
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937147"
---
# <a name="autotranslation-of-character-data"></a>Conversione automatica dei dati di tipo carattere
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dati di tipo carattere, ad esempio ANSI carattere variabili dichiarate con SQL_C_CHAR o i dati archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando il **char**, **varchar**, o **testo** tipi di dati, possono rappresentano solo un numero limitato di caratteri. I dati di tipo carattere archiviati utilizzando un byte per carattere possono rappresentare solo 256 caratteri. I valori archiviati nelle variabili SQL_C_CHAR vengono interpretati mediante la tabella codici ANSI (ACP) del computer client. I valori archiviati utilizzando **char**, **varchar**, o **testo** i tipi di dati sul server vengono valutati tramite degli Stati ACP del server.  
  
 Se il server e i client hanno la stessa tabella codici ANSI, quindi non persistono l'interpretazione dei valori archiviati nelle SQL_C_CHAR **char**, **varchar**, o **testo** oggetti. Se il server e il client dispone di ACP differenti, i dati SQL_C_CHAR del client possono essere interpretati come un carattere diverso sul server se viene usata in **char**, **varchar**, o **testo** colonne, variabili o parametri. Ad esempio, un byte di carattere contenente il valore 0xA5 viene interpretato come carattere Ñ su un computer utilizzando codici 437 e viene interpretato come lo yen (¥) in un computer con tabella codici 1252.  
  
 I dati Unicode vengono archiviati utilizzando due byte per carattere. Poiché tutti i caratteri estesi sono inclusi nella specifica Unicode, tutti i caratteri Unicode vengono interpretati allo stesso modo da tutti i computer.  
  
 La funzionalità di AutoTranslate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client tenta di ridurre al minimo i problemi di spostamento di dati carattere tra un client e un server che dispongono di tabelle codici diverse. AutoTranslate può essere impostata nella stringa di connessione di [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), nella stringa di configurazione di [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md), o durante la configurazione delle origini dati per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo Client ODBC driver utilizzando l'amministratore ODBC.  
  
 Quando AutoTranslate è impostata su "no", viene effettuata alcuna conversione sui dati spostati tra le variabili SQL_C_CHAR presenti sul client e **char**, **varchar**, o **testo** colonne, variabili, i parametri in o un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Se i dati contengono caratteri estesi e i due computer dispongono di tabelle codici diverse, gli schemi di bit potrebbero essere interpretati in modo diverso sui computer client e server. I dati verranno interpretati nello stesso modo se entrambi computer dispongono della stessa tabella codici.  
  
 Quando AutoTranslate è impostata su "Sì", il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client utilizza Unicode per convertire i dati spostati tra le variabili SQL_C_CHAR presenti sul client e **char**, **varchar**, oppure **testo** colonne, variabili o parametri in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database:  
  
-   Quando i dati vengono inviati da una variabile SQL_C_CHAR sul client per un **char**, **varchar**, o **testo** colonna, variabile o parametro in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database ODBC driver innanzitutto converte da SQL_C_CHAR a Unicode utilizzando l'ACP del client, quindi da Unicode al carattere utilizzando l'ACP del server.  
  
-   Quando i dati vengono inviati da un **char**, **varchar**, o **testo** colonna, variabile o parametro in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database a una variabile SQL_C_CHAR sul client, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver converte innanzitutto dal carattere a Unicode utilizzando l'ACP del server, quindi da Unicode a SQL_C_CHAR utilizzando l'ACP del client.  
  
 Poiché tutte queste conversioni vengono effettuate la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo Client ODBC driver in esecuzione sul client, il server ACP deve essere una delle pagine codice installate nel computer client.  
  
 L'utilizzo di Unicode consente di eseguire la conversione più appropriata di tutti i caratteri presenti in entrambe le tabelle codici. Se tuttavia un carattere esiste in una tabella codici ma non in un'altra, non può essere rappresentato nella tabella codici di destinazione. Il simbolo del marchio registrato (®), ad esempio, è presente nella tabella codici 1252, ma non nella tabella codici 437.  
  
 L'impostazione di AutoTranslate non ha effetto sulle conversioni seguenti:  
  
-   Spostare dati tra variabili del client SQL_C_CHAR carattere e Unicode **nchar**, **nvarchar**, o **ntext** colonne, variabili o parametri in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
-   Spostare dati tra variabili del client SQL_C_WCHAR Unicode e caratteri **char**, **varchar**, o **testo** colonne, variabili o parametri in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
 I dati devono essere sempre convertiti nel passaggio da carattere a Unicode.  
  
## <a name="see-also"></a>Vedere anche  
 [L'elaborazione dei risultati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
