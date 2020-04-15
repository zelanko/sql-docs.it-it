---
title: Tipi di dati C in ODBC Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306296"
---
# <a name="c-data-types-in-odbc"></a>Tipi di dati C in ODBC
ODBC definisce i tipi di dati C utilizzati dalle variabili di applicazione e gli identificatori di tipo corrispondenti. Vengono utilizzati dai buffer associati alle colonne del set di risultati e ai parametri dell'istruzione. Si supponga, ad esempio, che un'applicazione desideri recuperare dati da una colonna del set di risultati in formato carattere. Dichiara una variabile con il tipo di dati SQLCHAR e associa questa variabile alla colonna del set di risultati con un identificatore di tipo SQL_C_CHAR. Per un elenco completo dei tipi di dati C e degli identificatori di tipo, vedere [Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 ODBC definisce inoltre un mapping predefinito da ogni tipo di dati SQL a un tipo di dati C.ODBC also defines a default mapping from each SQL data type to a C data type. Ad esempio, un numero intero a 2 byte nell'origine dati viene mappato a un numero intero a 2 byte nell'applicazione. Per utilizzare il mapping predefinito, un'applicazione specifica l'identificatore del tipo SQL_C_DEFAULT. Tuttavia, l'uso di questo identificatore è sconsigliato per motivi di interoperabilità.  
  
 Tutti i tipi di dati Integer C definiti in ODBC *1.x* sono stati firmati. I tipi di dati C non firmati e gli identificatori di tipo corrispondenti sono stati aggiunti in ODBC 2.0. Per questo motivo, le applicazioni e i driver devono prestare particolare attenzione quando si gestiscono le versioni *1.x.*  
  
## <a name="c-data-type-extensibility"></a>Estensibilità del tipo di dati CC Data Type Extensibility  
 In ODBC 3.8, è possibile specificare i tipi di dati C specifici del driver. In questo modo è possibile associare un tipo SQL come tipo C specifico del driver nelle applicazioni ODBC quando si chiamano [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Ciò può essere utile per il supporto di nuovi tipi di server, perché i tipi di dati C esistenti potrebbero non rappresentare correttamente i nuovi tipi di dati del server. L'utilizzo di tipi C specifici del driver può aumentare il numero di conversioni che i driver possono eseguire.  
  
 Si supponga, ad esempio, che un sistema di gestione di database (DBMS) abbia introdotto un nuovo tipo SQL, **DATETIMEOFFSET**, per rappresentare la data e l'ora con le informazioni sul fuso orario. Non ci sarebbe alcun tipo C specifico in ODBC corrispondente a **DATETIMEOFFSET**. Un'applicazione deve associare **DATETIMEOFFSET** come SQL_C_BINARY ed eseguire il cast a un tipo di dati definito dall'utente. A partire da ODBC 3.8 con estensibilità del tipo di dati C, un driver può definire un nuovo tipo C corrispondente. Ad esempio, per il nuovo tipo SQL DATETIMEOFFSET, il driver può definire un nuovo tipo C corrispondente, ad esempio SQL_C_DATETIMEOFFSET. Quindi, un'applicazione può associare il nuovo tipo SQL come tipo C specifico del driver.  
  
 Un tipo di dati C viene definito nel driver come segue:  
  
-   Il livello di conformità ODBC per un'applicazione, driver ODBC e Gestione Driver è 3.8 (o superiore).  
  
-   L'intervallo di dati di un tipo C specifico del driver è compreso tra 0x4000 e 0x7FFF.  
  
-   Il driver definisce la struttura dei dati corrispondenti al tipo C.  Questa operazione può essere eseguita nell'SDK specifico del driver.  
  
 Gestione driver non convaliderà un tipo C definito nell'intervallo 0x4000 e 0x7FFF; il driver eseguirà la convalida e qualsiasi conversione del tipo di dati. Ma se l'intervallo di dati di un tipo C passato a Gestione driver è compreso tra 0x0000 e 0x3FFF o tra 0x8000 e 0xFFFF, Gestione driver convaliderà il tipo di dati C.  
  
> [!NOTE]  
>  I tipi di dati C specifici del driver devono essere descritti nella documentazione del driver.  
  
 Per specificare un livello di conformità ODBC 3.8, un'applicazione chiama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con l'attributo SQL_ATTR_ODBC_VERSION impostato su **SQL_OV_ODBC3_80**. Per determinare la versione del driver, un'applicazione chiama **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Per ulteriori informazioni su ODBC 3.8, vedere [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md)
