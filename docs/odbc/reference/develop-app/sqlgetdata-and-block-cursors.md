---
title: Cursori SQLGetData e Block Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299751"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursori rettangolari
**SQLGetData** opera su una singola colonna di una singola riga e non può recuperare una matrice contenente dati da più righe. Questo perché l'uso principale di **SQLGetData** è quello di recuperare dati lunghi in parti e non c'è motivo o nessun motivo per eseguire questa operazione per più di una riga alla volta.  
  
 Per utilizzare **SQLGetData** con un cursore a blocchi, un'applicazione chiama prima **SQLSetPos** per posizionare il cursore su una singola riga. Chiama quindi **SQLGetData** per una colonna in tale riga. Tuttavia, questo comportamento è facoltativo. Per determinare se un driver supporta l'utilizzo di **SQLGetData** con cursori a blocchi, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.
