---
title: Restrizioni relative alle connessioni normali e di contesto | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: d8cbdd195f698090602b98cdb6e5bab0a86556ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68216415"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Connessioni di contesto e connessioni normali - Restrizioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento vengono illustrate le restrizioni associate all'esecuzione del [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] codice nel processo tramite il contesto e le connessioni regolari.  
  
## <a name="restrictions-on-context-connections"></a>Restrizioni relative alle connessioni di contesto  
 Quando si sviluppa l'applicazione, tenere presenti le restrizioni seguenti che si applicano alle connessioni di contesto:  
  
-   È possibile tenere aperta una sola connessione di contesto per volta per una determinata connessione. Se vengono eseguite contemporaneamente più istruzioni in connessioni separate, ognuna di esse può avere la propria connessione di contesto. La restrizione non influisce sulle richieste simultanee provenienti da connessioni diverse ma solo su una specifica richiesta in una determinata connessione.  
  
-   Non è supportato il servizio MARS (Multiple Active Result Sets).  
  
-   La classe **SqlBulkCopy** non funziona in una connessione di contesto.  
  
-   Non è supportata l'esecuzione di batch di aggiornamenti.  
  
-   Non è possibile usare **SqlNotificationRequest** con i comandi eseguiti su una connessione di contesto.  
  
-   Non è supportato l'annullamento di comandi che vengono eseguiti su una connessione di contesto. Il metodo **SqlCommand. Cancel** ignora la richiesta in modo invisibile all'utente.  
  
-   Quando si utilizza "context connection=true", non è possibile utilizzare altre parole chiave della stringa di connessione.  
  
-   La proprietà **SqlConnection. DataSource** restituisce null se la stringa di connessione per **SqlConnection** è "context connection = true" anziché il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   L'impostazione della proprietà **SqlCommand. CommandTimeout** non produce alcun effetto quando il comando viene eseguito su una connessione di contesto.  
  
## <a name="restrictions-on-regular-connections"></a>Restrizioni relative alle connessioni normali  
 Quando si sviluppa l'applicazione, tenere presenti le restrizioni seguenti che si applicano alle connessioni normali:  
  
-   Non è supportata l'esecuzione asincrona di comandi su server interni. Se si include "Async = true" nella stringa di connessione di un comando e quindi si esegue il comando, viene generata l'eccezione **System. NotSupportedException** . Viene visualizzato il messaggio "Asynchronous Processing non è supportato se eseguito in un processo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]".  
  
-   L'oggetto **SqlDependency** non è supportato.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione di contesto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
