---
title: Sequenza di record di stato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a88095611a5f551708f3950359063317368757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465919"
---
# <a name="sequence-of-status-records"></a>Sequenza di record di stato
Se vengono restituiti due o più record di stato, il gestore dei Driver e il driver necessario classificarle in base alle regole seguenti. Il record con il valore più alto è il primo record. L'origine di un record (gestione Driver, driver, gateway e così via) non viene considerato quando i record di rango.  
  
-   **Errori** record di stato che descrivono gli errori hanno la priorità più alta. Tra i record degli errori, i record che indicano un errore della transazione o un errore della transazione possibili outrank tutti gli altri record. Se due o più record di descrivere la stessa condizione di errore, SQLSTATEs definito dalla specifica Open dell'interfaccia della riga di gruppo (classi 03 tramite HZ) outrank SQLSTATEs definite da ODBC e definiti dal driver.  
  
-   **N valori di dati definito dall'implementazione** i record di stato che descrivono i valori di dati non definiti dal driver (classe 02) hanno la seconda priorità più alta.  
  
-   **Avvisi** i record di stato che descrivono gli avvisi (classe 01) hanno la priorità più bassa. Se due o più record di descrivere la stessa condizione di avviso, di avviso SQLSTATEs definito dalla specifica CLI di gruppo aprire outrank SQLSTATEs definite da ODBC e definiti dal driver.  
  
 Se sono presenti due o più record con il valore più alto, non viene specificato di record che rappresenta il primo record. L'ordine di tutti gli altri record è definito. In particolare, poiché gli avvisi possono apparire prima di errori, le applicazioni devono controllare tutti i record di stato quando una funzione restituisce un valore diverso da SQL_SUCCESS.
