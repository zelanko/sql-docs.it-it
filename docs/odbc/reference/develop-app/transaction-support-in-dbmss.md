---
title: Supporto delle transazioni in DBMSs Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6da6fdc819d8852aadcd7b672ef06e99d46c0ea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298006"
---
# <a name="transaction-support-in-dbmss"></a>Supporto delle transazioni in DBMS
Alcuni database, in particolare i database desktop come dBASE, Paradox e Btrieve, non supportano le transazioni. Anche tra i database che supportano le transazioni, vi è una variazione in quali tipi di istruzioni SQL possono essere in una transazione. Per altre informazioni, vedere l'opzione SQL_TXN_CAPABLE nella descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQL_TXN_CAPABLE option in the SQLGetInfo function description.
