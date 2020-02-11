---
title: Parametri di binding ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bc40d4800e7cd013b7ac908400c0492286314e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107632"
---
# <a name="binding-parameters-odbc"></a>Associazione di parametri ODBC
Ogni parametro in un'istruzione SQL deve essere *associato o associato* a una variabile nell'applicazione prima che venga eseguita l'istruzione. Quando l'applicazione associa una variabile a un parametro, descrive il tipo di dati di indirizzo variabile, C e così via al driver. Descrive anche il parametro stesso: tipo di dati SQL, precisione e così via. Il driver archivia queste informazioni nella struttura che gestisce per tale istruzione e utilizza le informazioni per recuperare il valore dalla variabile quando viene eseguita l'istruzione.  
  
 I parametri possono essere associati o riassociati in qualsiasi momento prima dell'esecuzione di un'istruzione. Se un parametro viene riassociato dopo l'esecuzione di un'istruzione, l'associazione non viene applicata fino a quando l'istruzione non viene eseguita di nuovo. Per associare un parametro a una variabile diversa, un'applicazione riassocia semplicemente il parametro alla nuova variabile. l'associazione precedente viene rilasciata automaticamente.  
  
 Una variabile rimane associata a un parametro fino a quando non viene associata una variabile diversa al parametro, fino a quando tutti i parametri non sono associati chiamando **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS o fino a quando l'istruzione non viene rilasciata. Per questo motivo, l'applicazione deve assicurarsi che le variabili non vengano liberate fino a quando non sono associate. Per altre informazioni, vedere [allocazione e liberazione dei buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Poiché le associazioni di parametro sono solo le informazioni archiviate nella struttura gestita dal driver per l'istruzione, possono essere impostate in qualsiasi ordine. Sono inoltre indipendenti dall'istruzione SQL eseguita. Si supponga, ad esempio, che un'applicazione associ tre parametri e quindi esegua l'istruzione SQL seguente:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se l'applicazione esegue immediatamente l'istruzione SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 nello stesso handle di istruzione vengono usate le associazioni di parametro per l'istruzione **Insert** , perché si tratta delle associazioni archiviate nella struttura dell'istruzione. Nella maggior parte dei casi, si tratta di una procedura di programmazione insufficiente e deve essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS per annullare l'associazione di tutti i parametri obsoleti e quindi associare quelli nuovi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di marcatori di parametro](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Offset di associazione di parametri](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrizione di parametri](../../../odbc/reference/develop-app/describing-parameters.md)
