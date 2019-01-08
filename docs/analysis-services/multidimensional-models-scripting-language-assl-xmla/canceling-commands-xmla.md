---
title: Annullamento di comandi (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 313708ad1575c7b9922ac796791d0d623c51b54b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207520"
---
# <a name="canceling-commands-xmla"></a>Annullamento di comandi (XMLA)
  A seconda delle autorizzazioni amministrative dell'utente che invia il comando, il [annullare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) comando nel codice XML per Analysis (XMLA) può annullare un comando in una sessione, una sessione, una connessione, un processo del server o una sessione associata o connessione.  
  
## <a name="canceling-commands"></a>Annullamento di comandi  
 Un utente può annullare il comando attualmente in esecuzione all'interno del contesto della sessione corrente esplicita inviando un **annullare** comando senza proprietà specificate.  
  
> [!NOTE]  
>  Un comando in esecuzione in una sessione implicita non può essere annullato da un utente.  
  
### <a name="canceling-batch-commands"></a>Annullamento di comandi batch  
 Se un utente annulla una **Batch** comando, quindi tutti gli altri comandi non ancora eseguiti all'interno di **Batch** comando vengono annullate. Se il **Batch** comando è transazionale, tutti i comandi eseguiti prima le **Annulla** comando viene eseguito il rollback.  
  
## <a name="canceling-sessions"></a>Annullamento di sessioni  
 Specificando un identificatore di sessione per una sessione esplicita nella [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) proprietà delle **Annulla** comando, un amministratore di database o un amministratore del server può annullare una sessione, tra cui il comando attualmente in esecuzione. Un amministratore di database può annullare solo sessioni per i database per i quali dispone delle autorizzazioni amministrative.  
  
 Un amministratore di database può recuperare le sessioni attive per un database specifico recuperando il set di righe dello schema DISCOVER_SESSIONS. Per recuperare il set di righe dello schema DISCOVER_SESSIONS, l'amministratore del database utilizza XMLA **Discover** (metodo) e specifica l'identificatore del database appropriato per la colonna di restrizione SESSION_CURRENT_DATABASE nella [Restrizioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) proprietà del **Discover** (metodo).  
  
## <a name="canceling-connections"></a>Annullamento di connessioni  
 Specificando un identificatore di connessione nel [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) proprietà delle **Annulla** comando, un amministratore del server può annullare tutte le sessioni associate a una determinata connessione, inclusi tutti i esecuzione di comandi e annullare la connessione.  
  
> [!NOTE]
>  Se l'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non è possibile individuare e annullare le sessioni associate a una connessione, ad esempio quando il data pump apre più sessioni fornendo contemporaneamente connettività HTTP, l'istanza non è possibile annullare la connessione. Se questa situazione si verifica durante l'esecuzione di un **annullare** comando, si verifica un errore.  
  
 Un amministratore del server possa recuperare le connessioni attive per un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza mediante il recupero di righe dello schema DISCOVER_CONNECTIONS tramite XMLA **Discover** (metodo).  
  
## <a name="canceling-server-processes"></a>Annullamento di processi del server  
 Specificando un identificatore di processo server (SPID) nei [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) proprietà delle **Annulla** comando, un amministratore del server può annullare i comandi associati a un valore SPID specificato.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Annullamento di sessioni e connessioni associate  
 È possibile impostare il [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) su true per annullare le connessioni, sessioni e comandi associati con la connessione, sessione o valore SPID specificato nel **Annulla** comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
