---
title: I record di diagnostica | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90133b4a18876c52b9b6b6bffbe4c8c02c953e07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039884"
---
# <a name="diagnostic-records"></a>Record di diagnostica
Associato a ogni ambiente, connessione, istruzione e descrittore handle vengono *record di diagnostica*. Questi record contengono informazioni diagnostiche sull'ultima funzione chiamata che è usato un handle specifico. I record vengono sostituiti solo quando viene chiamata un'altra funzione utilizzando l'handle. Non sono previsti limiti al numero di record di diagnostica che possono essere archiviati in qualsiasi momento.  
  
 Esistono due tipi di record di diagnostica: una *record di intestazione* e zero o più *record di stato*. Il record di intestazione è 0. i record di stato sono record 1 e versioni successive. I record di diagnostica sono costituiti da un numero di campi distinti, che sono diversi per il record di intestazione e i record di stato. Componenti ODBC è inoltre possono definire i propri campi di record di diagnostica.  
  
 Anche se i record di diagnostica possono essere considerati come strutture, non è necessario per poter essere effettivamente strutture. come un driver archivia le informazioni di diagnostica è specifico del driver.  
  
 I campi nei record di diagnostica vengono recuperati con **SQLGetDiagField**. SQLSTATE, il numero di errore nativo e i campi di messaggio di diagnostica di record di stato possono essere recuperati in una singola chiamata con **SQLGetDiagRec**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Record di intestazione](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Record di stato](../../../odbc/reference/develop-app/status-records.md)
