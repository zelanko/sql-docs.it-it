---
title: La libreria di cursori ODBC - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300051"
---
# <a name="the-odbc-cursor-library"></a>Libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 I cursori a blocchi e scorrevoli sono aggiunte molto utili a molte applicazioni. Tuttavia, non tutti i driver supportano i cursori di blocco e scorrevoli. Lo stesso vale per le istruzioni di aggiornamento ed eliminazione posizionate e **SQLSetPos**, descritte in Aggiornamento dei dati. Pertanto, il componente ODBC di Windows SDK, precedentemente incluso in Microsoft Data Access Components (MDAC) SDK, include una libreria di cursori. La libreria di cursori implementa le istruzioni di blocco, i cursori statici, le istruzioni di aggiornamento ed eliminazione posizionate e **SQLSetPos** per qualsiasi driver che soddisfi il livello di conformità Open Group Standard CLI. La libreria di cursori può essere ridistribuita con le applicazioni ODBC; Per ulteriori informazioni, vedere il contratto di licenza nell'SDK.  
  
 Per utilizzare la libreria di cursori, un'applicazione imposta l'attributo di connessione SQL_ATTR_ODBC_CURSORS prima che si connetta all'origine dati. Per ulteriori informazioni sulla libreria di [cursori, vedere Appendice F: Libreria di cursori ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
