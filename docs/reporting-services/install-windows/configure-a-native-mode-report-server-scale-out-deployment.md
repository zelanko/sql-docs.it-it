---
description: Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa
title: Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa | Microsoft Docs
ms.date: 11/29/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8e9e8fab90a0c2f21ae29d113ea896b471177f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460003"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment"></a>Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services in modalità nativa supporta un modello di distribuzione con scalabilità orizzontale che consente di eseguire più istanze del server di report che condividono un singolo database del server di report. Le distribuzioni con scalabilità orizzontale vengono utilizzate per aumentare la scalabilità di server di report in modo che siano in grado di gestire più utenti simultanei e carichi di esecuzione di report maggiori. Tali distribuzioni possono essere utilizzate inoltre per dedicare server specifici all'elaborazione di report interattivi o pianificati.

Per il Server di report di Microsoft Power BI è necessario configurare l'affinità del client (denominata anche sessioni permanenti) nel bilanciamento del carico per gli ambienti scale-out, al fine di garantire prestazioni adeguate.  
  
Per SQL Server 2016 Reporting Services e versioni precedenti, i server di report in modalità SharePoint usano l'infrastruttura dei prodotti SharePoint per la scalabilità orizzontale. La scalabilità orizzontale della modalità SharePoint viene eseguita aggiungendo più server di report in modalità SharePoint alla farm di SharePoint. Per informazioni sulla scalabilità orizzontale in modalità SharePoint, vedere [Aggiungere un ulteriore server di report a una farm &#40;con scalabilità orizzontale SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
 
  La *distribuzione con scalabilità orizzontale* viene usata negli scenari seguenti:  
  
-   Come prerequisito per il bilanciamento del carico di più server di report in un cluster di server. Prima di bilanciare il carico di più server di report, è innanzitutto necessario configurare i server di report per la condivisione dello stesso database del server di report.  
  
-   Per segmentare applicazioni del server di report in computer diversi, utilizzando un server per l'elaborazione interattiva dei report e un secondo server per l'elaborazione pianificata dei report. In questo scenario ogni istanza del server elabora tipi diversi di richieste per lo stesso contenuto del server di report archiviato nel database del server di report condiviso.  
  
 **Le distribuzioni con scalabilità orizzontale sono costitute dagli elementi seguenti:**  
  
-   Due o più istanze del server di report che condividono un unico database del server di report.  
  
-   Facoltativamente, un cluster con bilanciamento del carico di rete per distribuire il carico utente interattivo tra le istanze del server di report.  
  
 Quando si distribuisce Reporting Services in un cluster con bilanciamento del carico di rete, è necessario verificare che il nome del server virtuale di bilanciamento del carico venga utilizzato nella configurazione dell'URL del server di report e che i server siano configurati per condividere lo stesso stato di visualizzazione.  
  
 Sebbene Reporting Services non partecipi ai cluster di Microsoft Cluster Services, è tuttavia possibile creare il database del server di report in un'istanza del Motore di database che appartiene a un cluster di failover.  
  
 **Per pianificare, installare e configurare una distribuzione con scalabilità orizzontale, effettuare le operazioni seguenti:**  
  
