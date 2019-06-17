---
title: Supporto delle transazioni in DBMS | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fed5ea04e15002d31e35e25fac405a729929be8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305685"
---
# <a name="transaction-support-in-dbmss"></a>Supporto delle transazioni in DBMS
Alcuni database, in particolare i database desktop, ad esempio Paradox, dBASE e Btrieve, non supportano transazioni. Anche nei database che supportano le transazioni, è variazione nei quali possono essere tipi di istruzioni SQL in una transazione. Per altre informazioni, vedere l'opzione SQL_TXN_CAPABLE nel [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.
