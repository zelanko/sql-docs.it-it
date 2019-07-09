---
title: Disconnettere utenti e sessioni in Analysis Services Server | Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624376"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Disconnettere utenti e sessioni sul server Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  Come amministratore, si consiglia di attività degli utenti finali come parte della gestione del carico di lavoro. annullando sessioni e connessioni. Le sessioni possono essere create automaticamente durante l'esecuzione di una query (implicite) oppure denominate dall'amministratore al momento della creazione (esplicite). Le connessioni sono circuiti aperti per l'esecuzione delle query. È possibile terminare sia le sessioni che le connessioni mentre sono attive. Ad esempio, è possibile terminare l'elaborazione di una sessione, se l'elaborazione richiede troppo tempo oppure se alcuni non è certo che il comando in esecuzione è stata scritta correttamente.  
  
## <a name="ending-sessions-and-connections"></a>Terminazione di sessioni e connessioni  
 Per gestire sessioni e connessioni, utilizzare viste a gestione dinamica (DMV) e XMLA:  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di Analysis Services.  
  
2.  Incollare una delle query DMV seguenti in una finestra Query MDX per ottenere un elenco di tutti i comandi, le sessioni e le connessioni attualmente in esecuzione:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  (Questa query non si applica ad Azure Analysis Services)
  
     `Select * from $System.Discover_Commands`  
  
3.  Premere F5 per eseguire la query.  
  
     La query DMV restituisce informazioni sulla sessione e sulla connessione in un set di risultati tabulare più facile da leggere e copiare.  
  
 Tenere aperta la finestra Query. Nel passaggio successivo sarà necessario tornare a questa pagina per copiare i valori SPID della sessione da disconnettere.  
  
 Per terminare una sessione, aprire una seconda finestra Query XMLA.  
  
1.  Incollare la sintassi seguente in una finestra Query MDX, sostituendo il segnaposto ConnectionID, SessionID o SPID con un valore valido copiato dal passaggio precedente.  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  Premere F5 per eseguire il comando Annulla.  

SessionID o SPID l'annullamento annullerà i comandi attivi in esecuzione nella sessione corrispondente all'ID di sessione/SPID. Annullamento di una connessione verrà identificare di sessione associata alla connessione e Annulla eventuali comandi attivi in esecuzione su tale sessione. In rari casi, una connessione non viene chiusa se il motore non è possibile tenere traccia di tutte le sessioni e i valori SPID associati alla connessione; ad esempio, quando più sessioni siano aperte in uno scenario HTTP.   
  
Per altre informazioni sul codice XMLA a cui fa riferimento in questo argomento, vedere [metodo Execute &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) e [Annulla elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di connessioni e sessioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [Elemento EndSession &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Elemento Session &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
