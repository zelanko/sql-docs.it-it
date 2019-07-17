---
title: Usando i parametri delle istruzioni | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1168c81d8eeb6a25b84f473858bc924f529a572
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058667"
---
# <a name="using-statement-parameters"></a>Utilizzo dei parametri delle istruzioni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Un parametro è una variabile in un'istruzione SQL che consente a un'applicazione ODBC di:  
  
-   Fornire in modo efficiente valori per le colonne di una tabella.  
  
-   Migliorare l'interazione dell'utente nella costruzione di criteri di query.  
  
-   Gestire **testo**, **ntext**, e **immagine** dei dati e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-tipi di dati C specifici.  
  
 Ad esempio, un **parti** tabella include colonne denominate **PartID**, **descrizione**, e **prezzo**. Per aggiungere una parte senza parametri, è necessario costruire un'istruzione SQL come:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Sebbene questa istruzione sia accettabile per l'inserimento di una riga con un set di valori noto, non risulta particolarmente efficace quando un'applicazione richiede l'inserimento di diverse righe. In ODBC il problema viene risolto consentendo a un'applicazione di sostituire qualsiasi valore dei dati in un'istruzione SQL con un marcatore di parametro, rappresentato da un punto interrogativo (?). Nell'esempio seguente tre valori di dati vengono sostituiti con marcatori di parametro:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Gli indicatori di parametro vengono quindi associati a variabili dell'applicazione. Per inserire una nuova riga, l'applicazione deve solo impostare i valori delle variabili ed eseguire l'istruzione. Il driver recupera quindi i valori correnti delle variabili e li invia all'origine dati. Se l'istruzione viene eseguita più volte, l'applicazione può rendere ancora più efficiente il processo preparando l'istruzione.  
  
 A ogni marcatore di parametro è associato il numero ordinale assegnato ai parametri, da sinistra verso destra. Il marcatore di parametro all'estrema sinistra in un'istruzione SQL presenta un valore ordinale pari a 1, il successivo è l'ordinale 2 e così via.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Associazione di parametri](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Vedere anche  
 [L'esecuzione di query &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
