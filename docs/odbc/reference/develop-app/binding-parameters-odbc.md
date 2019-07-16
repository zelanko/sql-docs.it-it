---
title: Associazione di parametri ODBC | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107632"
---
# <a name="binding-parameters-odbc"></a>Associazione di parametri ODBC
Ogni parametro in un'istruzione SQL deve essere associato, oppure *associata,* a una variabile nell'applicazione prima che venga eseguita l'istruzione. Quando l'applicazione associa una variabile a un parametro, descrive la variabile indirizzo, tipo di dati C e così via - il driver. Descrive anche il parametro - tipo di dati SQL, precisione e così via. Il driver di queste informazioni vengono memorizzate nella struttura mantiene per l'istruzione e utilizza le informazioni per recuperare il valore dalla variabile quando viene eseguita l'istruzione.  
  
 I parametri possono essere associati o riassociati in qualunque momento prima che venga eseguita un'istruzione. Se un parametro è riassociato dopo che viene eseguita un'istruzione, fino a quando non viene eseguita nuovamente l'istruzione non si applica l'associazione. Per associare un parametro a una variabile diversa, un'applicazione riassocia semplicemente il parametro con la nuova variabile; l'associazione precedente viene rilasciata automaticamente.  
  
 Una variabile rimane associata a un parametro fino a quando una variabile diversa è associata al parametro, fino a quando tutti i parametri sono non associati, chiamare **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS o finché non viene rilasciato l'istruzione. Per questo motivo, l'applicazione deve essere certi che le variabili non vengono liberate fino a dopo che sono non associati. Per altre informazioni, vedere [allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Poiché le associazioni di parametro sono solo le informazioni archiviate nella struttura gestita dal driver per l'istruzione, possono essere impostate in qualsiasi ordine. Sono anche indipendenti dell'istruzione SQL eseguita. Si supponga, ad esempio, un'applicazione associa tre parametri, quindi esegue l'istruzione SQL seguente:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Se quindi l'applicazione esegue immediatamente l'istruzione SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 sullo stesso handle di istruzione, le associazioni di parametro per il **Inserisci** istruzione vengono utilizzati in quanto queste sono le associazioni archiviate nella struttura di istruzione. Nella maggior parte dei casi, questa è una pratica di programmazione scarsa e deve essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_RESET_PARAMS a disassocia tutti i parametri precedenti e quindi associare nuovi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di marcatori di parametro](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Offset di associazione di parametri](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descrizione di parametri](../../../odbc/reference/develop-app/describing-parameters.md)
