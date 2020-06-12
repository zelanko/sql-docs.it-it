---
title: Annullamento di comandi (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 003c70362c38ae1838b4679abf6485fa031a9143
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545063"
---
# <a name="canceling-commands-xmla"></a>Annullamento di comandi (XMLA)
  A seconda delle autorizzazioni amministrative dell'utente che ha emesso il comando, il comando [Annulla](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) in XML for Analysis (XMLA) può annullare un comando in una sessione, una sessione, una connessione, un processo server o una sessione o una connessione associata.  
  
## <a name="canceling-commands"></a>Annullamento di comandi  
 Un utente può annullare il comando attualmente in esecuzione nel contesto della sessione corrente esplicita inviando un comando `Cancel` senza proprietà specificate.  
  
> [!NOTE]  
>  Un comando in esecuzione in una sessione implicita non può essere annullato da un utente.  
  
### <a name="canceling-batch-commands"></a>Annullamento di comandi batch  
 Se un utente annulla un comando `Batch`, tutti i comandi rimanenti non ancora eseguiti nel comando `Batch` vengono annullati. Se il comando `Batch` è transazionale, di tutti i comandi eseguiti prima del comando `Cancel` viene eseguito il rollback.  
  
## <a name="canceling-sessions"></a>Annullamento di sessioni  
 Specificando un identificatore di sessione per una sessione esplicita nella proprietà [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) del `Cancel` comando, un amministratore del database o un amministratore del server può annullare una sessione, incluso il comando attualmente in esecuzione. Un amministratore di database può annullare solo sessioni per i database per i quali dispone delle autorizzazioni amministrative.  
  
 Un amministratore di database può recuperare le sessioni attive per un database specifico recuperando il set di righe dello schema DISCOVER_SESSIONS. Per recuperare il set di righe dello schema DISCOVER_SESSIONS, l'amministratore del database utilizza il `Discover` metodo XMLA e specifica l'identificatore di database appropriato per la colonna di restrizione SESSION_CURRENT_DATABASE nella proprietà [restrictions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) del `Discover` metodo.  
  
## <a name="canceling-connections"></a>Annullamento di connessioni  
 Specificando un identificatore di connessione nella proprietà [ConnectionId](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) del `Cancel` comando, un amministratore del server può annullare tutte le sessioni associate a una determinata connessione, inclusi tutti i comandi in esecuzione, e annullare la connessione.  
  
> [!NOTE]  
>  Se l'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non è in grado di individuare e annullare le sessioni associate a una connessione, ad esempio quando il data pump apre più sessioni fornendo una connettività HTTP, l'istanza non può annullare la connessione. Se questa situazione si verifica durante l'esecuzione di un comando `Cancel`, si verifica un errore.  
  
 Un amministratore del server può recuperare le connessioni attive per un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recuperando il set di righe dello schema DISCOVER_CONNECTIONS tramite il metodo `Discover` XMLA.  
  
## <a name="canceling-server-processes"></a>Annullamento di processi del server  
 Specificando un identificatore di processo del server (SPID) nella proprietà [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) del `Cancel` comando, un amministratore del server può annullare i comandi associati a un determinato SPID.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Annullamento di sessioni e connessioni associate  
 È possibile impostare la proprietà [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) su true per annullare le connessioni, le sessioni e i comandi associati alla connessione, alla sessione o allo SPID specificati nel `Cancel` comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Discover &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
