---
title: Eseguire il commit e rollback delle transazioni | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7c028ca7e89378e959b11f59cad4119cef5086a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083316"
---
# <a name="committing-and-rolling-back-transactions"></a>Esecuzione del commit e del rollback delle transazioni
Per eseguire il commit o rollback della transazione in modalità di commit manuale, un'applicazione chiama **SQLEndTran**. I driver per DBMS che supportano le transazioni in genere implementano questa funzione tramite l'esecuzione di un **COMMIT** oppure **ROLLBACK** istruzione. Gestione Driver non chiama **SQLEndTran** quando la connessione è in modalità autocommit; semplicemente restituisce SQL_SUCCESS, anche se l'applicazione prova a eseguire il rollback della transazione. Poiché i driver per DBMS che non supportano le transazioni sono sempre in modalità autocommit, è possibile implementare **SQLEndTran** restituisce SQL_SUCCESS senza eseguire alcuna operazione o non implementare.  
  
> [!NOTE]  
>  Le applicazioni non devono eseguire il commit o il rollback delle transazioni eseguendo **COMMIT** oppure **ROLLBACK** istruzioni con **SQLExecute** o **SQLExecDirect**. Gli effetti di questa operazione non sono definiti. I problemi possibili includono il driver non è più sapere quando è attiva una transazione e tali istruzioni non superati rispetto a origini dati che non supportano transazioni. Queste applicazioni devono chiamare **SQLEndTran** invece.  
  
 Se un'applicazione passa l'handle di ambiente al **SQLEndTran** ma non passare un handle di connessione, gestione Driver chiama concettualmente **SQLEndTran** con l'handle di ambiente per ogni driver che dispone di uno o più connessioni attive nell'ambiente. Quindi il driver esegue il commit di transazioni in ogni connessione nell'ambiente. Tuttavia, è importante tenere presente che il driver né the Driver Manager esegue un commit in due fasi sulle connessioni dell'ambiente. si tratta semplicemente una facilitare la programmazione di chiamare simultaneamente **SQLEndTran** per tutte le connessioni nell'ambiente.  
  
 (Un *2PC* viene generalmente usato per eseguire il commit delle transazioni che vengono distribuite tra più origini dati. Nella prima fase, che indica se possono eseguire il commit di loro parte della transazione sono polling per le origini dati. Nella seconda fase, la transazione viene effettivamente eseguito il commit in tutte le origini dati. Se tutte le origini dati di risposta nella prima fase che è Impossibile eseguire il commit della transazione, la seconda fase non viene eseguito.)
