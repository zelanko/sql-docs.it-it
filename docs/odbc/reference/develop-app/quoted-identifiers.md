---
description: Identificatori delimitati
title: Identificatori delimitati | Microsoft Docs
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
ms.openlocfilehash: cd317e5d92618d8b458d6d28fa870c6945e136fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465681"
---
# <a name="quoted-identifiers"></a>Identificatori delimitati
In un'istruzione SQL, gli identificatori contenenti caratteri speciali o parole chiave corrispondenti devono essere racchiusi tra *virgolette*. gli identificatori racchiusi in tali caratteri sono noti come *identificatori tra virgolette* (noti anche come *identificatori delimitati* in SQL-92). Nell'istruzione **Select** seguente, ad esempio, l'identificatore contabilità fornitori è racchiuso tra virgolette:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Il motivo per cui vengono citati gli identificatori consiste nel rendere l'istruzione analizzabile. Se, ad esempio, gli account pagabili non erano racchiusi tra virgolette nell'istruzione precedente, il parser presumerebbe che fossero presenti due tabelle, account e pagabili e restituisse un errore di sintassi che non erano separate da virgole. Il carattere virgoletta identificatore è specifico del driver e viene recuperato con l'opzione SQL_IDENTIFIER_QUOTE_CHAR in **SQLGetInfo**. Gli elenchi di caratteri speciali e di parole chiave vengono recuperati con le opzioni SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS in **SQLGetInfo**.  
  
 Per essere sicuri, le applicazioni interoperative spesso citano tutti gli identificatori tranne quelli per le pseudo-colonne, ad esempio la colonna ROWID in Oracle. **SQLSpecialColumns** restituisce un elenco di pseudo-colonne. Inoltre, se sono presenti restrizioni specifiche dell'applicazione in cui è possibile visualizzare i caratteri speciali in un nome di oggetto, è preferibile che le applicazioni interoperative non usino caratteri speciali in tali posizioni.
