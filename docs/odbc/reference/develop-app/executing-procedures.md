---
title: Procedure di esecuzione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305712"
---
# <a name="executing-procedures"></a>Esecuzione di procedure
ODBC definisce una sequenza di escape standard per l'esecuzione di procedure. Per la sintassi di questa sequenza e un esempio di codice che la utilizza, vedere Chiamate di [routine](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Per eseguire una routine, un'applicazione esegue le azioni seguenti:To execute a procedure, an application performs the following actions:  
  
1.  Imposta i valori di tutti i parametri. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
2.  Chiama **SQLExecDirect** e passa una stringa contenente l'istruzione SQL che esegue la procedura. Questa istruzione può utilizzare la sequenza di escape definita da ODBC o dalla sintassi specifica di DBMS. le istruzioni che utilizzano la sintassi specifica di DBMS non sono interoperabili.  
  
3.  Quando **SQLExecDirect** viene chiamato, il driver:  
  
    -   Recupera i valori dei parametri correnti e li converte in base alle esigenze. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
    -   Chiama la routine nell'origine dati e le invia i valori dei parametri convertiti. Il modo in cui il driver chiama la procedura è specifico del driver. Ad esempio, potrebbe modificare l'istruzione SQL per utilizzare la grammatica SQL dell'origine dati e inviare questa istruzione per l'esecuzione oppure potrebbe chiamare la procedura direttamente utilizzando un meccanismo RPC (Remote Procedure Call) definito nel protocollo del flusso di dati del DBMS.  
  
    -   Restituisce i valori di qualsiasi parametro di input/output o output o il valore restituito della routine, presupponendo che la routine abbia esito positivo. Questi valori potrebbero non essere disponibili fino a quando non sono stati elaborati tutti gli altri risultati (conteggi delle righe e set di risultati) generati dalla procedura. Se la procedura non riesce, il driver restituisce eventuali errori.
