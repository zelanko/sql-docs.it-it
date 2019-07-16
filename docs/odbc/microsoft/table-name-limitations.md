---
title: Limitazioni per i nomi di tabella | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 152a0aa1e8d92424b2f60c49f44888de7d3e528c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939780"
---
# <a name="table-name-limitations"></a>Limitazioni dei nomi di tabella
I nomi di tabella possono contenere qualsiasi carattere validi (ad esempio, spazi). Se i nomi delle tabelle contengono i caratteri tranne lettere, numeri e caratteri di sottolineatura, il nome deve essere delimitato racchiudendolo tra virgolette back (').  
  
 Quando viene usato il driver di Microsoft Excel e un nome di tabella non è qualificato dal riferimento a un database, il database predefinito è implicito. Se un nome in Microsoft Excel include il "!" character, verrà automaticamente tradotto al carattere "$" invece.  
  
 Il nome della tabella che fa riferimento a Microsoft Excel \<nomefile > è supportato per Microsoft Excel 3.0 e 4.0 file. Il nome della tabella che fa riferimento a Microsoft Excel \<della cartella di lavoro-name > è supportato per i file di Microsoft Excel 97, versione 7.0 o 5.0.  
  
 Quando viene usato il driver dBASE, con un valore ASCII maggiore di 127 caratteri vengono convertiti in caratteri di sottolineatura.  
  
 Quando viene usato il driver Microsoft Access, il nome della tabella è limitato a 64 caratteri.  
  
 Quando viene usato il driver di Microsoft Excel versione 3.0 o 4.0, Paradox, o testo, dBASE, parole chiave CON, AUX, LPT1 e LPT2 di speciali MS-DOS non usare come nomi di tabella.
