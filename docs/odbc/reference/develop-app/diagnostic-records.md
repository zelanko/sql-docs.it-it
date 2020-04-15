---
title: Record diagnostici Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305182"
---
# <a name="diagnostic-records"></a>Record di diagnostica
Associato a ogni ambiente, connessione, istruzione e handle di descrittore sono *record di diagnostica*. Questi record contengono informazioni diagnostiche sull'ultima funzione chiamata che ha utilizzato un handle specifico. I record vengono sostituiti solo quando viene chiamata un'altra funzione utilizzando tale handle. Non esiste alcun limite al numero di record di diagnostica che possono essere archiviati contemporaneamente.  
  
 Esistono due tipi di record di diagnostica: un record di *intestazione* e zero o più *record di stato*. Il record di intestazione è il record 0; i record di stato sono record 1 e superiori. I record di diagnostica sono composti da diversi campi separati, diversi per il record di intestazione e i record di stato. Inoltre, i componenti ODBC possono definire i propri campi di record di diagnostica.  
  
 Anche se i record diagnostici possono essere considerati come strutture, non è necessario che siano effettivamente strutture; il modo in cui un driver archivia le informazioni di diagnostica è specifico del driver.  
  
 I campi nei record di diagnostica vengono recuperati con **SQLGetDiagField**. I campi SQLSTATE, il numero di errore nativo e i campi dei messaggi di diagnostica dei record di stato possono essere recuperati in una singola chiamata con **SQLGetDiagRec**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Record di intestazione](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Record di stato](../../../odbc/reference/develop-app/status-records.md)
