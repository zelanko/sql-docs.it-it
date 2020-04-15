---
title: 'Passaggio 5: Eseguire il commit della transazione . Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283351"
---
# <a name="step-5-commit-the-transaction"></a>Passaggio 5: Eseguire il commit della transazione
Il passaggio successivo consiste nell'eseguire il commit della transazione, come illustrato nella figura seguente.  
  
 ![Come eseguire il commit di una transazione](../../../odbc/reference/develop-app/media/pr16.gif "PR16 (informazioni in inglese)")  
  
 Il quinto passaggio consiste nel chiamare **SQLEndTran** per eseguire il commit o il rollback della transazione. L'applicazione esegue questo passaggio solo se imposta la modalità di commit della transazione su manual-commit; se la modalità di commit della transazione è auto-commit, che è l'impostazione predefinita, viene eseguito automaticamente il commit della transazione quando viene eseguita l'istruzione. Per altre informazioni, vedere [Transazioni](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Per eseguire un'istruzione in una nuova transazione, l'applicazione torna al passaggio 3.To execute a statement in a new transaction, the application returns to step 3. Per disconnettersi dall'origine dati, l'applicazione procede al passaggio 6.
