---
title: Supporto delle transazioni nei DBMS | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298006"
---
# <a name="transaction-support-in-dbmss"></a>Supporto delle transazioni in DBMS
Alcuni database, in particolare i database desktop come dBASE, Paradox e Btrieve, non supportano le transazioni. Anche tra i database che supportano le transazioni, esistono variazioni nei tipi di istruzioni SQL che possono essere presenti in una transazione. Per ulteriori informazioni, vedere l'opzione SQL_TXN_CAPABLE nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
