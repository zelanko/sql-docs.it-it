---
description: Supporto delle transazioni in DBMS
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
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487454"
---
# <a name="transaction-support-in-dbmss"></a>Supporto delle transazioni in DBMS
Alcuni database, in particolare i database desktop come dBASE, Paradox e Btrieve, non supportano le transazioni. Anche tra i database che supportano le transazioni, esistono variazioni nei tipi di istruzioni SQL che possono essere presenti in una transazione. Per ulteriori informazioni, vedere l'opzione SQL_TXN_CAPABLE nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
