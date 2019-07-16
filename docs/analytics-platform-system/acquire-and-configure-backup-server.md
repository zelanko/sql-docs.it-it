---
title: Acquisire e configurare un server di backup - Parallel Data Warehouse | Microsoft Docs
description: Questo articolo descrive come configurare un sistema di Windows non appliance come un server di backup per l'uso con le funzionalità di backup e ripristino di sistema di piattaforma Analitica (AP) e Parallel Data Warehouse (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f79cb13658328927cab81bbf8d559066c5a4d5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961640"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Acquisire e configurare un server di backup per Parallel Data Warehouse
Questo articolo descrive come configurare un sistema di Windows non appliance come un server di backup per l'uso con le funzionalità di backup e ripristino di sistema di piattaforma Analitica (AP) e Parallel Data Warehouse (PDW).  
  
  
## <a name="Basics"></a>Nozioni fondamentali di server di backup  
Il server di backup:  
  
-   Viene fornita e gestita dal team IT.  
  
-   Non richiede alcun software PDW specifici o strumenti. PDW non viene installato alcun software nel server di backup.  
  
-   Si trova nel proprio rack non appliance e non può essere inserito all'interno dell'appliance APS.  
  
-   Possono essere connesse alla rete InfiniBand appliance. I backup possono essere eseguiti tramite; Ethernet o InfiniBand InfiniBand è consigliato per motivi di prestazioni.  
  
-   È nel proprio dominio del cliente, non del dominio appliance. Non vi è alcuna relazione di trust tra il dominio del cliente e il dominio di appliance.  
  
-   Ospita una condivisione file di backup, ovvero una condivisione di file di Windows che utilizza il protocollo di rete a livello di applicazione Server Message Block (SMB). Le autorizzazioni di condivisione file di backup concedere a un utente di dominio di Windows (in genere si tratta di un utente dedicato per il backup) la possibilità di eseguire il backup e ripristinare le operazioni nella condivisione. Le credenziali nome utente e password dell'utente di dominio di Windows vengono archiviate in PDW in modo che PDW può eseguire il backup e ripristinare le operazioni nella condivisione di file di backup.  
  
## <a name="Step1"></a>Passaggio 1: Determinare i requisiti di capacità  
Requisiti di sistema per il server di Backup è quasi completamente dipendono il proprio carico di lavoro. Prima di richiedere l'acquisto o il provisioning di un server di backup è necessario determinare i requisiti di capacità. Il server di Backup non deve essere dedicata solo ai backup, purché lo gestirà i requisiti di archiviazione e le prestazioni del carico di lavoro. È anche possibile avere più server di backup per backup e ripristino di ogni database a uno dei diversi server.  
  
Usare la [Backup server capacità pianificazione foglio di lavoro](backup-capacity-planning-worksheet.md) per determinare i requisiti di capacità.  
  
## <a name="Step2"></a>Passaggio 2: Acquisire il server di backup  
Ora che meglio comprendere i requisiti di capacità, è possibile pianificare i server e componenti di rete che sarà necessario acquistare o effettuare il provisioning. Incorporare il seguente elenco di requisiti nel piano di acquisto e quindi acquistare il server o effettuare il provisioning di un server esistente.  
  
### <a name="software-requirements"></a>Requisiti software  
Qualsiasi file server che usa il protocollo di condivisione File di Windows (SMB).  
  
Si consiglia di Windows Server 2012 o oltre al fine di:  
  
-   Ottenere il miglioramento delle prestazioni di preallocazione dei file tramite SMB.  
  
-   Usare immediata dei File di inizializzazione immediata per operazioni di backup. Il team IT gestisce questa impostazione nel server di backup. Gestione configurazione PDW (dwconfig.exe) non impostata o control inizializzazione immediata dei file per il server di backup. Le versioni precedenti di Windows non è immediata, ma possono comunque essere utilizzate come server di backup.  
  
### <a name="networking-requirements"></a>Requisiti di rete  
Sebbene non obbligatorio, InfiniBand è il tipo di connessione consigliato per i server di Backup. Per preparare per la connessione server di caricamento per la rete InfiniBand di appliance:  
  
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
  
5.  Configurare le impostazioni per le schede di rete InfiniBand e DNS. Per istruzioni sulla configurazione, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Passaggio 4: Configurare la condivisione file di backup  
PDW potranno accedere il server di backup tramite una condivisione file UNC. Per configurare la condivisione file:  
  
