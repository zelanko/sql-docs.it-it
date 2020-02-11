---
title: SQLGetData e cursori a blocchi | Microsoft Docs
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
ms.openlocfilehash: 4841d8d923ff73d187569df3d7f9e29daf0f4e48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107404"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursori rettangolari
**SQLGetData** opera su una singola colonna di una singola riga e non è in grado di recuperare una matrice contenente dati da più righe. Questo è dovuto al fatto che l'utilizzo principale di **SQLGetData** è quello di recuperare dati lunghi in parti e non c'è alcun motivo per eseguire questa operazione per più di una riga alla volta.  
  
 Per utilizzare **SQLGetData** con un cursore a blocchi, un'applicazione chiama prima **SQLSetPos** per posizionare il cursore su una singola riga. Viene quindi chiamato **SQLGetData** per una colonna nella riga. Questo comportamento è tuttavia facoltativo. Per determinare se un driver supporta l'utilizzo di **SQLGetData** con cursori a blocchi, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.
