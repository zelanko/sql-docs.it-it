---
title: La libreria di cursori ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a896a5bb41c5530c65573fa22c418199a043f8fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114074"
---
# <a name="the-odbc-cursor-library"></a>Libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Cursori scorrevoli e blocco sono molto utili aggiunte a molte applicazioni. Tuttavia, non tutti i driver supportano blocco e i cursori scorrevoli. Lo stesso vale per gli aggiornamenti posizionati ed eliminare le istruzioni e **SQLSetPos**, che sono descritte nell'aggiornamento dei dati. Pertanto, il componente ODBC di Windows SDK, incluse in precedenza il SDK, in Microsoft Data Access Components (MDAC) include una libreria di cursori. La libreria di cursori implementa blocchi, i cursori statici, per gli aggiornamenti posizionati e istruzioni delete, e **SQLSetPos** per qualsiasi driver che soddisfi il livello di conformità Apri gruppo Standard CLI. La libreria di cursori può essere ridistribuita con le applicazioni ODBC; vedere il contratto di licenza nel SDK per altre informazioni.  
  
 Per usare la libreria di cursori, un'applicazione imposta l'attributo di connessione SQL_ATTR_ODBC_CURSORS prima che si connette all'origine dati. Per altre informazioni sulla libreria di cursori, vedere [appendice f: Libreria di cursori ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
