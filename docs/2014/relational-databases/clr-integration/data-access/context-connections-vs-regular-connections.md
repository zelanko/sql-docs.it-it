---
title: Connessione normale e Connessioni di contesto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f4255e17f7cd76cf402c10d84b015a1324d7d6f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874038"
---
# <a name="regular-vs-context-connections"></a>Connessione normale e Connessione di contesto:
  Se si esegue una connessione a un server remoto, utilizzare sempre connessioni normali anziché connessioni di contesto. Se è necessario connettersi allo stesso server in cui è in esecuzione la stored procedure o la funzione, utilizzare la connessione di contesto nella maggior parte dei casi. Questa connessione offre vantaggi quali l'esecuzione nello stesso spazio della transazione e la non necessità di eseguire una nuova autenticazione.  
  
 L'utilizzo della connessione di contesto, inoltre, consente in genere prestazioni migliori e un minore utilizzo delle risorse. La connessione di contesto è una connessione processo solo in, può contattare il server "direttamente" ignorando i livelli di trasporto e protocollo di rete per inviare istruzioni Transact-SQL e ricevere risultati. Viene ignorato anche il processo di autenticazione. Nella figura seguente vengono illustrati i componenti principali del provider gestito `SqlClient`, nonché l'interazione reciproca dei diversi componenti quando si utilizza una connessione normale e quando si utilizza una connessione di contesto.  
  
 ![Percorsi del codice di un contesto e una connessione normale. ](../../../database-engine/dev-guide/media/clrintdataaccess.gif "i percorsi di un contesto e una connessione normale del codice.")  
  
 Poiché la connessione di contesto segue un percorso di codice più corto e interessa un numero minore di componenti, è probabile che le richieste e i risultati vengano trasmessi al e dal server più rapidamente che in una connessione normale. I tempi di esecuzione delle query nel server sono uguali per le connessioni normali e di contesto.  
  
 In alcuni casi, potrebbe essere necessario aprire una connessione normale separata allo stesso server. Ad esempio, esistono alcune restrizioni nella connessione di contesto, descritto nella [restrizioni sulle normali e connessioni di contesto](context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione di contesto](context-connection.md)  
  
  
