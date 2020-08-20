---
description: Integration Services (SSIS) in un cluster
title: Integration Services (SSIS) in un cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b3e165cfddce38987b25045926ce2b940d86625b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457061"
---
# <a name="integration-services-ssis-in-a-cluster"></a>Integration Services (SSIS) in un cluster

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] il clustering non è consigliato, poiché il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non è un servizio cluster o compatibile con i cluster né supporta il failover tra nodi del cluster. In un ambiente cluster è pertanto necessario installare e avviare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come servizio autonomo in ogni nodo del cluster.  
  
 Sebbene il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non sia un servizio cluster, è possibile configurarlo manualmente come risorsa cluster dopo l'installazione separata di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster.  
  
 Se tuttavia la disponibilità elevata rappresenta l'obiettivo della configurazione di un ambiente hardware cluster, è consigliabile evitare di configurare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster.  Per gestire i pacchetti in qualsiasi nodo del cluster da qualsiasi altro nodo del cluster, modificare il file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster. I file di configurazione devono essere modificati in modo da puntare a tutte le istanze disponibili di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui sono archiviati i pacchetti. Questa soluzione garantisce l'elevata disponibilità di cui necessita la maggior parte degli utenti, senza i problemi potenziali riscontrati quando il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è configurato come risorsa cluster. Per altre informazioni su come modificare il file di configurazione, vedere [Servizio Integration Services &#40;SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 Per prendere decisioni appropriate sulla configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un ambiente cluster, è importante comprendere il ruolo di tale servizio. Per altre informazioni, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="disadvantages"></a>Svantaggi
 Tra i potenziali svantaggi della configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster sono inclusi i seguenti:  
  
-   **In caso di failover, i pacchetti in esecuzione non si riavviano.**
    
    È possibile risolvere gli errori relativi ai pacchetti riavviando i pacchetti dai checkpoint. È possibile eseguire il riavvio dai checkpoint senza configurare il servizio come risorsa cluster. Per ulteriori informazioni, vedere [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
-   Quando si configura il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un gruppo di risorse diverso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non è possibile utilizzare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dai computer client per gestire i pacchetti archiviati nel database msdb. Tramite il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non possono essere delegate le credenziali in questo scenario a doppio hop.  
  
-   Quando sono presenti più gruppi di risorse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che includono il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un cluster, un failover potrebbe provocare risultati imprevisti. Si consideri lo scenario seguente. Il Gruppo 1, che include il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è in esecuzione nel Nodo A. Il Gruppo 2, che come il Gruppo 1 include il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è in esecuzione nel Nodo B. Si verifica il failover del Gruppo 2 nel Nodo A. Il tentativo di avviare un'altra istanza del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Nodo A ha esito negativo in quanto il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un servizio a istanza singola. L'esito del tentativo di failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel Nodo A dipende dalla configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Gruppo 2. Se il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è stato configurato in modo da influire sugli altri servizi nel gruppo di risorse, il failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha esito negativo a causa dell'errore del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se il servizio è stato configurato per non influire sugli altri servizi nel gruppo di risorse, verrà eseguito il failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel Nodo A. A meno che il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel Gruppo 2 non sia stato configurato in modo da non influire sugli altri servizi nel gruppo di risorse, l'errore di failover del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può provocare anche un errore di failover del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

## <a name="configure-the-service-as-a-cluster-resource"></a>Configurare il servizio come risorsa cluster
In questa sezione vengono fornite le istruzioni necessarie per la configurazione per i clienti che ritengono che i vantaggi della configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster siano prevalenti rispetto agli svantaggi. [!INCLUDE[msCoName](../../includes/msconame-md.md)] non consiglia tuttavia la configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster.  
  
 Per configurare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster, è necessario completare le attività seguenti.  
  
-   Installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un cluster.  
  
     Per installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un cluster, è necessario installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster.  
  
-   Configurare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster.  
  
     Dopo avere installato Integration Services in ogni nodo nel cluster, è necessario configurarlo come risorsa cluster. Quando si configura il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster, è possibile aggiungere il servizio allo stesso gruppo di risorse del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]o a un gruppo diverso. Nella tabella seguente sono descritti i possibili vantaggi e svantaggi della selezione di un gruppo di risorse.  
  
    |Quando Integration Services e SQL Server sono nello stesso gruppo di risorse|Quando Integration Services e SQL Server sono in gruppi di risorse diversi|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |I computer client possono utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire i pacchetti archiviati nel database msdb in quanto sia il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono in esecuzione nello stesso server virtuale. Questa configurazione consente di evitare i problemi di delega dello scenario a doppio hop.|I computer client non possono utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per gestire i pacchetti archiviati nel database msdb. Il client può connettersi al server virtuale in cui è in esecuzione il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tale computer non può tuttavia delegare le credenziali dell'utente al server virtuale in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa situazione è nota come scenario a doppio hop.|  
    |Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli altri servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si contendono la CPU e altre risorse del computer.|Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli altri servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non si contendono la CPU e altre risorse del computer in quanto i diversi gruppi di risorse sono configurati in nodi diversi.|  
    |Il caricamento e il salvataggio di pacchetti nel database msdb sono più veloci e generano un minore traffico di rete in quanto entrambi i servizi sono in esecuzione nello stesso computer.|Il caricamento e il salvataggio di pacchetti nel database msdb potrebbero essere più lenti e generare un maggiore traffico di rete.|  
    |Entrambi i servizi sono online o offline contemporaneamente.|Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] potrebbe essere online mentre il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] è offline. I pacchetti archiviati nel database msdb del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non sono pertanto disponibili.|  
    |Non è possibile spostare rapidamente il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un altro nodo, se necessario.|È possibile spostare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un altro nodo più rapidamente, se necessario.|  
  
     Dopo avere deciso a quale gruppo di risorse aggiungere [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario configurare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster in tale gruppo.  
  
-   Configurare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e l'archivio pacchetti.  
  
     Dopo avere configurato [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] come risorsa cluster, è necessario modificare il percorso e il contenuto del file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster. Queste modifiche consentono di rendere disponibili sia il file di configurazione che l'archivio pacchetti in tutti i nodi in caso di failover. Dopo aver modificato il percorso e il contenuto del file di configurazione, portare il servizio online.  
  
-   Portare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] online come risorsa cluster.  
  
 Dopo avere configurato il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un cluster o in un server, potrebbe essere necessario configurare le autorizzazioni DCOM per potersi connettere al servizio da un computer client. Per altre informazioni, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 Tramite il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non possono essere delegate le credenziali. Non è pertanto possibile utilizzare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per gestire i pacchetti archiviati nel database msdb quando si verificano le condizioni seguenti:  
  
