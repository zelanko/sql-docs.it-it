---
title: L'esecuzione di procedure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff234d1d8e099611c8718eac5ae3b584e926a2bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061969"
---
# <a name="executing-procedures"></a>Esecuzione di procedure
ODBC definisce una sequenza di escape standard per l'esecuzione di procedure. Per la sintassi di questa sequenza e un esempio di codice che lo utilizza, vedere [le chiamate di procedura](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Per eseguire una routine, un'applicazione esegue le azioni seguenti:  
  
1.  Imposta i valori dei parametri. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
2.  Le chiamate **SQLExecDirect** e lo passa a una stringa contenente l'istruzione SQL che esegue la procedura. Questa istruzione consente di usare la sequenza di escape definita dalla sintassi ODBC o specifici del DBMS; le istruzioni che utilizzano la sintassi specifici del DBMS non sono interoperative.  
  
3.  Quando **SQLExecDirect** viene chiamato, il driver:  
  
    -   Recupera i valori di parametro corrente e li converte in base alle esigenze. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   La routine viene chiamata nell'origine dati e lo invia i valori di parametro convertito. Come il driver chiama la routine è specifico del driver. Ad esempio, potrebbe modificare l'istruzione SQL per usare la grammatica SQL dell'origine dati e inviare questa istruzione per l'esecuzione, o può chiamare la procedure direttamente tramite un meccanismo di chiamata RPC (Remote Procedure) che viene definito nel protocollo di flusso di dati del sistema DBMS.  
  
    -   Restituisce i valori dei parametri di output o input/output o il valore restituito di routine, presupponendo che la procedura ha esito positivo. Questi valori potrebbero non essere disponibili solo dopo l'elaborazione di tutti gli altri risultati (conteggio delle righe e set di risultati) generati dalla procedura. Se la procedura ha esito negativo, il driver restituisce eventuali errori.
