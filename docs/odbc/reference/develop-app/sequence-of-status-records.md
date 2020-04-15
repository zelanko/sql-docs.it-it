---
title: Sequenza dei record di stato Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304172"
---
# <a name="sequence-of-status-records"></a>Sequenza di record di stato
Se vengono restituiti due o più record di stato, Gestione Driver e driver classificarli in base alle seguenti regole. Il record con il rango più alto è il primo record. L'origine di un record (Gestione driver, driver, gateway e così via) non viene considerata durante la classificazione dei record.  
  
-   **Errori** I record di stato che descrivono gli errori hanno la classificazione più alta. Tra i record di errore, i record che indicano un errore di transazione o un possibile errore di transazione superano tutti gli altri record. Se due o più record descrivono la stessa condizione di errore, SQLSTATEs definito dalla specifica Open Group CLI (classi da 03 a Hz) superano SQLSTATE definite da ODBC e dal driver.  
  
-   **Valori no data definiti dall'implementazioneImplementation-defined No Data Values** I record di stato che descrivono i valori Nessun dato definiti dal driver (classe 02) hanno il secondo rango più alto.  
  
-   **Avvertenze** I record di stato che descrivono gli avvisi (classe 01) hanno il rango più basso. Se due o più record descrivono la stessa condizione di avviso, gli sqlSTATE di avviso definiti dalla specifica Open Group CLI superano le SQLSTATE definite da ODBC e dal driver.  
  
 Se sono presenti due o più record con la classificazione più alta, non è definito quale record è il primo record. L'ordine di tutti gli altri record non è definito. In particolare, poiché gli avvisi possono essere visualizzati prima degli errori, le applicazioni devono controllare tutti i record di stato quando una funzione restituisce un valore diverso da SQL_SUCCESS.
