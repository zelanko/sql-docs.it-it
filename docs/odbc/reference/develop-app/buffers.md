---
title: I buffer | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 306632f544f144aa4b21e150543c2d4ca5a37d0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008019"
---
# <a name="buffers"></a>Buffer
Un buffer è qualsiasi parte di memoria dell'applicazione utilizzata per passare dati tra l'applicazione e il driver. Ad esempio, i buffer dell'applicazione possono essere associati, oppure *associata,* con colonne del set di risultati **SQLBindCol**. Come viene recuperata ogni riga, i dati vengono restituiti per ogni colonna in questi buffer. *I buffer di input* vengono utilizzati per passare dati dall'applicazione al driver; *buffer di output* vengono utilizzate per restituire i dati dal driver per l'applicazione.  
  
> [!NOTE]  
>  Se una funzione ODBC restituisce SQL_ERROR, il contenuto di qualsiasi argomento di output per tale funzione è indefinito.  
  
 Questa sezione riguarda stesso principalmente con buffer di tipo indeterminato. Gli indirizzi di tali buffer sono visualizzati come argomenti di tipo SQLPOINTER, ad esempio la *TargetValuePtr* nell'argomento **SQLBindCol**. Tuttavia, alcuni degli elementi descritti in questo caso, ad esempio gli argomenti usati con i buffer, si applicano anche agli argomenti utilizzati per passare le stringhe al driver, ad esempio la *TableName* nell'argomento **SQLTables**.  
  
 Tali buffer sono in genere a coppie. *Buffer di dati* sono consente di passare i dati stessi, mentre *buffer di lunghezza/indicatore* vengono utilizzati per passare la lunghezza dei dati nel buffer di dati o un valore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono NULL. La lunghezza dei dati in un buffer di dati è diversa dalla lunghezza del buffer di dati stesso. Nella figura seguente mostra la relazione tra il buffer dei dati e buffer di lunghezza/indicatore.  
  
 ![Buffer dei dati e la lunghezza&#47;buffer di indicatore](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Un buffer di lunghezza/indicatore è necessario ogni volta che il buffer di dati contiene dati a lunghezza variabile, ad esempio carattere o binario. Se il buffer di dati contiene dati a lunghezza fissa, ad esempio una struttura di data o numero intero, un buffer di lunghezza/indicatore è necessario solo per passare i valori dell'indicatore perché la lunghezza dei dati è già nota. Se un'applicazione usa un buffer di lunghezza/indicatore con dati a lunghezza fissa, il driver ignora qualsiasi lunghezza passata in esso.  
  
 La lunghezza di buffer di dati e dei relativi dati viene misurata in byte, a differenza di caratteri. Questa distinzione è importante per i programmi che utilizzano le stringhe ANSI poiché le lunghezze in byte e i caratteri sono uguali.  
  
 Quando il buffer di dati rappresenta un campo di descrizione definito dal driver, un campo di diagnostica o un attributo, l'applicazione deve indicare al Driver Manager la natura dell'argomento della funzione che indica il valore del campo o attributo. L'applicazione viene eseguita impostando l'argomento length in qualsiasi chiamata di funzione che imposta il campo o attributo a uno dei valori seguenti. (Lo stesso vale per le funzioni che recuperano i valori del campo o attributo, con l'eccezione che l'argomento fa riferimento ai valori presenti per la funzione di impostazione nell'argomento stesso.)  
  
-   Se l'argomento della funzione che indica il valore del campo o attributo è un puntatore a una stringa di caratteri, il *lunghezza* argomento è la lunghezza della stringa o SQL_NTS.  
  
-   Se l'argomento della funzione che indica il valore del campo o attributo è un puntatore a un buffer binario, l'applicazione inserisce il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) (macro) nel *lunghezza* discussione. Un valore negativo in questo modo vengono inserite le *lunghezza* argomento.  
  
-   Se l'argomento della funzione che indica il valore del campo o attributo è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria, il *lunghezza* argomento deve avere il valore SQL_IS_POINTER.  
  
-   Se l'argomento della funzione che indica il valore del campo o attributo contiene un valore di lunghezza fissa, il *lunghezza* argomento è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, come appropriato.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Buffer posticipati](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Utilizzo dei buffer dei dati](../../../odbc/reference/develop-app/using-data-buffers.md)
