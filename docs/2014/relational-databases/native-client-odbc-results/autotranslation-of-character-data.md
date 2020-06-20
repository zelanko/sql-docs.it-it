---
title: Conversione automatica dei dati di tipo carattere | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cbced1bb62dcacb896a7ff30fdbd6b5aa28f20e3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039593"
---
# <a name="autotranslation-of-character-data"></a>Conversione automatica dei dati di tipo carattere
  I dati di tipo carattere, ad esempio le variabili di tipo carattere ANSI dichiarati con SQL_C_CHAR o i dati archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando i tipi di dati **char**, **varchar**o **Text** , possono rappresentare solo un numero limitato di caratteri. I dati di tipo carattere archiviati utilizzando un byte per carattere possono rappresentare solo 256 caratteri. I valori archiviati nelle variabili SQL_C_CHAR vengono interpretati mediante la tabella codici ANSI (ACP) del computer client. I valori archiviati utilizzando i tipi di dati **char**, **varchar**o **Text** nel server vengono valutati utilizzando l'ACP del server.  
  
 Se il server e il client hanno lo stesso ACP, non si verificano problemi durante l'interpretazione dei valori archiviati negli oggetti SQL_C_CHAR, **char**, **varchar**o **Text** . Se il server e il client hanno invece diversi, SQL_C_CHAR dati dal client possono essere interpretati come un carattere diverso nel server se usati in colonne, variabili o parametri di tipo **char**, **varchar**o **Text** . Un byte di caratteri contenente il valore 0xA5, ad esempio, viene interpretato come carattere? in un computer che usa la tabella codici 437 e viene interpretato come il segno di yen (??) in un computer che esegue la tabella codici 1252.  
  
 I dati Unicode vengono archiviati utilizzando due byte per carattere. Poiché tutti i caratteri estesi sono inclusi nella specifica Unicode, tutti i caratteri Unicode vengono interpretati allo stesso modo da tutti i computer.  
  
 La funzionalità AutoTranslate del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client tenta di ridurre al minimo i problemi di trasferimento dei dati di tipo carattere tra un client e un server con tabelle codici diverse. È possibile impostare AutoTranslate nella stringa di connessione di [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md), nella stringa di configurazione di [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)o quando si configurano le origini dati per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client mediante l'amministratore ODBC.  
  
 Quando AutoTranslate è impostato su "No", non vengono eseguite conversioni sui dati spostati tra SQL_C_CHAR variabili nelle colonne client e **char**, **varchar**o **Text** , variabili o parametri di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Se i dati contengono caratteri estesi e i due computer dispongono di tabelle codici diverse, gli schemi di bit potrebbero essere interpretati in modo diverso sui computer client e server. I dati verranno interpretati nello stesso modo se entrambi computer dispongono della stessa tabella codici.  
  
 Quando AutoTranslate è impostato su "Yes", il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client utilizza Unicode per convertire i dati spostati tra SQL_C_CHAR variabili nelle colonne client e **char**, **varchar**o **Text** , variabili o parametri di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database:  
  
-   Quando i dati vengono inviati da una variabile SQL_C_CHAR sul client a una colonna **char**, **varchar**o **Text** , una variabile o un parametro di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, il driver ODBC esegue prima la conversione da SQL_C_CHAR a Unicode utilizzando l'ACP del client, quindi da Unicode di nuovo a carattere utilizzando l'ACP del server.  
  
-   Quando i dati vengono inviati da una colonna di tipo **char**, **varchar**o **Text** , una variabile o un parametro di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database a una variabile di SQL_C_CHAR nel client, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client converte innanzitutto da carattere a Unicode utilizzando l'acp del server, quindi da Unicode a SQL_C_CHAR utilizzando l'ACP del client.  
  
 Poiché tutte le conversioni vengono eseguite dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client in esecuzione sul client, l'ACP del server deve essere una delle tabelle codici installate nel computer client.  
  
 L'utilizzo di Unicode consente di eseguire la conversione più appropriata di tutti i caratteri presenti in entrambe le tabelle codici. Se tuttavia un carattere esiste in una tabella codici ma non in un'altra, non può essere rappresentato nella tabella codici di destinazione. Ad esempio, la tabella codici 1252 presenta il simbolo del marchio registrato (??), mentre la tabella codici 437 non lo è.  
  
 L'impostazione di AutoTranslate non ha effetto sulle conversioni seguenti:  
  
-   Lo stato di trasferimento dei dati tra caratteri SQL_C_CHAR variabili client e colonne, variabili o parametri Unicode **nchar**, **nvarchar**o **ntext** nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
-   Lo stato di trasferimento dei dati tra le variabili client SQL_C_WCHAR Unicode e le colonne di tipo **char**, **varchar**o **Text** , le variabili o i parametri nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
 I dati devono essere sempre convertiti nel passaggio da carattere a Unicode.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBC](processing-results-odbc.md)   
 [Regole di confronto e supporto Unicode](../collations/collation-and-unicode-support.md)  
  
  
