---
title: Acquisire e configurare un server di caricamento - Parallel Data Warehouse | Microsoft Docs
description: Questo articolo descrive come acquisire e configurare un server di caricamento come un sistema di Windows non appliance per l'invio di caricamenti di dati per Parallel Data Warehouse (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d753237841695786de3d368bebf9a606875ea634
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961614"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Acquisire e configurare un server di caricamento per Parallel Data Warehouse
Questo articolo descrive come acquisire e configurare un server di caricamento come un sistema di Windows non appliance per l'invio di caricamenti di dati per Parallel Data Warehouse (PDW).  
  
## <a name="Basics"></a>Nozioni di base  
Il server di caricamento:  
  
-   Non è necessario essere un singolo server. È possibile caricare contemporaneamente a più server di caricamento.  
  
-   Viene fornita e gestita dal team IT. Potrebbe essere già presente uno o più server che può essere utilizzato per il caricamento dei dati in PDW.  
  
-   Si trova nel proprio rack non appliance e non può essere inserito all'interno dell'appliance di sistema di piattaforma Analitica.  
  
-   È connesso al dispositivo tramite la rete InfiniBand di Appliance o over Ethernet. Per prestazioni ottimali, è consigliabile usare InfiniBand.  
  
-   È nel proprio dominio del cliente, non del dominio appliance. Non vi è alcuna relazione di trust tra il dominio del cliente e il dominio di appliance.  
  
## <a name="Step1"></a>Passaggio 1: Determinare i requisiti di capacità  
Il caricamento del sistema può essere progettato come uno o più server di caricamento che eseguono caricamenti simultanei. Ogni server durante il caricamento non deve essere dedicata solo per il caricamento, purché lo gestirà i requisiti di archiviazione e le prestazioni del carico di lavoro.  
  
Requisiti di sistema per un server di caricamento è quasi completamente dipendono il proprio carico di lavoro. Usare la [caricamento capacità pianificazione foglio di lavoro Server](loading-server-capacity-planning-worksheet.md) per determinare i requisiti di capacità.  
  
## <a name="Step2"></a>Passaggio 2: Acquisire il sServer  
Ora che meglio comprendere i requisiti di capacità, è possibile pianificare i server e componenti di rete che sarà necessario acquistare o effettuare il provisioning. Incorporare il seguente elenco di requisiti nel piano di acquisto e quindi acquistare il server o effettuare il provisioning di un server esistente.  
  
### <a name="R"></a>Requisiti software  
Sistemi operativi supportati:  
  
-   Windows Server 2012 o Windows Server 2012 R2. Questi sistemi operativi richiedono la scheda di rete FDR.  
  
-   Windows Server 2008 R2. Questo sistema operativo richiede la scheda di rete DDR.  
  
Il server deve usare le impostazioni locali EN-US per poter utilizzare lo strumento della riga di comando di caricamento dwloader. dwloader non supporta altre impostazioni locali.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisiti di rete per Windows Server 2012 e Windows Server 2012 R2  
Sebbene non obbligatorio per il caricamento, InfiniBand è il tipo di connessione consigliato per il caricamento dei server. Per prestazioni ottimali, usare Windows Server 2012 o Windows Server 2012 R2 e la scheda di rete InfiniBand FDR per connettere il server di caricamento per la rete InfiniBand di appliance.  
  
Per prepararsi per una connessione di Windows Server 2012 o Windows Server 2012 R2 InfiniBand:  
  
