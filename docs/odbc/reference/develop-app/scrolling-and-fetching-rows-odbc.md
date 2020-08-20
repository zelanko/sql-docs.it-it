---
description: Scorrimento e recupero di righe (ODBC)
title: Scorrimento e recupero di righe (ODBC) | Microsoft Docs
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
ms.openlocfilehash: b6fcdd2cd635a7da66a5d81c4beb24088f96382b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476493"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>Scorrimento e recupero di righe (ODBC)
Quando si utilizza un cursore scorrevole, le applicazioni chiamano **SQLFetchScroll** per posizionare il cursore e recuperare le righe. **SQLFetchScroll** supporta lo scorrimento relativo (avanti, precedente e relativo *n* righe), lo scorrimento assoluto (primo, ultimo e riga *n*) e il posizionamento in base al segnalibro. Gli argomenti *FetchOrientation* e *FetchOffset* in **SQLFetchScroll** specificano il set di righe da recuperare, come illustrato nei diagrammi seguenti.  
  
 ![Recupero del rowset successivo, precedente, primo e ultimo](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **Recupero del rowset successivo, precedente, primo e ultimo**  
  
 ![Recupero di un rowset assoluto, relativo e con segnalibro](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **Recupero di set di righe assoluti, relativi e con segnalibro**  
  
 **SQLFetchScroll** posiziona il cursore sulla riga specificata e restituisce le righe nel set di righe che inizia con tale riga. Se il set di righe specificato si sovrappone alla fine del set di risultati, viene restituito un set di righe parziale. Se il set di righe specificato si sovrappone all'inizio del set di risultati, viene in genere restituito il primo set di righe nel set di risultati. per informazioni complete, vedere la descrizione della funzione [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .  
  
 In alcuni casi, l'applicazione potrebbe voler posizionare il cursore senza recuperare i dati. Ad esempio, potrebbe essere necessario verificare se una riga esiste o semplicemente ottenere il segnalibro per la riga senza trasferire altri dati nella rete. A tale scopo, imposta l'attributo dell'istruzione SQL_ATTR_RETRIEVE_DATA su SQL_RD_OFF. La variabile associata alla colonna del segnalibro, se presente, viene sempre aggiornata, indipendentemente dall'impostazione dell'attributo dell'istruzione.  
  
 Dopo che il set di righe è stato recuperato, l'applicazione può chiamare **SQLSetPos** per posizionarsi in una riga specifica del set di righe o aggiornare le righe nel set di righe. Per altre informazioni sull'uso di **SQLSetPos**, vedere [aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
> [!NOTE]  
>  Lo scorrimento è supportato in ODBC 2. driver *x* per **SQLExtendedFetch**. Per ulteriori informazioni, vedere [cursori a blocchi, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)in Appendice G: linee guida per la compatibilità con le versioni precedenti.
