---
title: Esecuzione del commit e rollback delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299111"
---
# <a name="committing-and-rolling-back-transactions"></a>Esecuzione del commit e del rollback delle transazioni
Per eseguire il commit o il rollback di una transazione in modalità di commit manuale, un'applicazione chiama **SQLEndTran**. I driver per DBMS che supportano le transazioni in genere implementano questa funzione eseguendo un'istruzione **commit** o **rollback** . Gestione driver non chiama **SQLEndTran** quando la connessione è in modalità autocommit; restituisce semplicemente SQL_SUCCESS, anche se l'applicazione tenta di eseguire il rollback della transazione. Poiché i driver per DBMS che non supportano le transazioni sono sempre in modalità autocommit, possono implementare **SQLEndTran** per restituire SQL_SUCCESS senza eseguire alcuna operazione o non implementarlo affatto.  
  
> [!NOTE]  
>  Le applicazioni non devono eseguire il commit o il rollback delle transazioni eseguendo istruzioni **commit** o **rollback** con **SQLExecute** o **SQLExecDirect**. Gli effetti di questa operazione non sono definiti. Tra i possibili problemi, il driver non è più in grado di sapere quando una transazione è attiva e le istruzioni non vengono eseguite su origini dati che non supportano le transazioni. Queste applicazioni devono invece chiamare **SQLEndTran** .  
  
 Se un'applicazione passa l'handle di ambiente a **SQLEndTran** ma non passa un handle di connessione, gestione driver chiama concettualmente **SQLEndTran** con l'handle di ambiente per ogni driver con una o più connessioni attive nell'ambiente. Il driver quindi eseguirà il commit delle transazioni in ogni connessione nell'ambiente. Tuttavia, è importante tenere presente che né il driver né Gestione driver eseguono un commit a due fasi sulle connessioni nell'ambiente. si tratta semplicemente di una praticità di programmazione per chiamare simultaneamente **SQLEndTran** per tutte le connessioni nell'ambiente.  
  
 Viene in genere utilizzato un *commit a due fasi* per eseguire il commit delle transazioni distribuite tra più origini dati. Nella prima fase, viene eseguito il polling delle origini dati per determinare se è possibile eseguire il commit della propria parte della transazione. Nella seconda fase, viene effettivamente eseguito il commit della transazione in tutte le origini dati. Se le origini dati rispondono nella prima fase in cui non è possibile eseguire il commit della transazione, la seconda fase non si verifica.
