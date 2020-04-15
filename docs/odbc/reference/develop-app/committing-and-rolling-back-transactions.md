---
title: Commit e rollback delle transazioni Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299111"
---
# <a name="committing-and-rolling-back-transactions"></a>Esecuzione del commit e del rollback delle transazioni
Per eseguire il commit o il rollback di una transazione in modalità di commit manuale, un'applicazione chiama **SQLEndTran**. I driver per DBSMO che supportano le transazioni in genere implementano questa funzione eseguendo un'istruzione **COMMIT** o **ROLLBACK.** Gestione Driver non chiama **SQLEndTran** quando la connessione è in modalità di commit automatico; restituisce semplicemente SQL_SUCCESS, anche se l'applicazione tenta di eseguire il rollback della transazione. Poiché i driver per DBMS che non supportano le transazioni sono sempre in modalità di commit automatico, possono implementare **SQLEndTran** per restituire SQL_SUCCESS senza eseguire alcuna operazione o non implementarlo affatto.  
  
> [!NOTE]  
>  Le applicazioni non devono eseguire il commit o il rollback delle transazioni eseguendo istruzioni **COMMIT** o **ROLLBACK** con **SQLExecute** o **SQLExecDirect**. Gli effetti di questa operazione sono indefiniti. I possibili problemi includono che il driver non sappia più quando una transazione è attiva e queste istruzioni non riescono a eseguire le origini dati che non supportano le transazioni. Queste applicazioni devono chiamare invece **SQLEndTran.These** applications should call SQLEndTran instead.  
  
 Se un'applicazione passa l'handle di ambiente a **SQLEndTran** ma non passa un handle di connessione, Gestione Driver chiama concettualmente **SQLEndTran** con l'handle di ambiente per ogni driver che dispone di una o più connessioni attive nell'ambiente. Il driver esegue quindi il commit delle transazioni su ogni connessione nell'ambiente. Tuttavia, è importante tenere presente che né il driver né Gestione Driver esegue un commit in due fasi sulle connessioni nell'ambiente; si tratta semplicemente di una comodità di programmazione per chiamare contemporaneamente **SQLEndTran** per tutte le connessioni nell'ambiente.  
  
 Un *commit in due fasi* viene in genere utilizzato per eseguire il commit di transazioni distribuite su più origini dati. Nella prima fase, viene eseguito il polling delle origini dati per verificare se è possibile eseguire il commit della parte della transazione. Nella seconda fase, viene effettivamente eseguito il commit della transazione in tutte le origini dati. Se nella prima fase le origini dati rispondono di cui non è possibile eseguire il commit della transazione, la seconda fase non si verifica.)
