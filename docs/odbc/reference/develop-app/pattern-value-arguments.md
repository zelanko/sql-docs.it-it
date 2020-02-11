---
title: Argomenti del valore del criterio | Microsoft Docs
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
ms.openlocfilehash: 53c091fd0b7a6cfdf390997fb5163fbc9d98e18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023345"
---
# <a name="pattern-value-arguments"></a>Argomenti del valore dei criteri
Alcuni argomenti nelle funzioni del catalogo, ad esempio l'argomento *TableName* in **SQLTables**, accettano i criteri di ricerca. Questi argomenti accettano i criteri di ricerca se l'attributo SQL_ATTR_METADATA_ID Statement è impostato su SQL_FALSE; si tratta di argomenti identificatore che non accettano un criterio di ricerca se questo attributo è impostato su SQL_TRUE.  
  
 I caratteri del criterio di ricerca sono:  
  
-   Carattere di sottolineatura (_), che rappresenta un carattere singolo.  
  
-   Segno di percentuale (%), che rappresenta qualsiasi sequenza di zero o più caratteri.  
  
-   Un carattere di escape, che è specifico del driver e viene usato per includere caratteri di sottolineatura, segni percentuali e il carattere di escape come valori letterali. Se il carattere di escape precede un carattere non speciale, il carattere di escape non ha un significato speciale. Se il carattere di escape precede un carattere speciale, evita il carattere speciale. Ad esempio, "\a" verrebbe considerato come due caratteri, "\\" e "a", ma "\\%" verrebbe considerato come il carattere singolo non speciale "%".  
  
 Il carattere di escape viene recuperato con l'opzione SQL_SEARCH_PATTERN_ESCAPE in **SQLGetInfo**. Deve precedere un carattere di sottolineatura, un segno di percentuale o un carattere di escape in un argomento che accetta i criteri di ricerca per includere tale carattere come valore letterale. Nella tabella seguente sono riportati alcuni esempi.  
  
|Criteri di ricerca|Descrizione|  
|--------------------|-----------------|  
|Un|Tutti gli identificatori contenenti la lettera A|  
|ABC_|Tutti i quattro identificatori di caratteri che iniziano con ABC|  
|ABC\\_|Identificatore ABC_, supponendo che il carattere di escape sia una\\barra rovesciata ()|  
|\\\\%|Tutti gli identificatori che iniziano con una\\barra rovesciata (), supponendo che il carattere di escape sia una barra rovesciata|  
  
 È necessario prestare particolare attenzione per eseguire l'escape di caratteri del criterio di ricerca negli argomenti che accettano i criteri di ricerca. Ciò è particolarmente vero per il carattere di sottolineatura, comunemente utilizzato negli identificatori. Un errore comune nelle applicazioni consiste nel recuperare un valore da una funzione di catalogo e passare tale valore a un argomento del criterio di ricerca in un'altra funzione di catalogo. Si supponga, ad esempio, che un'applicazione recuperi il nome della tabella MY_TABLE dal set di risultati per **SQLTables** e lo passi a **SQLColumns** per recuperare un elenco di colonne nel MY_TABLE. Anziché recuperare le colonne per MY_TABLE, l'applicazione otterrà le colonne per tutte le tabelle che corrispondono ai criteri di ricerca MY_TABLE, ad esempio MY_TABLE, MY1TABLE, MY2TABLE e così via.  
  
> [!NOTE]
>  ODBC 2. i driver *x* non supportano i criteri di ricerca nell'argomento *CatalogName* di **SQLTables**. I driver ODBC 3 *. x* accettano i criteri di ricerca in questo argomento se l'attributo SQL_ATTR_ ODBC_VERSION Environment è impostato su SQL_OV_ODBC3; non accettano i criteri di ricerca in questo argomento se è impostato su SQL_OV_ODBC2.  
  
 Il passaggio di un puntatore null a un argomento del criterio di ricerca non vincola la ricerca di tale argomento; ovvero, un puntatore null e il criterio di ricerca% (qualsiasi carattere) sono equivalenti. Tuttavia, un criterio di ricerca di lunghezza zero, ovvero un puntatore valido a una stringa di lunghezza zero-corrisponde solo alla stringa vuota ("").
