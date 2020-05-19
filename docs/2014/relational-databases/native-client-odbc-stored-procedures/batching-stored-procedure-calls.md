---
title: Invio in batch di chiamate a stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ce14de191cb8b57496cf2de87d241810e32624ec
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709868"
---
# <a name="batching-stored-procedure-calls"></a>Invio in batch di chiamate a stored procedure
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client esegue automaticamente il batch stored procedure le chiamate al server quando appropriato. Il driver effettua questa operazione solo quando viene utilizzata la sequenza di escape e non per l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE. L'invio in batch di chiamate a stored procedure può ridurre il numero di round trip al server e migliorare significativamente le prestazioni.  
  
 Il driver invia in batch al server le chiamate alle procedure quando si esegue un batch che contiene più sequenze di escape ODBC CALL. Invia inoltre in batch chiamate alle procedure quando si utilizzano matrici di parametri associati con una sequenza di escape ODBC CALL. Se, ad esempio, si utilizza l'associazione di parametri a livello di riga o di colonna per associare una matrice con cinque elementi ai parametri di un'istruzione SQL ODBC CALL, quando viene chiamato **SQLExecute** o **SQLExecDirect** , il driver invia un singolo batch con cinque chiamate di procedura al server.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione delle stored procedure](running-stored-procedures.md)  
  
  
