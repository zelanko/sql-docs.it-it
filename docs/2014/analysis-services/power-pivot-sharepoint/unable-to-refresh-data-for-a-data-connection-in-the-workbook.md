---
title: "Impossibile aggiornare i dati per una connessione dati della cartella di lavoro. Riprovare o contattare l'amministratore di sistema. Impossibile aggiornare le connessioni seguenti: I dati PowerPivot | Microsoft Docs"
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e99fc17cb8f369967ff4c26699e67f0ed91d33
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070940"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>Impossibile aggiornare i dati per una connessione dati della cartella di lavoro. Riprovare o contattare l'amministratore di sistema. Impossibile aggiornare le connessioni seguenti: Dati di PowerPivot
  Per cartelle di lavoro di Excel contenenti dati PowerPivot, in Excel Services viene restituito questo errore se viene inviata una richiesta di connessione a un server PowerPivot che non verrà completata.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Si applica a:|Installazione di PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Vedere di seguito.|  
|Testo del messaggio|Impossibile aggiornare i dati per una connessione dati della cartella di lavoro. Riprovare o contattare l'amministratore di sistema. Impossibile aggiornare le connessioni seguenti: Dati di PowerPivot|  
  
## <a name="explanation-and-resolution"></a>Spiegazione e risoluzione  
 Impossibile connettersi o caricare i dati PowerPivot in Excel Services. Di seguito sono riportate le condizioni che causano l'errore:  
  
 **Scenario 1: Servizio non è stato avviato**  
  
 L'istanza di SQL Server Analysis Services (PowerPivot) non è stata avviata. Una password scaduta determinerà l'arresto del servizio in esecuzione. Per altre informazioni sulla modifica della password, vedere [configurare account di servizio PowerPivot](configure-power-pivot-service-accounts.md) e [avviare o arrestare un PowerPivot per SharePoint Server](start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Scenario 2a: Apertura di una precedente versione cartella di lavoro server**  
  
 La cartella di lavoro che si sta tentando di aprire potrebbe essere stata creata con la versione SQL Server 2008 R2 di PowerPivot per Excel. Molto probabilmente, il provider di dati di Analysis Services specificato nella stringa di connessione dati non è presente sul computer che sta gestendo la richiesta.  
  
 In questo caso, si troveranno questo messaggio nel log ULS: "Aggiornamento non riuscito per 'Dati PowerPivot' nella cartella di lavoro '\<URL cartella di lavoro >'", seguito da "Impossibile stabilire una connessione".  
  
 Per determinare la versione della cartella di lavoro, aprirla in Excel e controllare il provider di dati specificato nella stringa di connessione. In una cartella di lavoro SQL Server 2008 R2 viene utilizzato MSOLAP.4 come provider di dati.  
  
 Una soluzione alternativa al problema è l'aggiornamento della cartella di lavoro. In alternativa, è possibile installare librerie client della versione SQL Server 2008 R2 di Analysis Services nei computer fisici che eseguono PowerPivot per SharePoint o Excel Services:  
  
 [Installazione del provider OLE DB Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **Scenario 2b: Excel Services è in esecuzione in un server applicazioni che dispone della versione errata delle librerie client**  
  
 Per impostazione predefinita, SharePoint Server 2010 installa la versione SQL Server 2008 del provider OLE DB per Analysis Services nei server applicazioni su cui è in esecuzione Excel Services. In una farm che supporta l'accesso ai dati PowerPivot, tutti i server fisici che eseguono applicazioni che richiedono dati PowerPivot, ad esempio Excel Services e PowerPivot per SharePoint, devono utilizzare una versione successiva del provider di dati.  
  
 Server che eseguono PowerPivot per SharePoint ottengono automaticamente il provider di dati OLE DB aggiornato. Ad altri server, quali quelli che eseguono un'istanza autonoma di Excel Services senza PowerPivot per SharePoint sullo stesso computer, è necessario applicare una patch perché utilizzino le librerie client più recenti. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
 **Scenario 3: Controller di dominio non è disponibile**  
  
 Il problema può essere dovuto al fatto che non è disponibile alcun controller di dominio per la convalida dell'identità utente. Il controller di dominio viene richiesto da Claims nel Servizio token Windows per autenticare l'utente di SharePoint in ogni connessione. Claims nel Servizio token Windows non utilizza le credenziali memorizzate nella cache. Convalida l'identità utente per ogni connessione.  
  
 È possibile confermare la causa di questo errore visualizzando il file registro di SharePoint. Se nei registri di SharePoint è incluso il messaggio "Impossibile recuperare WindowsIdentity da IClaimsIdentity", l'identità utente non può essere autenticata.  
  
 Per risolvere questo problema, unire in join il computer allo stesso dominio del server PowerPivot o installare un controller di dominio nel computer locale. La seconda soluzione, cioè l'installazione del controller di dominio, richiederà la creazione di account di dominio locali per tutti i servizi e gli utenti. Sarà necessario configurare gli account di servizio e le autorizzazioni di SharePoint per gli account definiti.  
  
 L'installazione di un controller di dominio nel computer è utile se si intende utilizzare PowerPivot per SharePoint in uno stato offline. Per istruzioni dettagliate sull'utilizzo di PowerPivot offline, vedere la voce del blog "Disconnettere il server PowerPivot esterno alla rete" [ http://www.powerpivotgeek.com ](https://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Scenario 4: Server instabile**  
  
 Uno o più servizi possono trovarsi in uno stato incoerente. In alcuni casi, l'esecuzione di IISRESET consentirà di risolvere il problema.  
  
  
