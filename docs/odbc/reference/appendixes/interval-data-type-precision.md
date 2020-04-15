---
title: Interval Tipo di dati Precisione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290741"
---
# <a name="interval-data-type-precision"></a>Precisione del tipo di dati intervallo
La precisione per un tipo di dati intervallo include la precisione di interlinea dell'intervallo, la precisione dell'intervallo e la precisione dei secondi.  
  
 Il campo iniziale di un intervallo è un valore numerico con segno. Il numero massimo di cifre per il campo iniziale è determinato da una quantità denominata *precisione interlinea intervallo,* che fa parte della dichiarazione del tipo di dati. Ad esempio, la dichiarazione: INTERVAL HOUR(5) TO MINUTE ha una precisione interlinea intervallo di 5; il campo HOUR può accettare valori compresi tra -99999 e 99999. La precisione di interlinea dell'intervallo è contenuta nel campo SQL_DESC_DATETIME_INTERVAL_PRECISION del record del descrittore.  
  
 L'elenco dei campi di cui è costituito un tipo di dati intervallo è denominato *precisione intervallo*. Non è un valore numerico, come potrebbe implicare il termine "precisione". Ad esempio, la precisione dell'intervallo del tipo INTERVAL DAY TO SECOND è l'elenco DAY, HOUR, MINUTE, SECOND. Non esiste alcun campo descrittore che contiene questo valore; la precisione dell'intervallo può sempre essere determinata dal tipo di dati intervallo.  
  
 Qualsiasi tipo di dati intervallo con un campo SECOND ha una *precisione di secondi.* Questo è il numero di cifre decimali consentite nella parte frazionaria del valore dei secondi. Questo è diverso rispetto ad altri tipi di dati, dove precisione indica il numero di cifre prima del separatore decimale. La precisione dei secondi di un tipo di dati intervallo è il numero di cifre dopo il separatore decimale. Ad esempio, se la precisione dei secondi è impostata su 6, il numero 123456 nel campo frazione verrà interpretato come 0,123456 e il numero 1230 verrebbe interpretato come 0,001230. Per altri tipi di dati, questa operazione viene definita scala. La precisione dei secondi dell'intervallo è contenuta nel campo SQL_DESC_PRECISION del descrittore. Se la precisione del componente secondi frazionari del valore dell'intervallo SQL è maggiore di quella che può essere mantenuta nella struttura dell'intervallo C, è definito dal driver se il valore dei secondi frazionari nell'intervallo SQL viene arrotondato o troncato quando viene convertito nella struttura dell'intervallo C.  
  
 Quando il campo SQL_DESC_CONCISE_TYPE è impostato su un tipo di dati intervallo, il campo SQL_DESC_TYPE viene impostato su SQL_INTERVAL e il SQL_DESC_DATETIME_INTERVAL_CODE viene impostato sul codice per il tipo di dati intervallo. Il campo SQL_DESC_DATETIME_INTERVAL_PRECISION viene impostato automaticamente sulla precisione di interlinea dell'intervallo predefinito pari a 2 e il campo SQL_DESC_PRECISION viene impostato automaticamente sulla precisione predefinita dei secondi dell'intervallo pari a 6. Se uno di questi valori non è appropriato, l'applicazione deve impostare in modo esplicito il campo del descrittore tramite una chiamata a **SQLSetDescField**.
