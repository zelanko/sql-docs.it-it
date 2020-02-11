---
title: Proprietà personalizzate dell'origine ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9239c1022cd9dfab1edba675c21e69129efe36c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770977"
---
# <a name="odbc-source-custom-properties"></a>Proprietà personalizzate dell'origine ODBC
  Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine ODBC. È possibile impostare tutte le proprietà dalle espressioni di proprietà SSIS.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Connessione|ODBC Connection|Connessione ODBC per accedere al database di origine.|  
|AccessMode|Integer (enumerazione)|Modalità utilizzata per accedere al database. I valori possibili sono Table Name (0) e SQL Command (1).<br /><br /> Il valore predefinito è Table Name (0).|  
|BatchSize|Integer|Dimensioni del batch per l'estrazione bulk. Corrisponde al numero di record estratti come matrice. Se il provider ODBC selezionato non supporta le matrici, le dimensioni del batch sono pari a 1.|  
|BindCharColumnAs|Integer (enumerazione)|Questa proprietà determina il modo in cui l'origine ODBC associa colonne con tipi string a più byte quali SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.<br /><br /> I valori possibili sono Unicode (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e ANSI (1), che specifica l'associazione delle colonne come SQL_C_CHAR. Il valore predefinito è Unicode (0).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|BindNumericAs|Integer (enumerazione)|Questa proprietà determina il modo in cui l'origine ODBC associa colonne con dati numerici con tipi di dati SQL_TYPE_NUMERIC e SQL_TYPE_DECIMAL.<br /><br /> Le opzioni possibili sono Char (0), che specifica l'associazione delle colonne come SQL_C_WCHAR, e Numeric (1), che specifica l'associazione delle colonne come SQL_C_NUMERIC. Il valore predefinito è Char (0).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|DefaultCodePage|Integer|Tabella codici da utilizzare per le colonne di output di tipo string.<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|ExposeCharColumnsAsUnicode|Boolean|Questa proprietà determina il modo in cui le colonne CHAR vengono esposte dal componente. Il valore predefinito è False, che indica che le colonne CHAR vengono esposte come stringhe a più byte (DT_STR). Se il valore è True, le colonne CHAR vengono esposte come stringhe wide (DT_WSTR).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|FetchMethod|Integer (enumerazione)|Metodo utilizzato per recuperare i dati. Le possibili opzioni sono Row by row (0) e Batch (1). Il valore predefinito è Batch (1).<br /><br /> Per altre informazioni su queste opzioni, vedere [Origine ODBC](odbc-source.md).<br /><br /> **Nota**: questa proprietà non è disponibile nell' **Editor origine ODBC**, ma può essere impostata tramite l' **Editor avanzato**.|  
|SqlCommand|string|Comando SQL da eseguire quando la proprietà AccessMode è impostata su SQL Command.|  
|StatementTimeout|Integer|Numero di secondi di attesa per l'esecuzione di un'istruzione SQL prima di tornare all'applicazione con un errore. Il valore predefinito è 0. Il valore 0 indica che al sistema non viene applicato alcun timeout.|  
|TableName|string|Nome della tabella con i dati in uso quando la proprietà AccessMode è impostata su Table Name.|  
|LobChunckSize|Integer|Allocazione delle dimensioni del blocco per colonne LOB.|  
||||  
  
## <a name="see-also"></a>Vedere anche  
 [Origine ODBC](odbc-source.md)   
 [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../odbc-source-editor-connection-manager-page.md)  
  
  
