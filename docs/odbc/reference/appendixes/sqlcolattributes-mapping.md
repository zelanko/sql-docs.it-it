---
title: 'Mapping di SQLColAttributes : Documenti Microsoft'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305417"
---
# <a name="sqlcolattributes-mapping"></a>Mapping di SQLColAttributes
Quando un'applicazione chiama **SQLColAttributes** tramite un driver ODBC *3.x,* la chiamata a **SQLColAttributes** viene mappata a **SQLColAttribute** come segue:  
  
> [!NOTE]
>  Il prefisso utilizzato nei valori *FieldIdentifier* in ODBC *3.x* è stato modificato rispetto a quello utilizzato in ODBC *2.x*. Il nuovo prefisso è "SQL_DESC"; il prefisso precedente era "SQL_COLUMN".  
  
1.  Se l'applicazione è un'applicazione ODBC *2.x,* *fDescType* è SQL_COLUMN_TYPE e il tipo restituito è un tipo DATETIME conciso, Gestione Driver esegue il mapping dei valori restituiti per i codici di data, ora e timestamp.  
  
2.  Se *fDescType* è SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE o SQL_COLUMN_COUNT, Gestione Driver chiama **SQLColAttribute** nel driver con il *FieldIdentifier* argomento mappato a SQL_DESC_NAME, SQL_DESC_NULLABLE o SQL_DESC_COUNT, come appropriato *.* Tutti gli altri valori di *fDescType* vengono passati al driver.  
  
 Un driver ODBC *3.x* deve supportare tutti i *fieldIdentifiers* ODBC *3.x* elencati per **SQLColAttribute**.  
  
 Un driver ODBC *3.x* deve supportare SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Questi valori sono diversi perché precisione, scala e lunghezza sono definiti in modo diverso in ODBC *3.x* rispetto a ODBC *2.x*. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) di visualizzazione nell'Appendice D: Tipi di dati.
