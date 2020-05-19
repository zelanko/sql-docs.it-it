---
title: SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dda7c4c0e2ae187f96883a32cac2528eceb90c74
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706293"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  Per le istruzioni eseguite, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client non deve eseguire una query sul server per descrivere le colonne in un set di risultati. In questo caso, non `SQLDescribeCol` causa un round trip del server. Analogamente a [SQLColAttribute](sqlnumresultcols.md), `SQLDescribeCol` la chiamata a istruzioni preparate ma non eseguite genera un round trip del server.  
  
 Quando un'istruzione o un batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] restituisce più set di righe di risultati, è possibile che una colonna, a cui fa riferimento un numero ordinale, provenga da una tabella separata o faccia riferimento a una colonna completamente diversa nel set di risultati. `SQLDescribeCol`deve essere chiamato per ogni set. Quando il set di risultati cambia, l'applicazione deve riassociare i valori dei dati prima di recuperare i risultati delle righe. Per ulteriori informazioni sulla gestione di più restituzione di set di risultati, vedere [SQLMoreResults](sqlmoreresults.md).  
  
 Gli attributi di colonna vengono indicati solo per il primo set di risultati quando più set di risultati vengono generati da un batch preparato di istruzioni SQL.  
  
 Per i tipi di dati con valori di grandi dimensioni, il valore restituito in *DataTypePTR* è SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Il valore SQL_SS_LENGTH_UNLIMITED in *ColumnSizePtr* indica che la dimensione è "illimitata".  
  
 I miglioramenti apportati al motore di database a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] consentono a SQLDescribeCol di ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati possono essere diversi dai valori restituiti da SQLDescribeCol nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>Supporto di SQLDescribeCol per le caratteristiche avanzate di data e ora  
 I valori restituiti per i tipi di data/ora sono i seguenti:  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|data|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>Supporto di SQLDescribeCol per tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLDescribeCol` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLDescribeCol (funzione)](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
