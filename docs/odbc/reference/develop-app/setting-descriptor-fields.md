---
title: Impostare i campi di descrizione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14724a5cc863074344cfbb02615f0ccff228f04c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447669"
---
# <a name="setting-descriptor-fields"></a>Configurazione dei campi del descrittore
Per modificare i campi di un descrittore, un'applicazione può chiamare **SQLSetDescField**. Alcuni campi sono di sola lettura e non possono essere impostate. (Vedere la [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descrizione della funzione.)  
  
 Campi del record del descrittore sono impostati con un numero di record (*RecNumber*) pari a 1 o versione successiva, mentre i campi di intestazione di descrizione vengono impostati con un numero di record pari a 0. Un numero di record 0 viene anche utilizzato per impostare i campi di segnalibro, in conformità con la convenzione che i segnalibri sono contenuti nella colonna 0. Questo potrebbe rendere l'impressione che sono contenuti i campi di segnalibro all'interno dell'intestazione del descrittore, ma ciò non avviene. I campi di segnalibro sono diversi dai campi di intestazione.  
  
 Quando si impostano i campi singolarmente, l'applicazione deve seguire la sequenza definita [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Se si imposta alcuni campi, il driver imposti gli altri campi. Ciò garantisce che il descrittore è sempre pronto per l'uso dopo l'applicazione ha specificato un tipo di dati. Quando l'applicazione imposta il campo SQL_DESC_TYPE, il driver verificherà che gli altri campi che specificano il tipo siano validi e coerenti.  
  
 Se una chiamata di funzione che è necessario impostare un campo di descrizione non riesce, il contenuto del campo del descrittore è non definito dopo la chiamata di funzione non riuscita.
