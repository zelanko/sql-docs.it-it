---
title: Argomenti di valore di modello Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0b8e7b7de64d8051118089a54cf14eb45dc96f74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282381"
---
# <a name="pattern-value-arguments"></a>Argomenti del valore dei criteri
Alcuni argomenti nelle funzioni di catalogo, ad esempio l'argomento *TableName* in **SQLTables**, accettano i criteri di ricerca. Questi argomenti accettano i criteri di ricerca se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; sono argomenti di identificatore che non accettano un criterio di ricerca se questo attributo è impostato su SQL_TRUE.  
  
 I caratteri del criterio di ricerca sono:  
  
-   Un carattere di sottolineatura (_), che rappresenta qualsiasi carattere singolo.  
  
-   Un segno di percentuale (%), che rappresenta qualsiasi sequenza di zero o più caratteri.  
  
-   Un carattere di escape, specifico del driver e utilizzato per includere caratteri di sottolineatura, segni di percentuale e il carattere di escape come valori letterali. Se il carattere di escape precede un carattere non speciale, il carattere di escape non ha alcun significato speciale. Se il carattere di escape precede un carattere speciale, esegue l'escape del carattere speciale. Ad esempio, "a" verrebbe considerato come\\due caratteri, "\\" e "a", ma " %" verrebbe considerato come il carattere singolo non speciale "%".  
  
 Il carattere di escape viene recuperato con l'opzione SQL_SEARCH_PATTERN_ESCAPE in **SQLGetInfo**. Deve precedere qualsiasi carattere di sottolineatura, segno di percentuale o carattere di escape in un argomento che accetta i criteri di ricerca per includere tale carattere come valore letterale. Gli esempi sono illustrati nella tabella seguente.  
  
|Modello di ricerca|Descrizione|  
|--------------------|-----------------|  
|%A%|Tutti gli identificatori contenenti la lettera A|  
|ABC_|Tutti e quattro gli identificatori di carattere che iniziano con ABC|  
|ABC\\_|L'identificatore ABC_, presupponendo che il\\carattere di escape sia una barra rovesciata ( )|  
|\\\\%|Tutti gli identificatori che\\iniziano con una barra rovesciata ( ), presupponendo che il carattere di escape sia una barra rovesciata|  
  
 È necessario prestare particolare attenzione per eseguire l'escape dei caratteri dei modelli di ricerca negli argomenti che accettano i criteri di ricerca. Ciò è particolarmente vero per il carattere di sottolineatura, che viene comunemente utilizzato negli identificatori. Un errore comune nelle applicazioni consiste nel recuperare un valore da una funzione di catalogo e passare tale valore a un argomento del criterio di ricerca in un'altra funzione di catalogo. Si supponga, ad esempio, che un'applicazione recuperi il nome della tabella MY_TABLE dal set di risultati per **SQLTables** e lo passi a **SQLColumns** per recuperare un elenco di colonne in MY_TABLE. Anziché ottenere le colonne per MY_TABLE, l'applicazione otterrà le colonne per tutte le tabelle che corrispondono al MY_TABLE del criterio di ricerca, ad esempio MY_TABLE, MY1TABLE, MY2TABLE e così via.  
  
> [!NOTE]
>  ODBC 2. *I* driver x non supportano i modelli di ricerca nell'argomento *CatalogName* in **SQLTables**. I driver*x* ODBC 3 accettano modelli di ricerca in questo argomento se l'attributo di ambiente SQL_ATTR_ ODBC_VERSION è impostato su SQL_OV_ODBC3; non accettano criteri di ricerca in questo argomento se è impostato su SQL_OV_ODBC2.  
  
 Il passaggio di un puntatore null a un argomento del criterio di ricerca non vincola la ricerca di tale argomento; ovvero un puntatore null e la % del criterio di ricerca (qualsiasi carattere) sono equivalenti. Tuttavia, un criterio di ricerca di lunghezza zero, ovvero un puntatore valido a una stringa di lunghezza zero, corrisponde solo alla stringa vuota ("").
