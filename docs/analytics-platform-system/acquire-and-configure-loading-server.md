---
title: Acquisisci & Configura server di caricamento
description: Questo articolo descrive come acquisire e configurare un server di caricamento come sistema Windows non Appliance per l'invio di caricamenti di dati a Parallel data warehouse (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401481"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Acquisire e configurare un server di caricamento per data warehouse paralleli
Questo articolo descrive come acquisire e configurare un server di caricamento come sistema Windows non Appliance per l'invio di caricamenti di dati a Parallel data warehouse (PDW).  
  
## <a name="basics"></a><a name="Basics"></a>Nozioni di base  
Server di caricamento:  
  
-   Non deve essere un singolo server. È possibile caricare simultaneamente con più server di caricamento.  
  
-   Viene fornito e gestito dal team IT. È possibile che si disponga già di un server o di server da usare per il caricamento dei dati in PDW.  
  
-   Si trova nel proprio rack non Appliance e non può essere inserito nell'appliance del sistema della piattaforma di analisi.  
  
-   È connesso al dispositivo tramite la rete InfiniBand dell'appliance o tramite Ethernet. Per le prestazioni, è consigliabile usare InfiniBand.  
  
-   Si trova nel dominio del cliente, non nel dominio dell'appliance. Non esiste alcuna relazione di trust tra il dominio del cliente e il dominio dell'appliance.  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>Passaggio 1: determinare i requisiti di capacità  
Il sistema di caricamento può essere progettato come uno o più server di caricamento che eseguono carichi simultanei. Per ogni server di caricamento non è necessario dedicarsi solo al caricamento, purché vengano gestiti i requisiti di prestazioni e archiviazione del carico di lavoro.  
  
I requisiti di sistema per un server di caricamento dipendono quasi completamente dal proprio carico di lavoro. Utilizzare il [foglio](loading-server-capacity-planning-worksheet.md) di lavoro per la pianificazione della capacità del server per determinare i requisiti di capacità.  
  
## <a name="step-2-acquire-the-sserver"></a><a name="Step2"></a>Passaggio 2: acquisire il sServer  
Ora che è possibile comprendere meglio i requisiti di capacità, è possibile pianificare i server e i componenti di rete che sarà necessario acquistare o effettuare il provisioning. Incorporare l'elenco di requisiti seguente nel piano di acquisto, quindi acquistare il server o effettuare il provisioning di un server esistente.  
  
### <a name="software-requirements"></a><a name="R"></a>Requisiti software  
Sistemi operativi supportati:  
  
-   Windows Server 2012 o Windows Server 2012 R2. Questi sistemi operativi richiedono la scheda di rete FDR.  
  
-   Windows Server 2008 R2. Questo sistema operativo richiede la scheda di rete DDR.  
  
Per usare lo strumento di caricamento da riga di comando dwloader, il server deve usare le impostazioni locali EN-US. dwloader non supporta altre impostazioni locali.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisiti di rete per Windows Server 2012 e Windows Server 2012 R2  
Sebbene non sia necessario per il caricamento, InfiniBand è il tipo di connessione consigliato per il caricamento dei server. Per ottenere prestazioni ottimali, utilizzare Windows Server 2012 o Windows Server 2012 R2 e la scheda di rete InfiniBand FDR per connettere il server di caricamento alla rete InfiniBand dell'appliance.  
  
Per preparare una connessione InfiniBand di Windows Server 2012 o Windows Server 2012 R2:  
  
1.  Pianificare il rack del server abbastanza vicino al dispositivo, in modo che sia possibile connetterlo ai commutatori InfiniBand dell'appliance. Per ulteriori informazioni sulle tecnologie Mellanox relative a InfiniBand, vedere il white paper [Introduzione a InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Acquistare una scheda di rete Mellanox ConnectX-3 FDR InfiniBand single o Dual Port. Si consiglia di acquistare la scheda di rete con due porte per la tolleranza di errore durante la trasmissione dei dati. Per la disponibilità elevata, è necessaria una scheda di rete a due porte.  
  
3.  Acquistare 2 cavi InfiniBand FDR per una scheda a doppia porta o 1 cavo InfiniBand FDR per una singola scheda di porta. I cavi InfiniBand FDR collegheranno il server di caricamento alla rete InfiniBand dell'appliance. La lunghezza del cavo dipende dalla distanza tra il server di caricamento e i commutatori InfiniBand dell'appliance, in base all'ambiente in uso.  
  
## <a name="step-3-connect-the-server-to-the-infiniband-networks"></a><a name="Step3"></a>Passaggio 3: connettere il server alle reti InfiniBand  
Utilizzare questa procedura per connettere il server di caricamento alla rete InfiniBand. Se il server non utilizza la rete InfiniBand, ignorare questo passaggio.  
  
1.  Rack il server sufficientemente vicino al dispositivo in modo che sia possibile connetterlo alla rete InfiniBand dell'appliance.  
  