-   Per istruzioni su come installare istanze del server di report, vedere [Installare SQL Server dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   Se si intende ospitare la distribuzione con scalabilità orizzontale in un cluster con bilanciamento del carico di rete, è necessario configurare tale cluster prima di configurare la distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Configurare un server di report in un cluster per il bilanciamento del carico di rete](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  
  
-   Per le linee guida su come condividere un database del server di report e aggiungere server di report a una distribuzione con scalabilità orizzontale, rivedere le procedure in questo argomento.  
  
     Nelle procedure viene illustrato come configurare una distribuzione con scalabilità orizzontale di un server di report con due nodi. Ripetere i passaggi descritti in questo argomento per aggiungere altri nodi del server di report alla distribuzione.  
  
    -   Utilizzare il programma di installazione per installare ogni istanza del server di report che verrà unita alla distribuzione con scalabilità orizzontale.  
  
         Per evitare errori di compatibilità a livello di database al momento della connessione delle istanze del server al database condiviso, verificare che tutte le istanze abbiano la stessa versione. Se, ad esempio, il database del server di report viene creato usando un'istanza del server di report di SQL Server 2016, anche tutte le altre istanze presenti nella stessa distribuzione dovranno essere istanze di SQL Server 2016.  
  
    -   Utilizzare Gestione configurazione di Reporting Services per connettere ogni server di report al database condiviso. È possibile connettersi e configurare un solo server di report alla volta.  
  
    -   Utilizzare lo strumento di configurazione di Reporting Services per completare la distribuzione con scalabilità orizzontale unendo le nuove istanze del server di report alla prima istanza del server report già connessa al database del server di report.  
  
## <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>Per installare un'istanza di SQL Server per ospitare i database del server di report  
  
1.  Installare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer che ospiterà i database del server di report. Installare almeno il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
2.  Se necessario, abilitare il server di report per le connessioni remote. In alcune versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le connessioni TCP/IP e Named Pipes remote non sono abilitate per impostazione predefinita. Per verificare se le connessioni remote sono consentite, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizzare le impostazioni di configurazione di rete dell'istanza di destinazione. Se l'istanza remota è anche un'istanza denominata, verificare che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser sia abilitato e in esecuzione nel server di destinazione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser fornisce il numero di porta usato per la connessione all'istanza denominata. 

## <a name="service-accounts"></a>Account di servizio

Gli account del servizio usati per l'istanza di Reporting Services sono importanti quando si lavora con una distribuzione con scalabilità orizzontale. È necessario scegliere una delle opzioni seguenti durante la distribuzione delle istanze di Reporting Services.

**Opzione 1:** tutte le istanze di Reporting Services devono essere configurate con lo stesso account utente di dominio per l'account del servizio.

**Opzione 2:** a ogni singolo account del servizio, account di dominio o non di dominio, devono essere concesse le autorizzazioni dbadmin all'interno dell'istanza di database di SQL Server che ospita il database del catalogo ReportServer.

Se è stata specificata una configurazione diversa dalle due opzioni precedenti, è possibile che si verifichino errori intermittenti delle attività di modifica con SQL Agent. Questi errori vengono visualizzati come errori nel log di Reporting Services e nel portale Web quando si modifica una sottoscrizione report.

```
An error occurred within the report server database.  This may be due to a connection failure, timeout or low disk condition within the database.
``` 

Il problema sarà intermittente perché solo il server che ha creato l'attività di SQL Agent disporrà dei diritti per visualizzare, eliminare o modificare l'elemento. Se non si sceglie una delle opzioni precedenti, le operazioni avranno esito negativo quando il servizio di bilanciamento del carico invia tutte le richieste per la sottoscrizione al server che ha creato l'attività di SQL Agent. 
  
## <a name="to-install-the-first-report-server-instance"></a>Per installare la prima istanza del server di report  
  
1.  Installare la prima istanza del server di report che fa parte della distribuzione. Quando si installa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], scegliere l'opzione **Installa senza configurare il server** nella pagina Opzioni di installazione del server di report.  
  
