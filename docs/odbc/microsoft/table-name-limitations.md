---
title: Limitazioni del nome della tabella | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289217"
---
# <a name="table-name-limitations"></a>Limitazioni dei nomi di tabella
I nomi delle tabelle possono contenere qualsiasi carattere valido, ad esempio spazi. Se i nomi di tabella contengono caratteri eccetto lettere, numeri e caratteri di sottolineatura, il nome deve essere racchiuso tra virgolette (').  
  
 Quando si utilizza il driver Microsoft Excel e il nome di una tabella non è qualificato da un riferimento al database, il database predefinito è implicito. Se un nome in Microsoft Excel include il carattere "!", verrà convertito automaticamente nel carattere "$".  
  
 Il nome della tabella di Microsoft Excel \<che fa riferimento a filename> è supportato per i file di microsoft Excel 3,0 e 4,0. Il nome della tabella di Microsoft Excel \<che fa riferimento a nome cartella di lavoro> è supportato per i file di microsoft Excel 5,0, 7,0 o 97.  
  
 Quando si usa il driver dBASE, i caratteri con un valore ASCII maggiore di 127 vengono convertiti in caratteri di sottolineatura.  
  
 Quando si utilizza il driver Microsoft Access, il nome della tabella è limitato a 64 caratteri.  
  
 Quando viene usato il driver dBASE, Microsoft Excel 3,0 o 4,0, Paradox o text, le parole chiave MS-DOS speciali CON, AUX, LPT1 e LPT2 non devono essere usate come nomi di tabella.
