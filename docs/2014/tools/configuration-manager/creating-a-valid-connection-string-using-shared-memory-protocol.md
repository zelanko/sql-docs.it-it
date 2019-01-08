---
title: Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c157d0b8cee3ee3635275c8f1b3c49fc6faf5a0a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802173"
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa
  Le connessioni a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un client in esecuzione nello stesso computer utilizzano il protocollo Shared Memory. La memoria condivisa non dispone di proprietà configurabili. Viene sempre utilizzata al primo tentativo di connessione e non può essere spostata dalla posizione iniziale nell'elenco **Protocolli abilitati** in **Proprietà protocolli client** . È possibile disabilitare il protocollo di memoria condivisa, operazione utile durante la risoluzione dei problemi relativi a uno degli altri protocolli.  
  
 Non è possibile creare un alias utilizzando il protocollo di memoria condivisa, ma, se si abilita la memoria condivisa e quindi ci si connette a [!INCLUDE[ssDE](../../includes/ssde-md.md)] tramite un nome, viene creata una connessione di memoria condivisa. Una stringa di connessione di memoria condivisa utilizza il formato `lpc:<servername>[\instancename]`.  
  
## <a name="connecting-to-the-local-server"></a>Connessione al server locale  
 Quando si stabilisce una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sullo stesso computer del client, è possibile usare **(locale)** come nome del server. Non si tratta di un'operazione consigliabile, in quanto genera ambiguità, ma può risultare utile se si è sicuri che il client viene eseguito nello stesso computer del server. Se, ad esempio, si crea un'applicazione per utenti mobili non connessi, ad esempio il personale di vendita, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito su computer portatili e usato per archiviare dati di progetto, un client che si connette al server **(locale)** si connetterà sempre all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sul portatile. In sostituzione di **(locale)** . è possibile usare la parola**localhost**o un punto ( **.**).  
  
## <a name="verifying-your-connection-protocol"></a>Verifica del protocollo di connessione  
 La query seguente restituisce il protocollo utilizzato per la connessione corrente.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Esempi:  
 I nomi seguenti consentono di connettersi al computer locale con il protocollo di memoria condivisa, se abilitato:  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 Non è possibile creare un alias per una connessione di memoria condivisa.  
  
> [!NOTE]  
>  Se si specifica un indirizzo IP nella casella **Server** , verrà stabilita una connessione TCP/IP.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stringa di connessione valida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Creazione di una stringa di connessione valida tramite named pipe](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