1.  Prevede di installare in rack server abbastanza ravvicinati per l'appliance in modo che è possibile connetterla all'appliance InfiniBand attiva. Per altre informazioni da tecnologie Mellanox InfiniBand, vedere il whitepaper [Introduzione a InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Acquistare una scheda di rete InfiniBand FDR Mellanox ConnectX-3 porta singola o doppia. È consigliabile acquistare la scheda di rete con due porte per la tolleranza di errore durante la trasmissione dei dati. Una scheda di rete due porte è necessaria per la disponibilità elevata.  
  
3.  Acquistare 2 cavi FDR InfiniBand per una scheda a porta doppia o cable FDR InfiniBand 1 per una scheda di singola porta. I cavi InfiniBand FDR si connetteranno il server di caricamento per la rete InfiniBand di appliance. La lunghezza del cavo dipende la distanza tra il server durante il caricamento e le opzioni di InfiniBand appliance, in base al proprio ambiente.  
  
## <a name="Step3"></a>Passaggio 3: Connettere il server alle reti InfiniBand  
Usare questi passaggi per connettere il server di caricamento per la rete InfiniBand. Se il server non usa la rete InfiniBand, ignorare questo passaggio.  
  
1.  Rack server abbastanza ravvicinati per l'appliance in modo che è possibile connetterla alla rete InfiniBand appliance.  
  
2.  Installare la scheda di rete InfiniBand FDR Mellanox ConnectX-3 InfiniBand nel server durante il caricamento.  
  
3.  Usare i cavi FDR per connettere la scheda di rete InfiniBand a una delle due opzioni InfiniBand nel primo rack appliance.  
  
4.  Installare e configurare il driver di Windows appropriato per la scheda di rete InfiniBand.  
  
    -   I driver InfiniBand per Windows sono sviluppati dal team di OpenFabrics Alliance, un consorzio di settore di fornitori InfiniBand.  Il driver corretto possa avere stato distribuito con la scheda di rete InfiniBand. In caso contrario, il driver può essere scaricato da www.openfabrics.org.  
  
5.  Configurare le impostazioni per le schede di rete InfiniBand e DNS. Per istruzioni sulla configurazione, vedere [schede di rete InfiniBand configurare](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Passaggio 4: Installare gli strumenti di caricamento  
Gli strumenti Client sono disponibili per il download da Microsoft Download Center. 

Per installare dwloader, eseguire l'installazione dwloader agli strumenti client.
  
Se si prevede di utilizzare Integration Services per il caricamento, è necessario installare Integration Services e le schede di destinazione di Integration Services. Le schede sono disponibili negli strumenti Client.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Passaggio 5: Avviare il caricamento  
A questo punto si è pronti avviare il caricamento dei dati. Per altre informazioni, vedere:  
  
1.  [Strumento di caricamento della riga di comando dwloader](dwloader.md)  
  
2.  [Panoramica di carico](load-overview.md)  
  
## <a name="performance"></a>Prestazioni  
Per ottenere migliori prestazioni in Windows Server 2012 e versioni successive di caricamento, attivare l'inizializzazione immediata dei File in modo che quando i dati vengono sovrascritti, il sistema operativo non sovrascriverà i dati esistenti con zeri. Se si tratta di un rischio per la sicurezza perché sono ancora presenti dati precedenti sui dischi, quindi assicurarsi di disattivare l'inizializzazione immediata dei File.  
  
## <a name="Security"></a>Avvisi di sicurezza  
Poiché i dati da caricare non vengono archiviati nell'appliance, il team IT è responsabile per la gestione di tutti gli aspetti della sicurezza per i dati da caricare. Ad esempio, ciò include la gestione di sicurezza dei dati da caricare, la sicurezza del server utilizzato per archiviare i carichi e la protezione dell'infrastruttura di rete che connette il server di caricamento per l'appliance di SQL Server PDW.  
  
> [!IMPORTANT]  
> È particolarmente importante per la protezione di ogni server di caricamento che userà lo strumento della riga di comando di caricamento dwloader. Quando dwloader carica i dati, esegue l'autenticazione prima di tutto con il nodo di controllo e quindi al termine dell'autenticazione Sposta i dati dal server durante il caricamento direttamente ai nodi di calcolo tramite canali di dati. Convalida del certificato non viene eseguito durante una tremolio tra ogni server durante il caricamento e ogni nodo di calcolo. In tal modo i nodi di calcolo esposti a potenziali attacchi man-in-the-middle a ciascun canale di dati durante il caricamento. Questi attacchi potrebbero essere manomessi dati e/o la divulgazione di informazioni.  
  
Per ridurre i rischi di sicurezza con i dati, si consiglia quanto segue:  
  
-   Impostare un account di Windows che viene usato esclusivamente allo scopo di caricamento di dati in PDW. Concedere all'account le autorizzazioni per il percorso di caricamento e altrove.  
  
-   Designare un utente PDW che dispone delle autorizzazioni per caricare i dati. A seconda dei requisiti di sicurezza, è possibile che un utente specifico per ogni database.  
  
-   Operazioni nel server durante il caricamento possono accettare un percorso UNC da cui per estrarre i dati dall'esterno della rete interna attendibile. E un utente malintenzionato sulla rete o con grado di influenzare la risoluzione dei nomi può intercettare o modificare i dati inviati a SQL Server PDW. Ciò comporta un rischio di divulgazione manomissioni e informazioni. Tramite la richiesta di firma per la connessione deve essere attenuato manomissioni. Per ridurre questo rischio, impostare l'opzione dei criteri di gruppo seguenti **protezione\Criteri Locali\opzioni di sicurezza** nel server di caricamento:  **Client di rete Microsoft: Firma digitale alle comunicazioni (sempre): Abilitato**  
  
-   Disattivare l'inizializzazione immediata dei File in Windows Server 2012 e versioni successive. Questo è un compromesso tra prestazioni e sicurezza, come indicato nella sezione prestazioni. È necessario effettuare la scelta migliore in base ai requisiti di sicurezza.  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica su backup e ripristino](backup-and-restore-overview.md)  
  
