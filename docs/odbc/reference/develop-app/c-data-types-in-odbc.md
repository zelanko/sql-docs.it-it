---
description: Tipi di dati C in ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 395f60860dd3179326687a6c2fb10bbaf027ca3a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494761"
---
# <a name="c-data-types-in-odbc"></a>Tipi di dati C in ODBC
ODBC definisce i tipi di dati C utilizzati dalle variabili dell'applicazione e i relativi identificatori di tipo corrispondenti. Tali valori vengono utilizzati dai buffer associati alle colonne del set di risultati e ai parametri di istruzione. Si supponga, ad esempio, che un'applicazione desideri recuperare i dati da una colonna del set di risultati in formato carattere. Dichiara una variabile con il tipo di dati SQLCHAR * e associa questa variabile alla colonna del set di risultati con un identificatore di tipo SQL_C_CHAR. Per un elenco completo dei tipi di dati C e degli identificatori di tipo, vedere [Appendice D: tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 ODBC definisce inoltre un mapping predefinito da ogni tipo di dati SQL a un tipo di dati C. Ad esempio, un numero intero a 2 byte nell'origine dati viene mappato a un numero intero a 2 byte nell'applicazione. Per utilizzare il mapping predefinito, un'applicazione specifica l'identificatore del tipo di SQL_C_DEFAULT. Tuttavia, l'utilizzo di questo identificatore è sconsigliato per motivi di interoperabilità.  
  
 Tutti i tipi di dati C Integer definiti in ODBC *1. x* sono stati firmati. I tipi di dati C senza segno e i relativi identificatori di tipo corrispondenti sono stati aggiunti in ODBC 2,0. Per questo motivo, è necessario prestare particolare attenzione alle applicazioni e ai driver quando si gestiscono le versioni *1. x* .  
  
## <a name="c-data-type-extensibility"></a>Estensibilità del tipo di dati C  
 In ODBC 3,8 è possibile specificare tipi di dati C specifici del driver. Ciò consente di associare un tipo SQL come tipo C specifico del driver nelle applicazioni ODBC quando si chiama [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Questa operazione può essere utile per supportare nuovi tipi di server, perché i tipi di dati C esistenti potrebbero non rappresentare correttamente i nuovi tipi di dati del server. L'utilizzo di tipi C specifici del driver può aumentare il numero di conversioni che possono essere eseguite dai driver.  
  
 Si supponga, ad esempio, che un sistema di gestione di database (DBMS) abbia introdotto un nuovo tipo SQL, **DateTimeOffset**, per rappresentare la data e l'ora con le informazioni sul fuso orario. Non è presente alcun tipo C specifico in ODBC corrispondente a **DateTimeOffset**. Un'applicazione deve associare **DateTimeOffset** come SQL_C_BINARY ed eseguirne il cast a un tipo di dati definito dall'utente. A partire da ODBC 3,8 con estensibilità del tipo di dati C, un driver può definire un nuovo tipo C corrispondente. Per il nuovo tipo SQL DATETIMEOFFSET, ad esempio, il driver può definire un nuovo tipo C corrispondente, ad esempio SQL_C_DATETIMEOFFSET. Quindi, un'applicazione può associare il nuovo tipo SQL come tipo C specifico del driver.  
  
 Un tipo di dati C viene definito nel driver come indicato di seguito:  
  
-   Il livello di conformità ODBC per un'applicazione, un driver ODBC e gestione driver è 3,8 (o versione successiva).  
  
-   L'intervallo di dati di un tipo C specifico del driver è compreso tra 0x4000 e 0x7FFF.  
  
-   Il driver definisce la struttura dei dati corrispondenti al tipo C.  Questa operazione può essere eseguita nell'SDK specifico del driver.  
  
 Gestione driver non convaliderà un tipo C definito nell'intervallo tra 0x4000 e 0x7FFF; il driver eseguirà la convalida e qualsiasi conversione del tipo di dati. Tuttavia, se l'intervallo di dati di un tipo C passato a gestione driver è compreso tra 0x0000 e 0x3FFF o tra 0x8000 e 0xFFFF, il tipo di dati C verrà convalidato da Gestione driver.  
  
> [!NOTE]  
>  I tipi di dati C specifici del driver devono essere descritti nella documentazione del driver.  
  
 Per specificare un livello di conformità ODBC 3,8, un'applicazione chiama [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con l'attributo SQL_ATTR_ODBC_VERSION impostato su **SQL_OV_ODBC3_80**. Per determinare la versione del driver, un'applicazione chiama **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Per ulteriori informazioni su ODBC 3,8, vedere Novità di [odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md)
