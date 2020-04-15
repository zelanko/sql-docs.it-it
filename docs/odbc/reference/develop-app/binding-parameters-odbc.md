---
title: Parametri di associazione ODBC Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306382"
---
# <a name="binding-parameters-odbc"></a>Associazione di parametri ODBC
Ogni parametro in un'istruzione SQL deve essere associato, o *associato,* a una variabile nell'applicazione prima dell'esecuzione dell'istruzione. Quando l'applicazione associa una variabile a un parametro, descrive tale variabile - indirizzo, tipo di dati C e così via - al driver. Vengono inoltre descritti il parametro stesso: tipo di dati SQL, precisione e così via. Il driver archivia queste informazioni nella struttura che gestisce per l'istruzione e utilizza le informazioni per recuperare il valore dalla variabile quando viene eseguita l'istruzione.  
  
 I parametri possono essere associati o riassociati in qualsiasi momento prima dell'esecuzione di un'istruzione. Se un parametro viene riassociato dopo l'esecuzione di un'istruzione, l'associazione non viene applicata fino a quando l'istruzione non viene eseguita nuovamente. Per associare un parametro a una variabile diversa, un'applicazione semplicemente riassocia il parametro con la nuova variabile; l'associazione precedente viene rilasciata automaticamente.  
  
 Una variabile rimane associata a un parametro fino a quando non viene associata una variabile diversa al parametro, fino a quando tutti i parametri non sono associati chiamando **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS o fino a quando non viene rilasciata l'istruzione. Per questo motivo, l'applicazione deve assicurarsi che le variabili non vengano liberate fino a quando non sono associate. Per ulteriori informazioni, consultate [Allocazione e liberazione dei buffer.](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
 Poiché le associazioni di parametri sono solo informazioni archiviate nella struttura gestita dal driver per l'istruzione, possono essere impostate in qualsiasi ordine. Sono inoltre indipendenti dall'istruzione SQL eseguita. Si supponga, ad esempio, che un'applicazione associa tre parametri e quindi esegue l'istruzione SQL seguente:For example, suppose an application binds three parameters and then executes the following SQL statement:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se l'applicazione esegue immediatamente l'istruzione SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 sullo stesso handle di istruzione, vengono utilizzate le associazioni di parametri per l'istruzione **INSERT** perché si tratta delle associazioni archiviate nella struttura dell'istruzione. Nella maggior parte dei casi, questa è una pratica di programmazione scadente e dovrebbe essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS per annullare l'associazione di tutti i parametri precedenti e quindi associare quelli nuovi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di marcatori di parametro](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Offset di associazione di parametri](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrizione di parametri](../../../odbc/reference/develop-app/describing-parameters.md)
