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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e216fae50bf8f4bd37f294abcc14be98ad4f69ea
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793021"
---
# <a name="sqlcolattributes-mapping"></a>Mapping di SQLColAttributes
Quando un'applicazione chiama **SQLColAttributes** tramite un database ODBC *3.x* driver, la chiamata al **SQLColAttributes** è mappato a **SQLColAttribute** come indicato di seguito:  
  
> [!NOTE]
>  Il prefisso utilizzato nelle *FieldIdentifier* i valori in ODBC *3.x* è stato modificato da tale utilizzato in ODBC *2.x*. Il nuovo prefisso è "SQL_DESC"; il prefisso precedente era "SQL_COLUMN".  
  
1.  Se l'applicazione è un database ODBC *2.x* applicazione *fDescType* è SQL_COLUMN_TYPE e il tipo restituito è un tipo DATETIME conciso, le mappe di gestione Driver la restituzione di valori per data, ora e timestamp codici.  
  
2.  Se *fDescType* è SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE o SQL_COLUMN_COUNT, le chiamate di gestione Driver **SQLColAttribute** nel driver con il *FieldIdentifier* argomento mappata SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, come appropriato *.* Tutti gli altri valori della *fDescType* vengono passati al driver.  
  
 Un database ODBC *3.x* driver devono supportare tutte ODBC *3.x* *FieldIdentifiers* elencati per **SQLColAttribute**.  
  
 Un database ODBC *3.x* driver devono supportare SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Questi valori sono diversi perché la precisione, scala e lunghezza vengono definite in modo diverso in ODBC *3.x* rispetto a ODBC *2.x*. Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) nell'appendice d: Tipi di dati.
