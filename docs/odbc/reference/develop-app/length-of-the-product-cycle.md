---
title: Lunghezza del ciclo di prodotto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306194"
---
# <a name="length-of-the-product-cycle"></a>Lunghezza del ciclo del prodotto
La domanda finale sull'interoperabilità è il tempo. Lo sviluppo di un'applicazione interoperativa richiede in genere più tempo rispetto allo sviluppo di uno noninteroperable. Il motivo è che l'applicazione deve controllare le funzionalità DBMS, eseguire le stesse attività in modo diverso per DBMS diversi, aggirare le funzionalità supportate da alcuni DBMS, ma non altri, e così via.  
  
 Oltre al tempo di sviluppo, è necessario prendere in considerazione la durata del prodotto. Se l'applicazione è progettata per essere usata una sola volta, ad esempio un'applicazione che trasferisce dati quando si esegue la migrazione da un sistema DBMS a un altro, non esiste alcun punto per renderlo interoperativo. L'applicazione verrà utilizzata una volta ed eliminata.  
  
 Se l'applicazione sarà disponibile per molto tempo, potrebbe essere più facile da gestire come applicazione interoperativa. Questo vale anche per le applicazioni personalizzate con un singolo sistema DBMS come destinazione. Il motivo è che il codice interoperativo usa un subset limitato di funzionalità di database. Il driver è necessario per rendere disponibili tali funzionalità, anche in caso di modifiche al sistema DBMS sottostante. Pertanto, il codice interoperabile può spostare il carico di fronte alle modifiche al sistema DBMS dallo sviluppatore di applicazioni allo sviluppatore del driver.