-   Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono in esecuzione in server separati o in server virtuali.  
  
-   Il client in cui è in esecuzione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è un terzo computer.  
  
 Il client può connettersi al server virtuale in cui è in esecuzione il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tale computer non può tuttavia delegare le credenziali dell'utente al server virtuale in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa situazione è nota come scenario a doppio hop.  
  
### <a name="to-install-integration-services-on-a-cluster"></a>Per installare Integration Services in un cluster  
  
1.  Installare e configurare un cluster con uno o più nodi.  
  
2.  (Facoltativo) Installare i servizi cluster, ad esempio il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
3.  Installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in ogni nodo del cluster.  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>Per configurare Integration Services come risorsa cluster  
  
1.  Aprire **Amministrazione cluster**.  
  
2.  Nell'albero della console selezionare la cartella Gruppi.  
  
3.  Nel riquadro dei risultati selezionare il gruppo a cui si desidera aggiungere [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
    -   Per aggiungere Integration Services come risorsa cluster allo stesso gruppo di risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare il gruppo a cui appartiene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Per aggiungere Integration Services come risorsa cluster a un gruppo diverso rispetto a quello di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare un gruppo diverso da quello a cui appartiene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
4.  Scegliere **Nuovo** dal menu **File**e quindi fare clic su **Risorsa**.  
  
5.  Nella pagina **Nuova risorsa** della procedura guidata per la creazione di risorse selezionare **"Servizio generico"** come **Tipo di servizio**. Non modificare il valore di **Gruppo**. Fare clic su **Avanti**.  
  
6.  Nella pagina **Proprietari possibili** aggiungere o rimuovere i nodi del cluster come possibili proprietari della risorsa. Fare clic su **Avanti**.  
  
7.  Per aggiungere dipendenze, nella pagina **Relazioni di dipendenza** selezionare una risorsa in **Risorse disponibili**e quindi fare clic su **Aggiungi**. In caso di failover, è necessario che sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che il disco condiviso in cui sono archiviati i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tornino online prima di poter riportare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] online. Dopo avere selezionato le dipendenze, fare clic su **Avanti**.  
  
     Per altre informazioni, vedere [Aggiungere dipendenze a una risorsa di SQL Server](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md).  
  
8.  Nella pagina **Parametri servizio generico** immettere **MsDtsServer** come nome del servizio. Fare clic su **Avanti**.  
  
9. Nella pagina **Replica Registro di sistema** fare clic su **Aggiungi** per aggiungere la chiave del Registro di sistema che identifica il percorso del file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tale file deve trovarsi in un disco condiviso nello stesso gruppo di risorse del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
10. Nella finestra di dialogo **Chiave del Registro di sistema** digitare **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**. Fare clic su **OK**e quindi su **Fine**.  
  
     A questo punto, il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è stato aggiunto come risorsa cluster.  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>Per configurare il servizio Integration Services e l'archivio pacchetti  
  
1.  Individuare il file di configurazione in %Programmi%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml. Copiarlo nel disco condiviso per il gruppo al quale è stato aggiunto il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Nel disco condiviso creare una nuova cartella denominata **Pacchetti** da usare come archivio pacchetti. Concedere le autorizzazioni di visualizzazione delle cartelle e di scrittura per la nuova cartella agli utenti e ai gruppi appropriati.  
  
3.  Nel disco condiviso aprire il file di configurazione in un editor di testo o XML. Modificare il valore dell'elemento **ServerName** impostando il nome del server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtuale presente nello stesso gruppo di risorse.  
  
4.  Modificare il valore dell'elemento **StorePath** impostando il percorso completo della cartella **Pacchetti** creata nel disco condiviso in uno dei passaggi precedenti.  
  
5.  In ogni nodo aggiornare il valore di **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** nel Registro di sistema impostando il percorso e il nome completo del file di configurazione del servizio nel disco condiviso.  
  
### <a name="to-bring-the-integration-services-service-online"></a>Per portare online il servizio Integration Services  
  
-   In **Amministrazione**cluster selezionare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , fare clic con il pulsante destro del mouse e scegliere **Online** dal menu di scelta rapida. A questo punto, il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è online come risorsa cluster.  
  
  
