---
title: Scorrimento e recupero di righe (ODBC) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304202"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Scorrimento e recupero di righe (ODBC)
Quando si utilizza un cursore scorrevole, le applicazioni chiamano **SQLFetchScroll** per posizionare il cursore e recuperare le righe. **SQLFetchScroll** supporta lo scorrimento relativo (successivo, precedente e relativo *n* righe), lo scorrimento assoluto (prima, ultima riga e riga *n*) e il posizionamento in base al segnalibro. Gli argomenti *FetchOrientation* e *FetchOffset* in **SQLFetchScroll** specificano il set di righe da recuperare, come illustrato nei diagrammi seguenti.  
  
 ![Recupero del rowset successivo, precedente, primo e ultimo](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Recupero del rowset successivo, precedente, primo e ultimo**  
  
 ![Recupero di un rowset assoluto, relativo e con segnalibro](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Recupero di set di righe assoluto, relativo e con segnalibro**  
  
 **SQLFetchScroll** posiziona il cursore sulla riga specificata e restituisce le righe nel set di righe a partire da tale riga. Se il set di righe specificato si sovrappone alla fine del set di risultati, viene restituito un set di righe parziale. Se il set di righe specificato si sovrappone all'inizio del set di risultati, viene in genere restituito il primo set di righe nel set di risultati; Per informazioni dettagliate, vedere la descrizione della funzione [SQLFetchScroll.For](../../../odbc/reference/syntax/sqlfetchscroll-function.md) complete details, see the SQLFetchScroll function description.  
  
 In alcuni casi, l'applicazione potrebbe voler posizionare il cursore senza recuperare alcun dato. Ad esempio, potrebbe voler verificare se esiste una riga o semplicemente ottenere il segnalibro per la riga senza portare altri dati in rete. A tale scopo, imposta l'attributo dell'istruzione SQL_ATTR_RETRIEVE_DATA su SQL_RD_OFF. La variabile associata alla colonna del segnalibro (se presente) viene sempre aggiornata, indipendentemente dall'impostazione di questo attributo dell'istruzione.  
  
 Dopo aver recuperato il set di righe, l'applicazione può chiamare **SQLSetPos** per posizionare una determinata riga nel set di righe o aggiornare le righe nel set di righe. Per ulteriori informazioni sull'utilizzo di **SQLSetPos**, vedere [Aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Lo scorrimento è supportato in ODBC 2. *x* driver di **SQLExtendedFetch**. Per altre informazioni, vedere Cursori a [blocchi, cursori scorrevoli e compatibilità](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)con le versioni precedenti nell'appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.
