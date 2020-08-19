---
description: Driver basati su file
title: Driver basati su file | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 770e8560c540e8423aebf0a79c0e8ee5c124c8e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429083"
---
# <a name="file-based-drivers"></a>Driver basati su file
I driver basati su file vengono usati con origini dati, ad esempio dBASE, che non forniscono un motore di database autonomo per il driver da usare. Questi driver accedono direttamente ai dati fisici e devono implementare un motore di database per l'elaborazione di istruzioni SQL. Come procedura standard, i motori di database nei driver basati su file implementano il subset di ODBC SQL definito dal livello di conformità SQL minimo. per un elenco delle istruzioni SQL in questo livello di conformità, vedere [Appendice C: grammatica SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Nel confronto di driver basati su file e DBMS, i driver basati su file sono più difficili da scrivere a causa del componente del motore di database, meno complicati da configurare perché non ci sono parti di rete e meno potenti perché poche persone hanno il tempo di scrivere motori di database potenti come quelli prodotti dalle società di database.  
  
 Nella figura seguente sono illustrate due diverse configurazioni di driver basati su file, una in cui i dati risiedono localmente e l'altro in cui si trovano in una rete file server.  
  
 ![Due configurazioni di driver basati su file&#45;](../../odbc/reference/media/pr06.gif "pr06")
