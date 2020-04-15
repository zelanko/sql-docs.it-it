---
title: COMANDO SET REPROCESS Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300831"
---
# <a name="set-reprocess-command"></a>SET REPROCESS (comando)
Specifica quante volte o per quanto tempo bloccare un file o un record dopo un tentativo di blocco non riuscito.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argomenti  
 TO *nTentativ*[SECONDI]  
 Specifica il numero di volte o il numero di secondi per tentare di bloccare un record o un file dopo un tentativo iniziale non riuscito. Il valore predefinito è 0; il valore massimo è 32.000.  
  
 SECONDS specifica che Visual FoxPro tenta di bloccare un file o un record per *nTentativ* secondi. È disponibile solo quando *nAttempts* è maggiore di zero.  
  
 Ad esempio, se *nAttempts* è 30, Visual FoxPro tenta di bloccare un record o un file fino a 30 volte. Se si include anche SECONDS (SET REPROCESS To 30 SECONDS), Visual FoxPro tenta continuamente di bloccare un record o un file per un massimo di 30 secondi.  
  
 Se è attiva una routine ON ERROR e se i tentativi da parte di un comando di bloccare il record o il file hanno esito negativo, viene eseguita la routine ON ERROR. Tuttavia, se una funzione tenta il blocco, non viene eseguita una routine ON ERROR e la funzione restituisce False (. F.).  
  
 Se una routine ON ERROR non è attiva, un comando tenta di bloccare il record o il file e il blocco non può essere inserito, viene generato un errore. Se una funzione tenta di inserire il blocco, l'avviso non viene visualizzato e la funzione restituisce False (. F.).  
  
 Se *nAttempts* è 0 (valore predefinito) e si esegue un comando o una funzione che tenta di bloccare un record o un file, Visual FoxPro tenta di bloccare il record o il file per un tempo indefinito. Se il record o il file diventa disponibile per il blocco durante l'attesa, il blocco viene inserito e il messaggio di sistema viene cancellato. Se una funzione ha tentato di posizionare il blocco, la funzione restituisce True (. T.).  
  
 Se è attiva una routine ON ERROR e un comando sta tentando di bloccare il record o il file, la routine ON ERROR ha la precedenza su ulteriori tentativi di bloccare il record o il file. La routine ON ERROR viene eseguita immediatamente. Visual FoxPro non tenta ulteriori blocchi di record o file e non visualizza il messaggio di sistema.  
  
 Se *nAttempts* è 1, Visual FoxPro tenta di bloccare il record o il file per un tempo indefinito e non viene eseguita una routine ON ERROR.  
  
 Se un blocco è stato inserito da un altro utente nel record o nel file che si sta tentando di bloccare, è necessario attendere che l'utente rilasci il blocco.  
  
 A AUTOMATICO  
 Specifica che Visual FoxPro tenta di bloccare il record o il file per un tempo indefinito. (SET REPROCESS TO -2 è un comando equivalente.)  
  
## <a name="remarks"></a>Osservazioni  
 Il primo tentativo di bloccare un record o un file non sempre ha esito positivo. Spesso, un record o un file è bloccato da un altro utente della rete. SET REPROCESS determina se Visual FoxPro effettua ulteriori tentativi di bloccare il record o il file quando il tentativo iniziale non riesce. È possibile specificare quante volte vengono effettuati ulteriori tentativi o per quanto tempo vengono effettuati i tentativi. Una routine ON ERROR influisce sulla modalità di gestione dei tentativi di blocco non riusciti.
