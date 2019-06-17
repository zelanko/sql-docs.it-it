---
title: Tipi di dati C in ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5472595383c7e4fcf448374c1fd85587246328f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199217"
---
# <a name="c-data-types-in-odbc"></a>Tipi di dati C in ODBC
ODBC definisce i tipi di dati C utilizzate da variabili di applicazione e i relativi identificatori di tipo corrispondente. Questi vengono usati dai buffer che sono associate a colonne del set di risultati e parametri dell'istruzione. Si supponga, ad esempio, che un'applicazione deve recuperare i dati da una colonna del set di risultati in formato carattere. Dichiara una variabile con i dati SQLCHAR * tipo di dati e si associa questa variabile per la colonna del set di risultati con un identificatore del tipo di SQL_C_CHAR. Per un elenco completo dei tipi di dati C e gli identificatori di tipo, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 Anche ODBC definisce già un mapping predefinito da ogni tipo di dati SQL a un tipo di dati C. Ad esempio, un integer a 2 byte nell'origine dati viene eseguito il mapping a un integer a 2 byte nell'applicazione. Per usare il mapping predefinito, un'applicazione specifica l'identificatore di tipo SQL_C_DEFAULT. Tuttavia, l'uso di questo identificatore è sconsigliato per motivi di interoperabilità.  
  
 Tutti i tipi di dati integer C definiti in ODBC 1*x* ha eseguito l'accesso. In ODBC 2.0 sono stati aggiunti tipi di dati C non firmati e i relativi identificatori di tipo corrispondente. Per questo motivo, le applicazioni e i driver devono prestare particolarmente attenzione quando si lavora con 1*x* versioni.  
  
## <a name="c-data-type-extensibility"></a>Estendibilità del tipo di dati C  
 In ODBC 3.8, è possibile specificare tipi di dati C specifici del driver. In questo modo è possibile associare un tipo SQL come tipo nelle applicazioni ODBC C specifici del driver quando si chiama [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Ciò può rivelarsi utile per il supporto di nuovi tipi di server, poiché i tipi di dati C esistenti potrebbero non rappresentare in modo corretto i nuovi tipi di dati di server. Utilizzo di tipi C specifiche del driver, è possibile aumentare il numero di conversioni che possono eseguire i driver.  
  
 Ad esempio, si supponga che un sistema di gestione di database (DBMS) introdotto un nuovo tipo SQL, **DATETIMEOFFSET**, per rappresentare la data e ora con informazioni sul fuso orario. Non vi sarà alcun tipo specifico di C in ODBC che corrispondessero alla **DATETIMEOFFSET**. Un'applicazione dovrà associare **DATETIMEOFFSET** come SQL_C_BINARY ed eseguire il cast a una data definito dall'utente digitare. Partire con estendibilità del tipo di dati C ODBC 3.8, un driver può definire un nuovo tipo di C corrispondente. Ad esempio, per il nuovo SQL tipo DATETIMEOFFSET, il driver può definire un nuovo tipo C corrispondente, ad esempio SQL_C_DATETIMEOFFSET. Quindi, un'applicazione può associare il nuovo tipo di SQL come tipo C specifiche del driver.  
  
 Viene definito un tipo di dati C nel driver come indicato di seguito:  
  
-   Il livello di conformità di ODBC per un'applicazione, il driver ODBC e Driver Manager è 3,8 (o versione successiva).  
  
-   L'intervallo di dati di tipo C specifiche del driver è tra 0x4000 e 0x7FFF.  
  
-   Il driver definisce la struttura dei dati corrispondenti al tipo C.  Questa operazione può essere eseguita nel SDK specifici del driver.  
  
 Gestione driver non verrà convalidato un tipo C definito nell'intervallo di 0x4000 e 0x7FFF; il driver esegue la convalida e qualsiasi conversione di tipi di dati. Ma se l'intervallo di dati di tipo C passato al gestore del driver è compreso tra 0x0000 e 0x3FFF o tra 0x8000 e 0xFFFF, Gestione driver convaliderà il tipo di dati C.  
  
> [!NOTE]  
>  Tipi di dati C specifici del driver devono essere descritti nella documentazione del driver.  
  
 Per specificare un livello di conformità ODBC di 3.8, un'applicazione chiama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con il SQL_ATTR_ODBC_VERSION attributo impostato su **SQL_OV_ODBC3_80**. Per determinare la versione del driver, un'applicazione chiama **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Per altre informazioni su ODBC 3.8, vedere [What ' s New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md)