2.  Installare la scheda di rete InfiniBand Mellanox ConnectX-3 FDR InfiniBand nel server di caricamento.  
  
3.  Usare i cavi FDR per connettere la scheda di rete InfiniBand a una delle due opzioni InfiniBand nel primo rack Appliance.  
  
4.  Installare e configurare il driver Windows appropriato per la scheda di rete InfiniBand.  
  
    -   I driver InfiniBand per Windows sono sviluppati da OpenFabrics Alliance, un consorzio di settore di fornitori InfiniBand.  Il driver corretto potrebbe essere stato distribuito con la scheda di rete InfiniBand. In caso contrario, il driver può essere scaricato da www.openfabrics.org.  
  
5.  Configurare le impostazioni InfiniBand e DNS per le schede di rete. Per istruzioni sulla configurazione, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="step-4-install-the-loading-tools"></a><a name="Step4"></a>Passaggio 4: installare gli strumenti di caricamento  
Gli strumenti client sono disponibili per il download dall'area download Microsoft. 

Per installare dwloader, eseguire l'installazione di dwloader dagli strumenti client.
  
Se si prevede di utilizzare Integration Services per il caricamento, sarà necessario installare Integration Services e gli adapter di destinazione Integration Services. Gli adapter sono disponibili negli strumenti client di.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="step-5-start-loading"></a><a name="Step5"></a>Passaggio 5: avviare il caricamento  
A questo punto è possibile iniziare a caricare i dati. Per altre informazioni, vedi:  
  
1.  [Strumento di caricamento da riga di comando dwloader](dwloader.md)  
  
2.  [Panoramica sul carico](load-overview.md)  
  
## <a name="performance"></a>Prestazioni  
Per ottimizzare le prestazioni in Windows Server 2012 e versioni successive, attivare l'inizializzazione immediata dei file in modo che, quando i dati vengono sovrascritti, il sistema operativo non sovrascriva i dati esistenti con zeri. Se si tratta di un rischio per la sicurezza perché i dati precedenti esistono ancora nei dischi, assicurarsi di disattivare l'inizializzazione immediata dei file.  
  
## <a name="security-notices"></a><a name="Security"></a>Avvisi sulla sicurezza  
Poiché i dati da caricare non vengono archiviati nell'appliance, il team IT è responsabile della gestione di tutti gli aspetti della sicurezza per il caricamento dei dati. Questo include ad esempio la gestione della sicurezza dei dati da caricare, la sicurezza del server usato per archiviare i carichi e la sicurezza dell'infrastruttura di rete che connette il server di caricamento al dispositivo SQL Server PDW.  
  
> [!IMPORTANT]  
> È particolarmente importante proteggere ogni server di caricamento che utilizzerà lo strumento di caricamento da riga di comando dwloader. Quando dwloader carica i dati, esegue prima l'autenticazione con il nodo di controllo e quindi, dopo aver completato l'autenticazione, sposta i dati dal server di caricamento direttamente ai nodi di calcolo sui canali di dati. La convalida del certificato non si verifica durante la mano tra ogni server di caricamento e ogni nodo di calcolo. In questo modo i nodi di calcolo vengono esposti a potenziali attacchi man-in-the-Middle su ogni canale dati durante il caricamento. Questi attacchi potrebbero comportare la divulgazione di dati e/o divulgazione di informazioni.  
  
Per ridurre i rischi di sicurezza con i dati, si consiglia quanto segue:  
  
-   Designare un account di Windows usato esclusivamente allo scopo di caricare i dati in PDW. Consentire a questo account di disporre delle autorizzazioni per il percorso di caricamento e nessun altro elemento.  
  
-   Designare un utente PDW con le autorizzazioni per caricare i dati. A seconda dei requisiti di sicurezza, è possibile avere un utente specifico per ogni database.  
  
-   Le operazioni sul server di caricamento possono accettare un percorso UNC da cui estrarre i dati dall'esterno della rete interna attendibile. E un utente malintenzionato sulla rete o la possibilità di influenzare la risoluzione dei nomi può intercettare o modificare i dati inviati al SQL Server PDW. Questa operazione presenta un rischio per la divulgazione di informazioni e manomissioni. La manomissione deve essere mitigata richiedendo l'accesso alla connessione. Per attenuare questo rischio, impostare l'opzione di criteri di gruppo seguente nelle **Opzioni sicurezza protezione\Criteri locali\Opzioni** nel server di caricamento: **client di rete Microsoft: Aggiungi firma digitale alle comunicazioni (sempre): abilitato**  
  
-   Disattivare l'inizializzazione immediata di file in Windows Server 2012 e versioni successive. Si tratta di un compromesso tra prestazioni e sicurezza, come indicato nella sezione relativa alle prestazioni. È necessario decidere qual è la scelta migliore in base ai requisiti di sicurezza.  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica di backup e ripristino](backup-and-restore-overview.md)  
  
