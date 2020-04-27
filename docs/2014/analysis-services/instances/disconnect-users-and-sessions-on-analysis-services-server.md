---
title: Disconnettere utenti e sessioni nel server Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ending user activity [Analysis Services]
- connections [Analysis Services]
- sessions [Analysis Services]
ms.assetid: 3b0145a2-f21d-4dd0-a09e-83afeb2ff4a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c1a974025e1f23cd5fa0a3b7824431d422bfe35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080065"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Disconnettere utenti e sessioni sul server Analysis Services
  Nell'ambito della gestione del carico di lavoro, un amministratore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può terminare l'attività dell'utente annullando sessioni e connessioni. Le sessioni possono essere create automaticamente durante l'esecuzione di una query (implicite) oppure denominate dall'amministratore al momento della creazione (esplicite). Le connessioni sono circuiti aperti per l'esecuzione delle query. È possibile terminare sia le sessioni che le connessioni mentre sono attive. Ad esempio, un amministratore può terminare l'elaborazione di una sessione se il processo richiede tempi troppo lunghi o non è certo che il comando in esecuzione sia stato registrato correttamente.  
  
## <a name="ending-sessions-and-connections"></a>Terminazione di sessioni e connessioni  
 Per gestire sessioni e connessioni, è possibile utilizzare viste a gestione dinamica (DMV) e XMLA:  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a un'istanza di Analysis Services.  
  
2.  Incollare una delle query DMV seguenti in una finestra Query MDX per ottenere un elenco di tutti i comandi, le sessioni e le connessioni attualmente in esecuzione:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
     `Select * from $System.Discover_Commands`  
  
3.  Premere F5 per eseguire la query.  
  
     La query DMV restituisce informazioni sulla sessione e sulla connessione in un set di risultati tabulare più facile da leggere e copiare.  
  
 Tenere aperta la finestra Query. Nel passaggio successivo sarà necessario tornare a questa pagina per copiare i valori SPID della sessione da disconnettere.  
  
 Per terminare una sessione, aprire una seconda finestra Query XMLA.  
  
1.  Incollare la sintassi seguente in una finestra Query MDX, sostituendo il segnaposto ConnectionID, SessionID o SPID con un valore valido copiato dal passaggio precedente.  
  
    ```  
    <Cancel xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  Premere F5 per eseguire il comando Annulla.  
  
 Se si modifica una connessione, saranno annullate tutte le sessioni e i valori SPID e la sessione host sarà chiusa.  
  
 Se si termina una sessione, saranno arrestati tutti i comandi (SPID) eseguiti nel corso di tale sessione.  
  
 Se si termina un SPID, sarà annullato un comando specifico.  
  
 In rari casi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non chiuderà una connessione se non è possibile rilevare tutte le sessioni e i valori SPID associati alla connessione, ad esempio nel caso in cui più sessioni siano aperte in uno scenario HTTP.  
  
 Per altre informazioni sul codice XMLA a cui si fa riferimento in questo argomento, vedere [Metodo Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) ed [Elemento Cancel &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla).  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione delle connessioni e delle sessioni &#40;&#41;XMLA](../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [Elemento EndSession &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Elemento Session &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
