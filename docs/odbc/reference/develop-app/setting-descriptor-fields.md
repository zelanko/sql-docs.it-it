---
title: Impostazione dei campi del descrittore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f9520e2ef462df481bb104e389aeb57b5dd457
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304152"
---
# <a name="setting-descriptor-fields"></a>Configurazione dei campi del descrittore
Per modificare i campi di un descrittore, un'applicazione può chiamare **SQLSetDescField**. Alcuni campi sono di sola lettura e non possono essere impostati. Vedere la descrizione della funzione [SQLSetDescField.](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
 I campi dei record del descrittore vengono impostati con un numero di record (*RecNumber*) pari a 1 o superiore, mentre i campi di intestazione del descrittore vengono impostati con un numero di record pari a 0. Un numero di record pari a 0 viene utilizzato anche per impostare i campi dei segnalibri, in base alla convenzione con cui i segnalibri sono contenuti nella colonna 0. Ciò potrebbe lasciare l'impressione che i campi segnalibro siano contenuti all'interno dell'intestazione del descrittore, ma questo non è il caso. I campi dei segnalibri sono distinti dai campi di intestazione.  
  
 Quando si impostano i campi singolarmente, l'applicazione deve seguire la sequenza definita in [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). L'impostazione di alcuni campi fa sì che il driver per impostare altri campi. Ciò garantisce che il descrittore sia sempre pronto per l'uso dopo che l'applicazione ha specificato un tipo di dati. Quando l'applicazione imposta il campo SQL_DESC_TYPE, il driver verifica che gli altri campi che specificano il tipo siano validi e coerenti.  
  
 Se una chiamata di funzione che imposta un campo del descrittore ha esito negativo, il contenuto del campo del descrittore non è definito dopo la chiamata di funzione non riuscita.
