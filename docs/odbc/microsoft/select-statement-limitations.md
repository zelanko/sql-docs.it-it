---
title: "Limitazioni dell'istruzione SELECT : Documenti Microsoft"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300921"
---
# <a name="select-statement-limitations"></a>Limitazioni dell'istruzione SELECT
Una colonna di funzione di aggregazione non può essere mista a una colonna non aggregata in un'istruzione SELECT.  
  
 L'elenco di selezione di un'istruzione SELECT con una clausola GROUP BY può avere solo espressioni della clausola GROUP BY o funzioni set.  
  
 L'utilizzo di un asterisco (per selezionare tutte le colonne) in un'istruzione SELECT contenente una clausola GROUP BY non è supportato. È necessario specificare i nomi delle colonne da selezionare.  
  
 L'uso di una barra verticale in un'istruzione SELECT non è supportato. Utilizzare un parametro nell'istruzione SELECT se è necessario fare riferimento a un valore di dati che contiene una barra verticale.  
  
 Quando si utilizza un alias di colonna in un'istruzione SELECT, la parola "as" deve precedere l'alias. Ad esempio, "SELECT col1 come a from b." Senza "as", l'istruzione restituirà un errore.  
  
 Se viene immesso un nome di colonna non corretto in un'istruzione SELECT, viene restituito un errore SQLSTATE 07001, "Numero errato di parametri", anziché un errore SQLSTATE S0022, "Colonna non trovata".  
  
 Quando viene utilizzato il driver di Microsoft Excel, se una stringa vuota viene inserita in una colonna, la stringa vuota viene convertita in un valore NULL; un'istruzione SELECT eseguita con una stringa vuota nella clausola WHERE non avrà esito positivo in tale colonna.
