---
title: Durata del ciclo del prodotto Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306194"
---
# <a name="length-of-the-product-cycle"></a>Lunghezza del ciclo del prodotto
L'ultima domanda sull'interoperabilità è il tempo. Lo sviluppo di un'applicazione interoperabile richiede in genere più tempo rispetto allo sviluppo di un'applicazione interoperabile. Il motivo è che l'applicazione deve controllare le funzionalità DBMS, eseguire le stesse attività in modo diverso per DBMS diversi, aggirare le funzionalità supportate da alcuni DBMS ma non altri e così via.  
  
 Oltre ai tempi di sviluppo, è necessario considerare la durata del prodotto. Se l'applicazione è progettata per essere utilizzata una sola volta, ad esempio un'applicazione che trasferisce i dati durante la migrazione da un DBMS a un altro, non ha senso renderli interoperabili. L'applicazione verrà utilizzata una sola volta e scartata.  
  
 Se l'applicazione esisterà per un lungo periodo di tempo, potrebbe essere più facile da gestire come applicazione interoperabile. Questo vale anche per le applicazioni personalizzate che hanno un singolo DBMS come destinazione. Il motivo è che il codice interoperabile utilizza un sottoinsieme limitato di funzionalità del database. Il driver è necessario per mantenere tali funzionalità disponibili, anche a fronte di modifiche al DBMS sottostante. Pertanto, il codice interoperabile può spostare l'onere di affrontare le modifiche al DBMS dallo sviluppatore dell'applicazione allo sviluppatore del driver.
