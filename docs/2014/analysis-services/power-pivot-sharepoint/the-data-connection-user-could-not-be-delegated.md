---
title: "Per la connessione dati viene utilizzata l'autenticazione di Windows e le credenziali utente non possono essere delegate. Impossibile aggiornare le connessioni seguenti: dati PowerPivot | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b11e1510213aefa98c6bf2c0c779cebaeed85e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071026"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>Per la connessione dati viene utilizzata l'autenticazione di Windows e le credenziali utente non possono essere delegate. Impossibile aggiornare le connessioni seguenti: Dati PowerPivot
  Per cartelle di lavoro di Excel contenenti dati PowerPivot, in Excel Services viene restituito questo errore se non è possibile connettersi a un'istanza del server PowerPivot in SharePoint.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Si applica a|PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Errore di connessione nel tentativo di utilizzare un provider di dati PowerPivot.|  
|Testo del messaggio|Per la connessione dati viene utilizzata l'autenticazione di Windows e le credenziali utente non possono essere delegate. Impossibile aggiornare le connessioni seguenti: Dati PowerPivot|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio di errore può avere più cause. Il fattore comune a tutte è che tramite Excel Services non è possibile ottenere un'identità utente di Windows valida da un token di attestazione in SharePoint. Nel caso di cartelle di lavoro di Excel contenenti dati PowerPivot, questo errore si verifica quando sussiste una delle condizioni seguenti:  
  
-   Claims nel Servizio token Windows non è in esecuzione. È possibile confermare la causa di questo errore visualizzando il file registro di SharePoint. Se nei registri di SharePoint è incluso il messaggio "Impossibile trovare l'endpoint di pipe di 'net.pipe://localhost/s 4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' nel computer locale", Claims nel Servizio token Windows non è in esecuzione. Per avviarlo, utilizzare Amministrazione centrale, quindi verificare che il servizio sia in esecuzione nell'applicazione console Servizi.  
  
-   Un controller di dominio non è disponibile per la convalida dell'identità utente. Claims nel Servizio token Windows non utilizza le credenziali memorizzate nella cache. Convalida l'identità utente per ogni connessione. È possibile confermare la causa di questo errore visualizzando il file registro di SharePoint. Se nei registri di SharePoint è incluso il messaggio "Impossibile recuperare WindowsIdentity da IClaimsIdentity", l'identità utente non può essere autenticata.  
  
-   I computer devono essere membri dello stesso dominio o trovarsi in domini in cui è disponibile una relazione di trust bidirezionale.  
  
-   È necessario utilizzare account utente di dominio Windows. Gli account devono disporre di un UPN (Universal Principal Name).  
  
-   L'account servizio di Excel Services deve disporre delle autorizzazioni di Active Directory per eseguire una query sull'oggetto.  
  
## <a name="user-action"></a>Azione dell'utente  
 Utilizzare le istruzioni seguenti per controllare lo stato di Claims nel Servizio token Windows.  
  
 Per tutti gli altri scenari, controllare con l'amministratore di rete.  
  
#### <a name="enable-claims-to-windows-token-service"></a>Abilitare Claims nel Servizio token Windows  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  Selezionare **Attestazioni per il servizio token Windows**e quindi fare clic su **Avvia**.  
  
3.  Nella console Servizi verificare che anche il servizio sia in esecuzione:  
  
    1.  In Strumenti di amministrazione fare clic su Servizi.  
  
    2.  Avviare Claims nel Servizio token Windows nel caso non sia in esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio PowerPivot](configure-power-pivot-service-accounts.md)  
  
  
