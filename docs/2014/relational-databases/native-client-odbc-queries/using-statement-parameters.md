---
title: Utilizzo dei parametri dell'istruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
author: rothja
ms.author: jroth
ms.openlocfilehash: 8657c439d35a539892e7f166d8a0a443a5fb759b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049733"
---
# <a name="using-statement-parameters"></a>Utilizzo dei parametri delle istruzioni
  Un parametro è una variabile in un'istruzione SQL che consente a un'applicazione ODBC di:  
  
-   Fornire in modo efficiente valori per le colonne di una tabella.  
  
-   Migliorare l'interazione dell'utente nella costruzione di criteri di query.  
  
-   Gestire i dati di tipo **Text**, **ntext**e **Image** e i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati C specifici di.  
  
 Una tabella **parts** , ad esempio, include colonne denominate **partID**, **Description**e **Price**. Per aggiungere una parte senza parametri, è necessario costruire un'istruzione SQL come:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Sebbene questa istruzione sia accettabile per l'inserimento di una riga con un set di valori noto, non risulta particolarmente efficace quando un'applicazione richiede l'inserimento di diverse righe. In ODBC il problema viene risolto consentendo a un'applicazione di sostituire qualsiasi valore dei dati in un'istruzione SQL con un marcatore di parametro, rappresentato da un punto interrogativo (?). Nell'esempio seguente tre valori di dati vengono sostituiti con marcatori di parametro:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Gli indicatori di parametro vengono quindi associati a variabili dell'applicazione. Per inserire una nuova riga, l'applicazione deve solo impostare i valori delle variabili ed eseguire l'istruzione. Il driver recupera quindi i valori correnti delle variabili e li invia all'origine dati. Se l'istruzione viene eseguita più volte, l'applicazione può rendere ancora più efficiente il processo preparando l'istruzione.  
  
 A ogni marcatore di parametro è associato il numero ordinale assegnato ai parametri, da sinistra verso destra. Il marcatore di parametro all'estrema sinistra in un'istruzione SQL presenta un valore ordinale pari a 1, il successivo è l'ordinale 2 e così via.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Associazione di parametri](using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
