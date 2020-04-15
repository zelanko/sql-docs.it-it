---
title: Proprietà Buffers . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306286"
---
# <a name="buffers"></a>Buffer
Un buffer è qualsiasi parte della memoria dell'applicazione utilizzata per passare i dati tra l'applicazione e il driver. Ad esempio, i buffer dell'applicazione possono essere associati o associati a colonne del set di risultati con **SQLBindCol**o *associati a* colonne del set di risultati . Man mano che ogni riga viene recuperata, i dati vengono restituiti per ogni colonna in questi buffer. *I buffer di input* vengono utilizzati per passare i dati dall'applicazione al driver; buffer di output vengono *utilizzati* per restituire i dati dal driver all'applicazione.  
  
> [!NOTE]  
>  Se una funzione ODBC restituisce SQL_ERROR, il contenuto di tutti gli argomenti di output per tale funzione non è definito.  
  
 Questa discussione riguarda se stesso principalmente con buffer di tipo indeterminato. Gli indirizzi di questi buffer vengono visualizzati come argomenti di tipo SQLPOINTER, ad esempio l'argomento *TargetValuePtr* in **SQLBindCol**. Tuttavia, alcuni degli elementi descritti di seguito, ad esempio gli argomenti utilizzati con i buffer, si applicano anche agli argomenti utilizzati per passare stringhe al driver, ad esempio il *TableName* argomento **sqlTables**.  
  
 Questi buffer di solito sono in coppia. *I buffer di* dati vengono utilizzati per passare i dati stessi, mentre *i buffer di lunghezza/indicatore* vengono utilizzati per passare la lunghezza dei dati nel buffer di dati o un valore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono NULL. La lunghezza dei dati in un buffer di dati è diversa dalla lunghezza del buffer di dati stesso. Nella figura seguente viene illustrata la relazione tra il buffer di dati e il buffer di lunghezza/indicatore.  
  
 ![Buffer di dati e buffer dell'indicatore di&#47;di lunghezza](../../../odbc/reference/develop-app/media/pr09.gif "pr09 (informazioni in stato di prper)")  
  
 Un buffer di lunghezza/indicatore è necessario ogni volta che il buffer di dati contiene dati a lunghezza variabile, ad esempio dati di tipo carattere o binario. Se il buffer di dati contiene dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, un buffer di lunghezza/indicatore è necessario solo per passare i valori dell'indicatore perché la lunghezza dei dati è già nota. Se un'applicazione utilizza un buffer di lunghezza/indicatore con dati a lunghezza fissa, il driver ignora tutte le lunghezze passate.  
  
 La lunghezza del buffer di dati e dei dati in esso contenuti viene misurata in byte, anziché in caratteri. Questa distinzione non è importante per i programmi che utilizzano stringhe ANSI perché le lunghezze in byte e caratteri sono uguali.  
  
 Quando il buffer di dati rappresenta un campo descrittore definito dal driver, un campo di diagnostica o un attributo, l'applicazione deve indicare a Gestione Driver la natura dell'argomento della funzione che indica il valore per il campo o l'attributo. L'applicazione esegue questa operazione impostando l'argomento length in qualsiasi chiamata di funzione che imposta il campo o l'attributo su uno dei valori seguenti. Lo stesso vale per le funzioni che recuperano i valori del campo o dell'attributo, con l'eccezione che l'argomento punta ai valori che per la funzione di impostazione si trovano nell'argomento stesso.  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo è un puntatore a una stringa di caratteri, l'argomento *length* è la lunghezza della stringa o SQL_NTS.  
  
-   Se l'argomento della funzione che indica il valore del campo o dell'attributo è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) nell'argomento *length.* In questo modo un valore negativo nell'argomento *length.*  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, il *valore* dell'argomento deve avere il valore SQL_IS_POINTER.  
  
-   Se l'argomento della funzione che indica il valore per il campo o l'attributo contiene un valore a lunghezza fissa, l'argomento *length* viene SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_ISI_USMALLINT, a seconda dei casi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Buffer posticipati](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Allocazione e rilascio di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Uso dei buffer dei dati](../../../odbc/reference/develop-app/using-data-buffers.md)
