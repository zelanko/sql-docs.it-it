---
title: Gestione degli aggiornamenti non riusciti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: dbd8346c481fc4fdfddb7aa6260bd5b8422b941a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758294"
---
# <a name="dealing-with-failed-updates"></a>Gestione degli aggiornamenti non riusciti
Quando un aggiornamento termina con errori, la modalità di risoluzione degli errori dipende dalla natura e dalla gravità degli errori e dalla logica dell'applicazione. Tuttavia, se il database è condiviso con altri utenti, un errore tipico è che qualcun altro modifica il campo prima di procedere. Questo tipo di errore è denominato conflitto. ADO rileva questa situazione e segnala un errore.  
  
## <a name="remarks"></a>Commenti  
 Se sono presenti errori di aggiornamento, verranno intercettati in una routine di gestione degli errori. Filtrare il recordset con la costante adFilterConflictingRecords in modo che siano visibili solo le righe in conflitto. In questo esempio, la strategia di risoluzione degli errori è semplicemente stampare il nome e il cognome dell'autore (au_fname e au_lname).  
  
 Il codice per avvisare l'utente del conflitto di aggiornamento è simile al seguente:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
