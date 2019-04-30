---
title: SQLGetData e cursori rettangolari | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a14c98f045fd974b404209cc998496dc5fa7193e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149073"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursori rettangolari
**SQLGetData** opera su una singola colonna di una singola riga e non è possibile recuperare una matrice contenente i dati da più righe. Infatti, l'uso primario di **SQLGetData** consiste nel recuperare dati long in parti, e c'è motivo di non offrivano per eseguire questa operazione per più di una riga alla volta.  
  
 Per utilizzare **SQLGetData** con un cursore a blocchi, un'applicazione chiama innanzitutto **SQLSetPos** per posizionare il cursore su una singola riga. Chiama poi **SQLGetData** per una colonna in tale riga. Tuttavia, questo comportamento è facoltativo. Per determinare se un driver supporta l'utilizzo delle **SQLGetData** con cursori a blocchi, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.
