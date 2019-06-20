---
title: Supporto delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306040"
---
# <a name="transaction-support"></a>Supporto delle transazioni
Il livello di supporto delle transazioni è definito dal driver. ODBC è progettato per essere implementata in un database utente singolo o desktop che è necessario gestire più aggiornamenti da propri dati. Inoltre, alcuni database che supportano le transazioni di eseguire in modo che solo per le istruzioni Data Manipulation Language (DML) di SQL. Esistono restrizioni o semantica delle transazioni speciali relative all'utilizzo del linguaggio DDL (Data Definition) quando una transazione è attiva. Vale a dire, è possibile il supporto delle transazioni più aggiornamenti simultanei a tabelle, ma non per modificare il numero e la definizione delle tabelle durante una transazione.  
  
 Un'applicazione determina se sono supportate le transazioni, se DDL possono essere inclusi in una transazione e gli effetti speciali di inclusione di DDL in una transazione, chiamando **SQLGetInfo** con l'opzione SQL_TXN_CAPABLE. Per altre informazioni, vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.  
  
 Se il driver non supporta le transazioni, ma l'applicazione è in grado (tramite un'API diversa da ODBC) per bloccare e sbloccare i dati, le applicazioni possono ottenere il supporto delle transazioni dal blocco e sblocco record e tabelle in base alle esigenze. Per implementare l'esempio di trasferimento di account, l'applicazione verrebbe bloccare i record per entrambi gli account, copiare i valori correnti, addebitato il primo account, il secondo account di credito e sbloccare i record. Se non è stato possibile tutti i passaggi, l'applicazione Reimposta gli account con le copie.  
  
 Origini di dati che supportano le transazioni potrebbero non essere in grado di supportare più di una transazione alla volta all'interno di un determinato ambiente. Le applicazioni chiamano **SQLGetInfo** con l'opzione SQL_MULTIPLE_ACTIVE_TXN per determinare se un'origine dati può supportare le transazioni attive simultanee su più connessioni nello stesso ambiente. Poiché è presente una sola transazione per ogni connessione, questo è solo interessano per applicazioni che dispongono di più connessioni alla stessa origine dati.
