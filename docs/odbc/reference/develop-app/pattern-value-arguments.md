---
title: Modello valore argomenti | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f4a32d9ab637de5b52466cfcb628a57ff6c044b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861728"
---
# <a name="pattern-value-arguments"></a>Argomenti del valore dei criteri
Alcuni argomenti nel catalogo di funzioni, ad esempio la *TableName* nell'argomento **SQLTables**, accettare i criteri di ricerca. Questi argomenti accettano criteri di ricerca se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; argomenti di tipo identificatore che non accettano un criterio di ricerca se questo attributo è impostato su SQL_TRUE sono.  
  
 I caratteri di pattern di ricerca sono:  
  
-   Un carattere di sottolineatura (_), che rappresenta qualsiasi carattere singolo.  
  
-   Un segno di percentuale, %, che rappresenta qualsiasi sequenza di zero o più caratteri.  
  
-   Un carattere di escape, che è specifico del driver e viene usato per includere caratteri di sottolineatura, segni di percentuale, e il carattere di escape come valori letterali. Se il carattere di escape precede un carattere non speciali, il carattere di escape non ha alcun significato speciale. Se il carattere di escape precede un carattere speciale, viene eseguito l'escape del carattere speciale. Ad esempio, "\a" verrebbe considerato come due caratteri, "\\" e "a", ma "\\%" verrebbe considerato come il carattere singolo non speciali "%".  
  
 Il carattere di escape viene recuperato con l'opzione SQL_SEARCH_PATTERN_ESCAPE **SQLGetInfo**. In un argomento che accetta i criteri di ricerca per includere tale carattere come valore letterale deve precedere qualsiasi carattere di sottolineatura, un segno di percentuale o un carattere di escape. Nella tabella seguente sono riportati alcuni esempi.  
  
|Criterio di ricerca|Descrizione|  
|--------------------|-----------------|  
|%A%|Tutti gli identificatori che contengono la lettera A|  
|ABC_|Tutti gli identificatori di quattro caratteri iniziano con ABC|  
|ABC\\_|L'identificatore ABC, presupponendo che il carattere di escape è una barra rovesciata (\\)|  
|\\\\%|Tutti gli identificatori che iniziano con una barra rovesciata (\\), presupponendo che il carattere di escape è una barra rovesciata|  
  
 Particolare attenzione per eseguire l'escape di caratteri di ricerca del modello negli argomenti di accettano i criteri di ricerca. Ciò è particolarmente vero per il carattere di sottolineatura, che viene usato comunemente negli identificatori. Un errore comune nelle applicazioni consiste nel recuperare un valore di una funzione di catalogo e passa tale valore a un argomento di modello di ricerca in un'altra funzione di catalogo. Ad esempio, si supponga che un'applicazione recupera il nome della tabella MY_TABLE dal risultato impostato per **SQLTables** e la passa a **SQLColumns** per recuperare un elenco di colonne in MY_TABLE. Anziché ottenere le colonne per MY_TABLE, l'applicazione recupererà le colonne per tutte le tabelle che corrispondono al criterio di ricerca MY_TABLE, ad esempio MY_TABLE MY1TABLE, MY2TABLE e così via.  
  
> [!NOTE]
>  ODBC 2. *x* driver non supportano i criteri di ricerca nel *CatalogName* argomento nel **SQLTables**. ODBC 3*x* driver accettano criteri di ricerca in questo argomento se l'attributo di ambiente sql_attr ODBC_VERSION è impostato su SQL_OV_ODBC3; non accetta i criteri di ricerca in questo argomento se è impostato su SQL_OV_ODBC2.  
  
 Passando un puntatore null a un argomento di modello di ricerca non vincola la ricerca per tale argomento. vale a dire, un puntatore null e la percentuale di pattern di ricerca (caratteri) sono equivalenti. Tuttavia, un criterio di ricerca di lunghezza zero, vale a dire, un puntatore valido a una stringa di lunghezza zero - corrisponde solo una stringa vuota ("").
