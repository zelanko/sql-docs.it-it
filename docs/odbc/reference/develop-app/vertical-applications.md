---
title: Applicazioni Verticali Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300376"
---
# <a name="vertical-applications"></a>Applicazioni verticali
Le applicazioni verticali eseguono in genere un'attività ben definita su un singolo DBMS. Ad esempio, un collegamento per la registrazione degli ordini tiene traccia degli ordini di una società. Ciò che questi tipi di applicazioni hanno in comune è che lo schema del database è in genere progettato dallo sviluppatore dell'applicazione e, mentre l'applicazione potrebbe funzionare con un numero di DBMS diversi, funziona con un singolo DBMS per un singolo cliente.  
  
 Poiché le applicazioni verticali richiedono in genere determinate funzionalità, ad esempio cursori scorrevoli o transazioni, raramente supportano tutti i DBSMO. Al contrario, tendono ad essere altamente interoperabili tra una serie limitata di DBSMO. In genere, gli sviluppatori di applicazioni verticali scelgono di supportare i DBSMO che rappresentano una grande frazione del mercato e ignorare il resto. Potrebbero anche scegliere di supportare driver specifici per tali DBS per ridurre i costi di test e supporto del prodotto.  
  
 Poiché le applicazioni verticali possono supportare un set noto di DBMS, a volte contengono codice specifico del driver o DBMS. Tuttavia, tale codice è meglio mantenere al minimo perché richiede più tempo per la manutenzione.
