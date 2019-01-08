---
title: Configurare una distribuzione di tipo Scale-Out Server di Report in modalità nativa (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 68951c637d0c0db1fc86bab6405868e73770aca2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395234"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment-ssrs-configuration-manager"></a>Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa (Gestione configurazione SSRS)

  Reporting Services in modalità nativa supporta un modello di distribuzione con scalabilità orizzontale che consente di eseguire più istanze del server di report che condividono un singolo database del server di report. Le distribuzioni con scalabilità orizzontale vengono utilizzate per aumentare la scalabilità di server di report in modo che siano in grado di gestire più utenti simultanei e carichi di esecuzione di report maggiori. Distribuzioni di questo tipo possono essere utilizzate inoltre per dedicare server specifici all'elaborazione di report interattivi o pianificati  
  
 I server di report in modalità SharePoint utilizzano l'infrastruttura di prodotti SharePoint per la scalabilità orizzontale. La scalabilità orizzontale della modalità SharePoint viene eseguita aggiungendo più server di report in modalità SharePoint alla farm di SharePoint. Per informazioni sulla scalabilità orizzontale in modalità SharePoint, vedere [Aggiungere un ulteriore server di report a una farm &#40;con scalabilità orizzontale SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
 **Le distribuzioni con scalabilità orizzontale sono costitute dagli elementi seguenti:**  
  
-   Due o più istanze del server di report che condividono un unico database del server di report.  
  
-   Facoltativamente, un cluster con bilanciamento del carico di rete per distribuire il carico utente interattivo tra le istanze del server di report.  
  
 Quando si distribuisce Reporting Services in un cluster con bilanciamento del carico di rete, è necessario verificare che il nome del server virtuale di bilanciamento del carico venga utilizzato nella configurazione dell'URL del server di report e che i server siano configurati per condividere lo stesso stato di visualizzazione.  
  
 Sebbene Reporting Services non partecipi ai cluster di Microsoft Cluster Services, è tuttavia possibile creare il database del server di report in un'istanza del Motore di database che appartiene a un cluster di failover.  
  
 **Per pianificare, installare e configurare una distribuzione con scalabilità orizzontale, effettuare le operazioni seguenti:**  
  
-   Revisione [installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41; ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online per istruzioni su come installare istanze del server di report.  
  
-   Se si intende ospitare la distribuzione con scalabilità orizzontale in un cluster con bilanciamento del carico di rete, è necessario configurare tale cluster prima di configurare la distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Configurare un server di report in un cluster per il bilanciamento del carico di rete](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  
  
-   Per le linee guida su come condividere un database del server di report e aggiungere server di report a una distribuzione con scalabilità orizzontale, rivedere le procedure in questo argomento.  
  
     Nelle procedure viene illustrato come configurare una distribuzione con scalabilità orizzontale di un server di report con due nodi. Ripetere i passaggi descritti in questo argomento per aggiungere altri nodi del server di report alla distribuzione.  
  
    -   Utilizzare il programma di installazione per installare ogni istanza del server di report che verrà unita alla distribuzione con scalabilità orizzontale.  
  
         Per evitare errori di compatibilità a livello di database al momento della connessione delle istanze del server al database condiviso, verificare che tutte le istanze abbiano la stessa versione. Se, ad esempio, il database del server di report viene creato utilizzando un'istanza del server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , anche tutte le altre istanze presenti nella stessa distribuzione dovranno essere istanze di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    -   Utilizzare Gestione configurazione di Reporting Services per connettere ogni server di report al database condiviso. È possibile connettersi e configurare un solo server di report alla volta.  
  
    -   Utilizzare lo strumento di configurazione di Reporting Services per completare la distribuzione con scalabilità orizzontale unendo le nuove istanze del server di report alla prima istanza del server report già connessa al database del server di report.  
  
### <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>Per installare un'istanza di SQL Server per ospitare i database del server di report  
  
1.  Installare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer che ospiterà i database del server di report. Installare almeno il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
2.  Se necessario, abilitare il server di report per le connessioni remote. In alcune versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le connessioni TCP/IP e Named Pipes remote non sono abilitate per impostazione predefinita. Per verificare se le connessioni remote sono consentite, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizzare le impostazioni di configurazione di rete dell'istanza di destinazione. Se l'istanza remota è anche un'istanza denominata, verificare che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sia abilitato e in esecuzione nel server di destinazione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser fornisce il numero di porta usato per la connessione all'istanza denominata.  
  
### <a name="to-install-the-first-report-server-instance"></a>Per installare la prima istanza del server di report  
  
1.  Installare la prima istanza del server di report che fa parte della distribuzione. Quando si installa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], scegliere l'opzione **Installa senza configurare il server** nella pagina Opzioni di installazione del server di report.  
  
2.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Configurare l'URL del servizio Web ReportServer, l'URL di Gestione report e il database del server di report. Per altre informazioni, vedere [Configurare un server di report &#40;modalità nativa di Reporting Services&#41;](../report-server/configure-a-report-server-reporting-services-native-mode.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Verificare che il server di report sia operativo. Per altre informazioni, vedere [Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-install-and-configure-the-second-report-server-instance"></a>Per installare e configurare la seconda istanza del server di report  
  
1.  Eseguire il programma di installazione per installare una seconda istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un computer diverso o come istanza denominata nello stesso computer. Quando si installa Reporting Services, scegliere l'opzione **Installa senza configurare il server** nella pagina Opzioni di installazione del server di report.  
  
2.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi alla nuova istanza installata.  
  
3.  Connettere il server di report allo stesso database utilizzato per la prima istanza del server di report:  
  
    1.  Fare clic su **Database** per aprire la pagina di Database.  
  
    2.  Fare clic su **Cambia database**.  
  
    3.  Fare clic su **Scegli un database del server di report esistente**.  
  
    4.  Digitare il nome del server dell'istanza del Motore di database di SQL Server che ospita il database del server di report che si desidera utilizzare. Il server deve essere lo stesso a cui ci si è connessi durante i passaggi del set di istruzioni precedente.  
  
    5.  Fare clic su **Test connessione**, quindi fare clic su **successivo**.  
  
    6.  Nelle **Database del Server di Report**, selezionare il database creato per il primo server di report e quindi fare clic su **successivo**. Il nome predefinito è ReportServer. Non selezionare ReportServerTempDB. Questo database viene utilizzato solo per l'archiviazione temporanea dei dati durante l'elaborazione dei report. Se l'elenco dei database è vuoto, ripetere i quattro passaggi precedenti per stabilire una connessione al server.  
  
    7.  Nella pagina Credenziali selezionare il tipo di account e il tipo di credenziali utilizzati dal server di report per la connessione al database del server di report. È possibile utilizzare le stesse credenziali della prima istanza del server di report oppure altre credenziali. Scegliere **Avanti**.  
  
    8.  Fare clic su **Summary** e quindi fare clic su **fine**.  
  
4.  Configurare l'URL del servizio Web ReportServer. Non eseguire ancora il test dell'URL. L'URL non verrà risolto se prima il server di report non viene unito alla distribuzione con scalabilità orizzontale.  
  
5.  Configurare l'URL di Gestione report. Non eseguire ancora il test dell'URL e non tentare di verificare la distribuzione. Il server di report non sarà disponibile fino a quando non viene unito alla distribuzione con scalabilità orizzontale.  
  
### <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>Per unire la seconda istanza del server di report alla distribuzione con scalabilità orizzontale  
  
1.  Aprire lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e riconnettersi alla prima istanza del server di report. Poiché il primo server di report è già inizializzato per operazioni di crittografia reversibile, potrà essere utilizzato per unire altre istanze del server di report alla distribuzione con scalabilità orizzontale.  
  
2.  Fare clic su **Distribuzione con scalabilità orizzontale** per aprire la pagina Distribuzione con scalabilità orizzontale. Verranno visualizzate due voci, una per ciascuna istanza del server di report connessa al database del server di report. La prima istanza del server di report risulterà già unita. Il secondo server di report sarà identificato come "In attesa dell'unione". Se non viene visualizzata alcuna voce simile per la distribuzione, verificare di essere connessi al primo server di report già configurato e inizializzato per l'utilizzo del database del server di report.  
  
     ![Screenshot parziale della pagina Distribuzione con scalabilità orizzontale](../../../2014/sql-server/install/media/scaloutscreen.gif "Screenshot parziale della pagina Distribuzione con scalabilità orizzontale")  
  
3.  Nella pagina distribuzione con scalabilità orizzontale, selezionare l'istanza di server di report che è in attesa di aggiunta alla distribuzione, quindi fare clic su **Aggiungi Server**.  
  
    > [!NOTE]  
    >  **Problema:** Quando si tenta di unire un'istanza di server di report di Reporting Services alla distribuzione con scalabilità orizzontale, potrebbero verificarsi messaggi di errore simili a "Accesso negato".  
    >   
    >  **Soluzione alternativa:** Eseguire il backup di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] chiave di crittografia dal primo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dell'istanza e ripristinare la chiave nel secondo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] server di report. Successivamente, tentare di aggiungere il secondo server alla distribuzione con scalabilità orizzontale di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  A questo punto dovrebbe essere possibile verificare che entrambe le istanze del server di report siano operative. Per verificare la seconda istanza, è possibile utilizzare lo strumento di configurazione di Reporting Services per connettersi al server di report e fare clic su URL servizio Web o URL Gestione report.  
  
 Se si prevede di eseguire i server di report in un cluster di report con carico bilanciato, sono necessarie ulteriori operazioni di configurazione. Per altre informazioni, vedere [Configurare un server di report in un cluster per il bilanciamento del carico di rete](../report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Gestire un server di report in modalità nativa di Reporting Services](../report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
