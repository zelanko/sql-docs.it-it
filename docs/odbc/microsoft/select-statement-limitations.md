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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300921"
---
# <a name="select-statement-limitations"></a>Limitazioni dell'istruzione SELECT
Impossibile combinare una colonna della funzione di aggregazione con una colonna non aggregata in un'istruzione SELECT.  
  
 L'elenco di selezione di un'istruzione SELECT con una clausola GROUP BY può includere solo espressioni della clausola GROUP BY o set Functions.  
  
 L'utilizzo di un asterisco (per la selezione di tutte le colonne) in un'istruzione SELECT contenente una clausola GROUP BY non è supportato. È necessario specificare i nomi delle colonne da selezionare.  
  
 L'uso di una barra verticale in un'istruzione SELECT non è supportato. Se è necessario fare riferimento a un valore di dati che contiene una barra verticale, utilizzare un parametro nell'istruzione SELECT.  
  
 Quando si utilizza un alias di colonna in un'istruzione SELECT, la parola "As" deve precedere l'alias. Ad esempio, "SELECT col1 As a from b". Senza "As", l'istruzione restituirà un errore.  
  
 Se in un'istruzione SELECT viene immesso un nome di colonna errato, viene restituito un errore SQLSTATE 07001, ovvero un numero errato di parametri, anziché un errore SQLSTATE S0022, "Column not found".  
  
 Quando si utilizza il driver Microsoft Excel, se in una colonna viene inserita una stringa vuota, la stringa vuota viene convertita in un valore NULL. un'istruzione SELECT con ricerca eseguita con una stringa vuota nella clausola WHERE non riuscirà in tale colonna.
