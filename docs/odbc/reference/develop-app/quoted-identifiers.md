---
title: Gli identificatori tra virgolette | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bc4d8378c243edf9f01cca58ff8be11d675711a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078998"
---
# <a name="quoted-identifiers"></a>Identificatori delimitati
In un'istruzione SQL, gli identificatori che contengono caratteri speciali o parole chiave di corrispondenza devono essere racchiuso *caratteri di identificatore offerta*; gli identificatori racchiusi tra tali caratteri sono note come *racchiusi tra virgolette gli identificatori*(noto anche come *identificatori delimitati* in SQL-92). Ad esempio, l'identificatore di contabilità è racchiuso tra virgolette in quanto segue **seleziona** istruzione:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Il motivo per inserire identificatori è eseguire l'istruzione analizzabili. Ad esempio, se contabilità fornitori non è delimitato nell'istruzione precedente, il parser sarebbe presuppongono che si sono verificati due tabelle, gli account e i fornitori e restituire un errore di sintassi che non sono stati separati da una virgola. L'identificatore virgolette è specifico del driver e viene recuperata con l'opzione SQL_IDENTIFIER_QUOTE_CHAR **SQLGetInfo**. Gli elenchi di caratteri speciali e parole chiave vengono recuperati con le opzioni SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS **SQLGetInfo**.  
  
 Per sicurezza, applicazioni interoperative citare spesso tutti gli identificatori, ad eccezione di quelli per le pseudo-colonne, ad esempio la colonna ROWID in Oracle. **SQLSpecialColumns** restituisce un elenco di pseudocolonne. Inoltre, se sono presenti restrizioni specifiche dell'applicazione in cui sono sono presenti caratteri speciali nei nomi degli oggetti, è consigliabile per le applicazioni interoperative di non usare caratteri speciali in tali posizioni.
