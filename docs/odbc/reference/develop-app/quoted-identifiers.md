---
title: Identificatori quotati Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282004"
---
# <a name="quoted-identifiers"></a>Identificatori delimitati
In un'istruzione SQL, gli identificatori contenenti caratteri speciali o parole chiave di corrispondenza devono essere racchiusi tra *caratteri di virgolette dell'identificatore*; Gli identificatori racchiusi tra tali caratteri sono noti come *identificatori tra virgolette (noti* anche come *identificatori delimitati* in SQL-92). Ad esempio, l'identificatore contabilità fornitori viene citato nella seguente istruzione **SELECT:**  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Il motivo per citare gli identificatori è quello di rendere l'istruzione analizzabile. Ad esempio, se la contabilità fornitori non è stata quotata nell'istruzione precedente, il parser presupporrà che siano presenti due tabelle, Accounts e Payable, e restituirà un errore di sintassi che non sono separati da una virgola. Il carattere dell'virgoletta dell'identificatore è specifico del driver e viene recuperato con l'opzione SQL_IDENTIFIER_QUOTE_CHAR in **SQLGetInfo**. Gli elenchi di caratteri speciali e di parole chiave vengono recuperati con le opzioni SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS in **SQLGetInfo**.  
  
 Per essere sicure, le applicazioni interoperabili spesso citano tutti gli identificatori ad eccezione di quelli per le pseudo-colonne, ad esempio la colonna ROWID in Oracle.To be safe, interoperabilable applications often quote all identifiers except those for pseudo-columns, such as the ROWID column in Oracle. **SQLSpecialColumns** restituisce un elenco di pseudo-colonne. Inoltre, se sono presenti restrizioni specifiche dell'applicazione in cui possono essere visualizzati caratteri speciali nel nome di un oggetto, è consigliabile che le applicazioni interoperabili non utilizzino caratteri speciali in tali posizioni.
