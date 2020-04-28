---
title: Cursori statici ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282446"
---
# <a name="odbc-static-cursors"></a>Cursori statici ODBC
Un cursore statico è quello in cui il set di risultati sembra essere statico. Non rileva in genere le modifiche apportate all'appartenenza, all'ordine o ai valori del set di risultati dopo l'apertura del cursore. Si supponga, ad esempio, che un cursore statico recuperi una riga e un'altra applicazione aggiorni la riga. Se il cursore statico recupera la riga, i valori che visualizza sono invariati, nonostante le modifiche apportate dall'altra applicazione.  
  
 I cursori statici possono rilevare gli aggiornamenti, le eliminazioni e gli inserimenti, sebbene non siano necessari per eseguire questa operazione. Il fatto che un determinato cursore statico rilevi queste modifiche viene segnalato tramite l'opzione SQL_STATIC_SENSITIVITY in **SQLGetInfo**. I cursori statici non rilevano mai altri aggiornamenti, eliminazioni e inserimenti.  
  
 La matrice di stato della riga specificata dall'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR per qualsiasi riga. Viene restituito SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED per le righe aggiornate, eliminate o inserite dal cursore, supponendo che il cursore possa rilevare tali modifiche.  
  
 I cursori statici vengono in genere implementati bloccando le righe nel set di risultati oppure creando una copia, o snapshot, del set di risultati. Sebbene il blocco delle righe sia relativamente semplice, presenta lo svantaggio della riduzione significativa della concorrenza. La creazione di una copia consente una maggiore concorrenza e consente al cursore di tenere traccia dei propri aggiornamenti, eliminazioni e inserimenti modificando la copia. Tuttavia, una copia è più costosa da creare e può divergere dai dati sottostanti poiché i dati vengono modificati da altri.
