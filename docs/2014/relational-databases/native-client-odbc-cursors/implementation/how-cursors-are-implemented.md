---
title: La modalità di implementazione dei cursori | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c92391b1d8874da3a8901ccc5c6245e48334241
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188515"
---
# <a name="how-cursors-are-implemented"></a>Modalità di implementazione dei cursori
  Le applicazioni ODBC controllano il comportamento di un cursore impostando uno o più attributi di istruzione prima di eseguire un'istruzione SQL. In ODBC sono disponibili due modalità diverse per specificare le caratteristiche di un cursore:  
  
-   Tipo di cursore  
  
     Tipi di cursore vengono impostati usando l'attributo SQL_ATTR_CURSOR_TYPE di [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). I tipi di cursore ODBC sono forward-only, statici, gestiti da keyset, misti e dinamici. L'impostazione del tipo di cursore è stato il metodo originale utilizzato per la specifica di cursori in ODBC.  
  
-   Comportamento dei cursori  
  
     Comportamento del cursore viene impostato utilizzando gli attributi SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY di **SQLSetStmtAttr**. Questi attributi vengono modellati sulle parole chiave SCROLL e SENSITIVE definite per l'istruzione DECLARE CURSOR negli standard ISO. Queste due opzioni ISO sono state introdotte in ODBC versione 3.0.  
  
 Le caratteristiche di un cursore ODBC devono essere specificate utilizzando uno dei due metodi appena descritti. In genere prevale l'utilizzo dei tipi di cursore ODBC.  
  
 Oltre a impostare il tipo di un cursore, nelle applicazioni ODBC vengono impostate anche altre opzioni, ad esempio il numero di righe restituite in ciascun recupero, le opzioni di concorrenza e i livelli di isolamento delle transazioni. Queste opzioni possono essere impostate per i cursori di tipo ODBC (forward-only, statico, gestito da keyset, misto e dinamico) o per i cursori di tipo ISO (scorrimento e sensibilità).  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta diversi metodi per implementare fisicamente i vari tipi di cursori. Alcuni tipi di cursori vengono implementati mediante un set di risultati predefinito di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], altri come cursori del server o tramite la libreria dei cursori ODBC.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Uso dei set di risultati predefiniti di SQL Server](using-sql-server-default-result-sets.md)  
  
-   [Uso dei cursori server](using-server-cursors.md)  
  
-   [Libreria di cursori ODBC](odbc-cursor-library.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;ODBC&#41;](../using-cursors-odbc.md)  
  
  