1.  Creare una cartella nel server di backup per l'archiviazione dei backup.  
  
2.  Creare una condivisione file, chiamata di una condivisione di backup, per la cartella di backup.  
  
3.  Definire o creare un account di dominio Windows nel dominio dei clienti che si desidera utilizzare ai fini dell'esecuzione di backup e ripristini. Per motivi di sicurezza, è consigliabile usare un account dedicato come l'utente di backup.  
  
4.  Aggiungere le autorizzazioni per il backup condividano in modo che possa accedere solo gli account attendibili e un account di backup del dominio, lettura e scrivere nel percorso di condivisione.  
  
5.  Aggiungere le credenziali dell'account di dominio di backup in PDW.  
  
    Ad esempio:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Per altre informazioni, vedere queste stored procedure:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Passaggio 5: Avviare il backup dei dati  
A questo punto si è pronti avviare il backup dei dati per il server di backup.  
  
Eseguire il backup dei dati, utilizzare un client di query per connettersi a SQL Server PDW e quindi inviare BACKUP DATABASE o RESTORE DATABASE i comandi. Usare il disco = clausola per specificare il percorso di backup e server di Backup.  
  
> [!IMPORTANT]  
> Ricordarsi di usare l'indirizzo IP InfiniBand del server di backup. In caso contrario, verranno copiati i dati su Ethernet anziché InfiniBand.  
  
Ad esempio:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Per altre informazioni, vedere: 
  
-   [BACKUP DEL DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Avvisi di sicurezza  
Il server di backup non è aggiunto al dominio privato dell'Appliance. È nella propria rete e senza alcuna relazione di trust tra il proprio dominio e private appliance.  
  
Poiché i backup PDW non vengono archiviati nell'appliance, il tuo team IT è responsabile per la gestione di tutti gli aspetti della sicurezza dei backup. Ad esempio, ciò include la gestione della protezione dei dati di backup, la sicurezza del server utilizzato per archiviare i backup e la sicurezza dell'infrastruttura di rete che si connette il server di backup per l'appliance APS.  
  
### <a name="manage-network-credentials"></a>Gestire le credenziali di rete  
  
L'accesso di rete alla directory di backup è basato sulla sicurezza di condivisione dei file di Windows standard. Prima di eseguire un backup, è necessario creare o designare un account di Windows che verrà usato per l'autenticazione di PDW per la directory di backup. L'account di Windows deve avere le autorizzazioni per accedere, creare e scrivere nella directory di backup.  
  
> [!IMPORTANT]  
> Per ridurre i rischi di sicurezza dei dati, è consigliabile impostare un account di Windows dedicato esclusivamente all'esecuzione delle operazioni di backup e ripristino. Concedere all'account le autorizzazioni solo per il percorso di backup.  
  
Per archiviare il nome utente e la password in PDW, utilizzare il [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) stored procedure. PDW Usa Gestione credenziali di Windows per archiviare e crittografare i nomi utente e password nel nodo di controllo e nodi di calcolo. Con il comando BACKUP DATABASE non viene eseguito il backup delle credenziali.  
  
Per rimuovere le credenziali di rete da PDW, utilizzare il [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) stored procedure.  
  
Per elencare tutte le credenziali di rete archiviate in SQL Server PDW, utilizzare il [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) vista a gestione dinamica.  
  
### <a name="secure-communications"></a>Proteggere le comunicazioni  
  
Operazioni nel server durante il caricamento è possono usare un percorso UNC per estrarre i dati dall'esterno della rete interna attendibile. Un utente malintenzionato sulla rete o con grado di influenzare la risoluzione dei nomi può intercettare o modificare i dati inviati a di PDW. Ciò comporta un rischio di divulgazione manomissioni e informazioni. Per aiutare a ridurre il rischio di manomissione:

- Richiedere la firma per la connessione. 
- Nel server durante il caricamento, impostare l'opzione di criteri di gruppo seguente in protezione\Criteri Locali\opzioni di sicurezza:  Client di rete Microsoft: Firma digitale alle comunicazioni (sempre): Abilitata.  
  
## <a name="see-also"></a>Vedere anche  
[Backup e ripristino](backup-and-restore-overview.md)  
  