2.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Configurare l'URL del servizio Web ReportServer, l'URL del portale Web e il database del server di report. Per altre informazioni, vedere [Configurare un server di report &#40;modalità nativa di Reporting Services&#41;](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)
  
4.  Verificare che il server di report sia operativo. Per altre informazioni, vedere [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
## <a name="to-install-and-configure-the-second-report-server-instance"></a>Per installare e configurare la seconda istanza del server di report  
  
1.  Eseguire il programma di installazione per installare una seconda istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un computer diverso o come istanza denominata nello stesso computer. Quando si installa Reporting Services, scegliere l'opzione **Installa senza configurare il server** nella pagina Opzioni di installazione del server di report.  
  
2.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi alla nuova istanza installata.  
  
3.  Connettere il server di report allo stesso database utilizzato per la prima istanza del server di report:  
  
    1.  Selezionare **Database** per aprire la pagina Database.  
  
    2.  Selezionare **Cambia database**.  
  
    3.  Selezionare **Scegli un database del server di report esistente**.  
  
    4.  Digitare il nome del server dell'istanza del Motore di database di SQL Server che ospita il database del server di report che si desidera utilizzare. Il server deve essere lo stesso a cui ci si è connessi durante i passaggi del set di istruzioni precedente.  
  
    5.  Selezionare **Test connessione**, quindi fare clic su **Avanti**.  
  
    6.  In **Database server report**selezionare il database creato per il primo server di report, quindi fare clic su **Avanti**. Il nome predefinito è ReportServer. Non selezionare ReportServerTempDB. Questo database viene utilizzato solo per l'archiviazione temporanea dei dati durante l'elaborazione dei report. Se l'elenco dei database è vuoto, ripetere i quattro passaggi precedenti per stabilire una connessione al server.  
  
    7.  Nella pagina Credenziali selezionare il tipo di account e il tipo di credenziali utilizzati dal server di report per la connessione al database del server di report. È possibile utilizzare le stesse credenziali della prima istanza del server di report oppure altre credenziali. Selezionare **Avanti**.  
  
    8.  Selezionare **Riepilogo** e quindi fare clic su **Fine**.  
  
4.  Configurare l' **URL servizio Web**ReportServer. Non eseguire ancora il test dell'URL. L'URL non verrà risolto se prima il server di report non viene unito alla distribuzione con scalabilità orizzontale.  
  
5.  Configurare l' **URL del portale Web**. Non eseguire ancora il test dell'URL e non tentare di verificare la distribuzione. Il server di report non sarà disponibile fino a quando non viene unito alla distribuzione con scalabilità orizzontale.  
  
## <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>Per unire la seconda istanza del server di report alla distribuzione con scalabilità orizzontale  
  
1.  Aprire lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e riconnettersi alla prima istanza del server di report. Poiché il primo server di report è già inizializzato per operazioni di crittografia reversibile, potrà essere utilizzato per unire altre istanze del server di report alla distribuzione con scalabilità orizzontale.  
  
2.  Fare clic su **Distribuzione con scalabilità orizzontale** per aprire la pagina Distribuzione con scalabilità orizzontale. Verranno visualizzate due voci, una per ciascuna istanza del server di report connessa al database del server di report. La prima istanza del server di report risulterà già unita. Il secondo server di report sarà identificato come "In attesa dell'unione". Se non viene visualizzata alcuna voce simile per la distribuzione, verificare di essere connessi al primo server di report già configurato e inizializzato per l'utilizzo del database del server di report.  
  
     ![Screenshot parziale della pagina Distribuzione con scalabilità orizzontale](../../reporting-services/install-windows/media/scaloutscreen.gif "Screenshot parziale della pagina Distribuzione con scalabilità orizzontale")  
  
3.  Nella pagina Distribuzione con scalabilità orizzontale selezionare l'istanza del server di report in attesa dell'aggiunta alla distribuzione, quindi selezionare **Aggiungi server**.  
  
    > [!NOTE]  
    >  **Problema:** quando si cerca di aggiungere un'istanza del server di report di Reporting Services alla distribuzione con scalabilità orizzontale, potrebbero essere visualizzati messaggi di errore di tipo "Accesso negato".  
    >   
    >  **Soluzione alternativa:** eseguire il backup della chiave di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dalla prima istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e ripristinare la chiave nel secondo server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Successivamente, tentare di aggiungere il secondo server alla distribuzione con scalabilità orizzontale di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  A questo punto dovrebbe essere possibile verificare che entrambe le istanze del server di report siano operative. Per verificare la seconda istanza, è possibile usare lo strumento Configurazione di Reporting Services per connettersi al server di report e fare clic su **URL servizio Web** o su **URL del portale Web**.  
  
 Se si prevede di eseguire i server di report in un cluster di report con carico bilanciato, sono necessarie ulteriori operazioni di configurazione. Per altre informazioni, vedere [Configurare un server di report in un cluster per il bilanciamento del carico di rete](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  

## <a name="next-steps"></a>Passaggi successivi

[Configurare un account del servizio](configure-the-report-server-service-account-ssrs-configuration-manager.md)
[Configurare un URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Creare un database del server di report in modalità nativa](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[Configurare gli URL del server di report](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurare una connessione del database del server di report](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
[Gestire un server di report in modalità nativa di Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
