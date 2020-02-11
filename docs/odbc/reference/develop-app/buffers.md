---
title: Buffer | Microsoft Docs
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
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118740"
---
# <a name="buffers"></a>Buffer
Un buffer è una parte della memoria dell'applicazione usata per passare i dati tra l'applicazione e il driver. Ad esempio, i buffer dell'applicazione possono essere associati *a* colonne del set di risultati con **SQLBindCol**. Quando ogni riga viene recuperata, i dati vengono restituiti per ogni colonna nei buffer. I *buffer di input* vengono utilizzati per passare i dati dall'applicazione al driver; i *buffer di output* vengono utilizzati per restituire i dati dal driver all'applicazione.  
  
> [!NOTE]  
>  Se una funzione ODBC restituisce SQL_ERROR, il contenuto di tutti gli argomenti di output della funzione non è definito.  
  
 Questa discussione riguarda principalmente i buffer di tipo indeterminato. Gli indirizzi di questi buffer vengono visualizzati come argomenti di tipo SQLPOINTER, ad esempio l'argomento *TargetValuePtr* in **SQLBindCol**. Tuttavia, alcuni degli elementi descritti in questa sezione, ad esempio gli argomenti utilizzati con i buffer, si applicano anche agli argomenti utilizzati per passare stringhe al driver, ad esempio l'argomento *TableName* in **SQLTables**.  
  
 Questi buffer sono in genere di coppie. I *buffer di dati* vengono utilizzati per passare i dati stessi, mentre i buffer di *lunghezza/indicatore* vengono utilizzati per passare la lunghezza dei dati nel buffer di dati o un valore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono null. La lunghezza dei dati in un buffer di dati è diversa dalla lunghezza del buffer di dati stesso. Nella figura seguente viene illustrata la relazione tra il buffer dei dati e il buffer di lunghezza/indicatore.  
  
 ![Buffer di dati e lunghezza&#47;buffer indicatore](../../../odbc/reference/develop-app/media/pr09.gif "PR09")  
  
 Un buffer di lunghezza/indicatore è necessario ogni volta che il buffer dei dati contiene dati a lunghezza variabile, ad esempio dati di tipo carattere o binario. Se il buffer dei dati contiene dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, è necessario un buffer di lunghezza/indicatore solo per passare i valori dell'indicatore poiché la lunghezza dei dati è già nota. Se un'applicazione utilizza un buffer di lunghezza/indicatore con dati a lunghezza fissa, il driver ignora le lunghezze passate.  
  
 La lunghezza del buffer di dati e dei dati in esso contenuti viene misurata in byte, in contrapposizione ai caratteri. Questa distinzione non è importante per i programmi che usano stringhe ANSI perché le lunghezze in byte e caratteri sono uguali.  
  
 Quando il buffer dei dati rappresenta un campo del descrittore definito dal driver, un campo di diagnostica o un attributo, l'applicazione deve indicare alla gestione driver la natura dell'argomento della funzione che indica il valore per il campo o l'attributo. Questa operazione viene eseguita dall'applicazione impostando l'argomento length in una chiamata di funzione che imposta il campo o l'attributo su uno dei valori seguenti. (Lo stesso vale per le funzioni che recuperano i valori del campo o dell'attributo, con l'eccezione che l'argomento punta ai valori per la funzione di impostazione si trovano nell'argomento stesso).  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo è un puntatore a una stringa di caratteri, l'argomento *length* è la lunghezza della stringa o del SQL_NTS.  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR (*length*) nell'argomento *length* . Questo inserisce un valore negativo nell'argomento *length* .  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, il valore dell'argomento *length* deve essere SQL_IS_POINTER.  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo contiene un valore a lunghezza fissa, l'argomento *length* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, a seconda dei casi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Buffer posticipati](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Allocazione e rilascio di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Uso dei buffer dei dati](../../../odbc/reference/develop-app/using-data-buffers.md)
