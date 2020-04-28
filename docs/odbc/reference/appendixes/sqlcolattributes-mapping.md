---
title: Mapping di SQLColAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305417"
---
# <a name="sqlcolattributes-mapping"></a>Mapping di SQLColAttributes
Quando un'applicazione chiama **SQLColAttributes** tramite un driver ODBC *3. x* , viene eseguito il mapping della chiamata a **SQLColAttributes** a **SQLColAttribute** come indicato di seguito:  
  
> [!NOTE]
>  Il prefisso utilizzato nei valori *FieldIdentifier* in ODBC *3. x* è stato modificato rispetto a quello utilizzato in ODBC *2. x*. Il nuovo prefisso è "SQL_DESC"; il prefisso precedente è "SQL_COLUMN".  
  
1.  Se l'applicazione è un'applicazione ODBC *2. x* , *fDescType* è SQL_COLUMN_TYPE e il tipo restituito è un tipo DateTime conciso, gestione driver esegue il mapping dei valori restituiti per i codici di data, ora e timestamp.  
  
2.  Se *fDescType* è SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE o SQL_COLUMN_COUNT, gestione driver chiama **SQLColAttribute** nel driver con l'argomento *FieldIdentifier* mappato a SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, a seconda dei casi *.* Tutti gli altri valori di *fDescType* vengono passati al driver.  
  
 Un driver ODBC *3. x* deve supportare tutti i *FieldIdentifiers* ODBC *3. x* elencati per **SQLColAttribute**.  
  
 Un driver ODBC *3. x* deve supportare SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Questi valori sono diversi perché la precisione, la scala e la lunghezza sono definite in modo diverso in ODBC *3. x* rispetto a ODBC *2. x*. Per ulteriori informazioni, vedere [dimensioni della colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Appendice D: tipi di dati.
