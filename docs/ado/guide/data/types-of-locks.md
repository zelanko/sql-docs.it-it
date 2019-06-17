---
title: Tipi di blocchi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 64ac7dae1a5760ff18f1a109a031bd00bb30eb1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718652"
---
# <a name="types-of-locks"></a>Tipi di blocchi
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica gli aggiornamenti in blocco ottimistico. Obbligatorio per la modalità di aggiornamento batch.  
  
 Molte applicazioni di recuperano un numero di righe in una sola volta e quindi necessario eseguire gli aggiornamenti coordinati che includono l'intero set di righe inserite, aggiornate o eliminate. Con i cursori di batch, un solo round trip al server è necessario, migliorando così le prestazioni dell'aggiornamento e ridurre il traffico di rete. Usa una libreria di cursori di batch, è possibile creare un cursore statico e quindi disconnettersi dall'origine dati. A questo punto è possibile apportare modifiche alle righe e successivamente riconnettersi e inviare le modifiche all'origine dati in un batch.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica che il provider Usa ottimistica blocco: blocco dei record solo quando si chiama il **Update** (metodo). Ciò significa che è probabile che un altro utente può modificare i dati tra il momento si modifica il record e quando si chiama **Update**, che consente di creare conflitti. Usare questo tipo di blocco nelle situazioni in cui le probabilità di collisione sono insufficiente o conflitti in cui possono essere risolti immediatamente.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica il blocco pessimistico, un record. Il provider non sia necessaria per garantire la corretta modifica dei record, in genere dal blocco dei record nell'origine dati prima della modifica. Naturalmente, ciò significa che i record non sono disponibili ad altri utenti dopo aver iniziato la modifica, fino a quando non si rilascia il blocco chiamando **Update.** Usare questo tipo di blocco in un sistema in cui è possibile disporre le modifiche simultanee ai dati, ad esempio in un sistema di prenotazione.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica i record di sola lettura. Non è possibile modificare i dati. Un blocco di sola lettura è il tipo di blocco "veloce" perché non richiede il server per mantenere un blocco per i record.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 Non specifica un tipo di blocco.
