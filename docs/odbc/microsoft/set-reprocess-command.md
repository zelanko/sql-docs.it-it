---
title: SET REPROCESS (comando) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16f87c52b4149d62a8d57884216890b7421e8ef6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063618"
---
# <a name="set-reprocess-command"></a>SET REPROCESS (comando)
Specifica quante volte o per informazioni su come long per bloccare un file o un record dopo un tentativo di blocco non riuscito.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argomenti  
 PER *nAttempts*[secondi]  
 Specifica il numero di volte o numero di secondi per tentare di bloccare un record o un file dopo il tentativo iniziale non riuscita. Il valore predefinito è 0. il valore massimo è 32.000.  
  
 SECONDI specifica che Visual FoxPro tenta di bloccare un file o per registrare *nAttempts* secondi. È disponibile solo quando *nAttempts* è maggiore di zero.  
  
 Ad esempio, se *nAttempts* è 30, Visual FoxPro tenta di bloccare un record o il file fino a 30 volte. Se si includono anche (impostare RIELABORARE a 30 secondi), Visual FoxPro continuamente tenta di bloccare un record o un file fino a 30 secondi.  
  
 Se una routine ON ERROR è attivo e se i tentativi da parte di un comando per bloccare il record o il file non hanno esito positivo, viene eseguita la routine ON ERROR. Tuttavia, se una funzione di prova del blocco, non viene eseguita una routine ON ERROR e la funzione restituisce False (. F.).  
  
 Se una routine ON ERROR non è in effetti, un comando tenta di bloccare il record o il file e non è possibile attivare il blocco, viene generato un errore. Se una funzione tenta di inserire il blocco, non viene visualizzato l'avviso e la funzione restituisce False (. F.).  
  
 Se *nAttempts* è 0 (valore predefinito) e si esegue un comando o una funzione che tenta di bloccare un record o un file, Visual FoxPro tenta di bloccare il record o del file per un periodo illimitato. Se il record o il file diventa disponibile per il blocco durante l'attesa, viene inserito il blocco e il messaggio di sistema viene cancellato. Se una funzione ha tentato di inserire il blocco, la funzione restituisce True (. T.).  
  
 Se una routine ON ERROR è attiva e un comando tenta di bloccare il record o un file, la routine ON ERROR ha la precedenza su ulteriori tentativi di bloccare il record o un file. La routine ON ERROR viene eseguita immediatamente. Visual FoxPro non Cerca altro record o i blocchi di file e non visualizza il messaggio di sistema.  
  
 Se *nAttempts* è 1, Visual FoxPro tenta di bloccare il record o per un periodo illimitato di file e non viene eseguita una routine ON ERROR.  
  
 Se un blocco è stato inserito da un altro utente per il file che si sta tentando di bloccare o record, è necessario attendere fino a quando l'utente rilascia il blocco.  
  
 SU AUTOMATICO  
 Specifica che Visual FoxPro tenta di bloccare il record o del file per un periodo illimitato. (SET REPROCESS su -2 è un comando equivalente).  
  
## <a name="remarks"></a>Note  
 Il primo tentativo di bloccare un record o un file non è sempre esito positivo. Spesso, un record o un file è bloccato da un altro utente nella rete. SET REPROCESS determina se Visual FoxPro esegue ulteriori tentativi di bloccare il record o il file durante il tentativo iniziale ha esito negativo. È possibile specificare quante volte ulteriori tentativi vengano eseguiti o per quanto tempo i tentativi vengono stabiliti. Una routine ON ERROR influisce sul blocco non riuscito come vengono gestiti i tentativi.
