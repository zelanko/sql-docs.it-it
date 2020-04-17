---
title: Connessioni regolari rispetto a connessioni di contesto Documenti Microsoft
description: In SQL ServerSQL Server è talvolta necessario usare connessioni regolari per le istruzioni Transact-SQLTransact-SQL , ma le connessioni di contesto offrono vantaggi in termini di prestazioni e utilizzo delle risorse.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: 881b7463400665d22baaa9b19f13cb5949df0830
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485232"
---
# <a name="context-connections-vs-regular-connections"></a>Connessioni di contesto e connessioni regolariContext Connections vs.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se si esegue una connessione a un server remoto, utilizzare sempre connessioni normali anziché connessioni di contesto. Se è necessario connettersi allo stesso server in cui è in esecuzione la stored procedure o la funzione, utilizzare la connessione di contesto nella maggior parte dei casi. Questa connessione offre vantaggi quali l'esecuzione nello stesso spazio della transazione e la non necessità di eseguire una nuova autenticazione.  
  
 L'utilizzo della connessione di contesto, inoltre, consente in genere prestazioni migliori e un minore utilizzo delle risorse. La connessione di contesto è una connessione solo in-process, pertanto può contattare il server "direttamente" ignorando il protocollo di rete e i livelli di trasporto per inviare istruzioni Transact-SQLTransact-SQL e ricevere risultati. Viene ignorato anche il processo di autenticazione. Nella figura seguente vengono illustrati i componenti principali del provider gestito **SqlClient,** nonché il modo in cui i diversi componenti interagiscono tra loro quando si utilizza una connessione normale e quando si utilizza la connessione di contesto.  
  
 ![Percorsi del codice di una connessione del contesto e una connessione regolare](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Percorsi del codice di una connessione del contesto e una connessione regolare")  
  
 Poiché la connessione di contesto segue un percorso di codice più corto e interessa un numero minore di componenti, è probabile che le richieste e i risultati vengano trasmessi al e dal server più rapidamente che in una connessione normale. I tempi di esecuzione delle query nel server sono uguali per le connessioni normali e di contesto.  
  
 In alcuni casi, potrebbe essere necessario aprire una connessione normale separata allo stesso server. Ad esempio, esistono alcune restrizioni sull'utilizzo della connessione di contesto , descritte in Restrizioni sulle connessioni [regolari e di contesto](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione di contesto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
