---
title: Esecuzione di routine | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305712"
---
# <a name="executing-procedures"></a>Esecuzione di procedure
ODBC definisce una sequenza di escape standard per l'esecuzione di routine. Per la sintassi di questa sequenza e un esempio di codice che lo usa, vedere [procedure calls](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Per eseguire una procedura, un'applicazione esegue le azioni seguenti:  
  
1.  Imposta i valori di tutti i parametri. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
2.  Chiama **SQLExecDirect** e la passa a una stringa contenente l'istruzione SQL che esegue la procedura. Questa istruzione può utilizzare la sequenza di escape definita da ODBC o dalla sintassi specifica di DBMS. le istruzioni che utilizzano la sintassi specifica di DBMS non sono interoperative.  
  
3.  Quando viene chiamato **SQLExecDirect** , il driver:  
  
    -   Recupera i valori di parametro correnti e li converte secondo necessità. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   Chiama la stored procedure nell'origine dati e li invia ai valori dei parametri convertiti. Il modo in cui il driver chiama la procedura è specifico del driver. È possibile, ad esempio, modificare l'istruzione SQL in modo che utilizzi la grammatica SQL dell'origine dati e inviare questa istruzione per l'esecuzione. in alternativa, è possibile che venga chiamata direttamente la procedura utilizzando un meccanismo RPC (Remote Procedure Call) definito nel protocollo del flusso di dati del sistema DBMS.  
  
    -   Restituisce i valori di qualsiasi parametro di input/output o di output o il valore restituito della procedura, supponendo che la procedura abbia esito positivo. Questi valori potrebbero non essere disponibili finché non vengono elaborati tutti gli altri risultati (conteggi di righe e set di risultati) generati dalla procedura. Se la procedura non riesce, il driver restituisce eventuali errori.
