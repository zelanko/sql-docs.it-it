---
title: Limitazioni dell'istruzione SELECT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26bf17596dbd3279498df2edcee7636db95ae139
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127856"
---
# <a name="select-statement-limitations"></a>Limitazioni dell'istruzione SELECT
Una colonna di funzione di aggregazione non può essere combinata con una colonna non di aggregazione in un'istruzione SELECT.  
  
 Elenco di selezione di un'istruzione SELECT che include una clausola GROUP BY può avere solo le espressioni nella clausola GROUP BY o funzioni di set.  
  
 Non è supportato l'uso di un asterisco (per selezionare tutte le colonne) in un'istruzione SELECT contenente una clausola GROUP BY. Specificare i nomi delle colonne da selezionare.  
  
 L'uso di una barra verticale in un'istruzione SELECT non è supportato. Usare un parametro nell'istruzione SELECT se è necessario fare riferimento a un valore di dati che contiene una barra verticale.  
  
 Quando si usa un alias di colonna in un'istruzione SELECT, la parola "as" deve precedere l'alias. Ad esempio, "SELECT col1 come un da b." Senza il "come", l'istruzione restituirà un errore.  
  
 Se viene immesso un nome di colonna non corretto in un'istruzione SELECT, viene restituito un errore SQLSTATE 07001, "Numero di parametri errati," anziché un errore con SQLSTATE S0022, "colonna non trovata."  
  
 Quando viene utilizzato il driver di Microsoft Excel, se una stringa vuota viene inserita in una colonna, una stringa vuota verrà convertita in un valore NULL. un'istruzione SELECT di ricerca che viene eseguita con una stringa vuota nella clausola WHERE non riuscirà per tale colonna.
