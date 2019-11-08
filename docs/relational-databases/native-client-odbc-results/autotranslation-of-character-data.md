---
title: Conversione automatica dei dati di tipo carattere | Microsoft Docs
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
ms.openlocfilehash: c08a0987e11f25c3f5b535d8d26526db5bb14a38
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779173"
---
# <a name="autotranslation-of-character-data"></a>Conversione automatica dei dati di tipo carattere
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  I dati di tipo carattere, ad esempio le variabili di tipo carattere ANSI dichiarati con SQL_C_CHAR o i dati archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando i tipi di dati **char**, **varchar**o **Text** , possono rappresentare solo un numero limitato di caratteri. I dati di tipo carattere archiviati utilizzando un byte per carattere possono rappresentare solo 256 caratteri. I valori archiviati nelle variabili SQL_C_CHAR vengono interpretati mediante la tabella codici ANSI (ACP) del computer client. I valori archiviati utilizzando i tipi di dati **char**, **varchar**o **Text** nel server vengono valutati utilizzando l'ACP del server.  
  
 Se il server e il client hanno lo stesso ACP, non si verificano problemi durante l'interpretazione dei valori archiviati negli oggetti SQL_C_CHAR, **char**, **varchar**o **Text** . Se il server e il client hanno invece diversi, SQL_C_CHAR dati dal client possono essere interpretati come un carattere diverso nel server se usati in colonne, variabili o parametri di tipo **char**, **varchar**o **Text** . Ad esempio, un byte di caratteri contenente il valore 0xA5 viene interpretato come il carattere Ñ in un computer che usa la tabella codici 437 e viene interpretato come il segno di yen (¥) in un computer che esegue la tabella codici 1252.  
  
 I dati Unicode vengono archiviati utilizzando due byte per carattere. Poiché tutti i caratteri estesi sono inclusi nella specifica Unicode, tutti i caratteri Unicode vengono interpretati allo stesso modo da tutti i computer.  
  
 La funzionalità AutoTranslate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client tenta di ridurre al minimo i problemi di trasferimento dei dati di tipo carattere tra un client e un server con tabelle codici diverse. È possibile impostare AutoTranslate nella stringa di connessione di [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), nella stringa di configurazione di [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)o quando si configurano le origini dati per il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client mediante l'amministratore ODBC.  
  
 Quando AutoTranslate è impostato su "No", non vengono eseguite conversioni sui dati spostati tra SQL_C_CHAR variabili nelle colonne client e **char**, **varchar**o **Text** , variabili o parametri di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se i dati contengono caratteri estesi e i due computer dispongono di tabelle codici diverse, gli schemi di bit potrebbero essere interpretati in modo diverso sui computer client e server. I dati verranno interpretati nello stesso modo se entrambi computer dispongono della stessa tabella codici.  
  
 Quando AutoTranslate è impostato su "Yes", il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client utilizza Unicode per convertire i dati spostati tra SQL_C_CHAR variabili nelle colonne client e **char**, **varchar**o **Text** , variabili o parametri di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database  
  
-   Quando i dati vengono inviati da una variabile SQL_C_CHAR sul client a una colonna **char**, **varchar**o **Text** , una variabile o un parametro in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il driver ODBC converte prima di tutto da SQL_C_CHAR a Unicode utilizzando l'ACP del client , quindi da Unicode di nuovo a carattere utilizzando l'ACP del server.  
  
-   Quando i dati vengono inviati da una colonna, una variabile o un parametro di tipo **char**, **varchar**o **text** in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una variabile SQL_C_CHAR sul client, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client viene innanzitutto convertito da carattere a Unicode utilizzando l'ACP del server, quindi da Unicode a SQL_C_CHAR usando l'ACP del client.  
  
 Poiché tutte le conversioni vengono eseguite dal driver ODBC di Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sul client, l'ACP del server deve essere una delle tabelle codici installate nel computer client.  
  
 L'utilizzo di Unicode consente di eseguire la conversione più appropriata di tutti i caratteri presenti in entrambe le tabelle codici. Se tuttavia un carattere esiste in una tabella codici ma non in un'altra, non può essere rappresentato nella tabella codici di destinazione. Il simbolo del marchio registrato (®), ad esempio, è presente nella tabella codici 1252, ma non nella tabella codici 437.  
  
 L'impostazione di AutoTranslate non ha effetto sulle conversioni seguenti:  
  
-   Lo stato di trasferimento dei dati tra caratteri SQL_C_CHAR variabili client e colonne, variabili o parametri Unicode **nchar**, **nvarchar**o **ntext** nei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Lo stato di trasferimento dei dati tra le variabili client SQL_C_WCHAR Unicode e le colonne di tipo **char**, **varchar**o **Text** , le variabili o i parametri in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
 I dati devono essere sempre convertiti nel passaggio da carattere a Unicode.  
  
## <a name="see-also"></a>Vedere anche  
   di [ &#40;elaborazione&#41; ODBC dei risultati](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
 [Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
