---
title: Acquisisci & configurare il server di backup
description: Questo articolo descrive come configurare un sistema Windows non Appliance come server di backup per l'uso con le funzionalità di backup e ripristino in Analytics Platform System (APS) e Parallel data warehouse (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b1d817bae593d4083f3e4873d626e147e58d5c28
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767160"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Acquisire e configurare un server di backup per data warehouse paralleli
Questo articolo descrive come configurare un sistema Windows non Appliance come server di backup per l'uso con le funzionalità di backup e ripristino in Analytics Platform System (APS) e Parallel data warehouse (PDW).  
  
  
## <a name="backup-server-basics"></a><a name="Basics"></a>Nozioni fondamentali sul server di backup  
Server di backup:  
  
-   Viene fornito e gestito dal team IT.  
  
-   Non richiede software o strumenti specifici di PDW. PDW non installa alcun software nel server di backup.  
  
-   Si trova nel proprio rack non Appliance e non può essere inserito all'interno del dispositivo APS.  
  
-   Può essere connesso alla rete InfiniBand dell'appliance. I backup possono essere eseguiti su InfiniBand o Ethernet; InfiniBand è consigliato per motivi di prestazioni.  
  
-   Si trova nel dominio del cliente, non nel dominio dell'appliance. Non esiste alcuna relazione di trust tra il dominio del cliente e il dominio dell'appliance.  
  
-   Ospita una condivisione file di backup, ovvero una condivisione file di Windows che usa il protocollo di rete a livello di applicazione SMB (Server Message Block). Le autorizzazioni per la condivisione file di backup assegnano a un utente di dominio di Windows (in genere si tratta di un utente di backup dedicato) la possibilità di eseguire operazioni di backup e ripristino sulla condivisione. Le credenziali del nome utente e della password dell'utente di dominio Windows sono archiviate in PDW, in modo che PDW possa eseguire operazioni di backup e ripristino nella condivisione file di backup.  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>Passaggio 1: determinare i requisiti di capacità  
I requisiti di sistema per il server di backup dipendono quasi completamente dal proprio carico di lavoro. Prima di acquistare o effettuare il provisioning di un server di backup, è necessario determinare i requisiti di capacità. Non è necessario che il server di backup sia dedicato solo ai backup, purché vengano gestiti i requisiti di prestazioni e archiviazione del carico di lavoro. È inoltre possibile disporre di più server di backup per eseguire il backup e il ripristino di ogni database in uno dei diversi server.  
  
Utilizzare il [foglio](backup-capacity-planning-worksheet.md) di lavoro per la pianificazione della capacità del server di backup per determinare i requisiti di capacità.  
  
## <a name="step-2-acquire-the-backup-server"></a><a name="Step2"></a>Passaggio 2: acquisire il server di backup  
Ora che è possibile comprendere meglio i requisiti di capacità, è possibile pianificare i server e i componenti di rete che sarà necessario acquistare o effettuare il provisioning. Incorporare l'elenco di requisiti seguente nel piano di acquisto, quindi acquistare il server o effettuare il provisioning di un server esistente.  
  
### <a name="software-requirements"></a>Requisiti software  
Qualsiasi file server che utilizza il protocollo SMB (Windows file sharing).  
  
È consigliabile Windows Server 2012 o versioni successive per:  
  
-   Ottenere il vantaggio in merito alle prestazioni della pre-allocazione dei file su SMB.  
  
-   Usare l'inizializzazione immediata dei file per le operazioni di backup. Il team IT gestisce questa impostazione nel server di backup. Il Configuration Manager PDW (dwconfig.exe) non imposta o controlla l'uso di IFI nel server di backup. Le versioni precedenti di Windows non dispongono di IFI, ma possono comunque essere utilizzate come server di backup.  
  
### <a name="networking-requirements"></a>Requisiti di rete  
Sebbene non sia obbligatorio, InfiniBand è il tipo di connessione consigliato per i server di backup. Per preparare la connessione del server di caricamento alla rete InfiniBand dell'appliance:  
  
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
  
## <a name="step-4-configure-the-backup-file-share"></a><a name="Step4"></a>Passaggio 4: configurare la condivisione file di backup  
PDW effettuerà l'accesso al server di backup tramite una condivisione file UNC. Per configurare la condivisione file:  
  
1.  Creare una cartella nel server di backup per l'archiviazione dei backup.  
  
2.  Creare una condivisione file, denominata condivisione di backup, per la cartella di backup.  
  
3.  Designare o creare un account di dominio di Windows nel dominio del cliente che si desidera utilizzare ai fini dell'esecuzione di backup e ripristini. Per motivi di sicurezza, è preferibile usare un account dedicato come utente di backup.  
  
4.  Aggiungere autorizzazioni alla condivisione di backup in modo che solo gli account attendibili e un account di backup di dominio possano accedere, leggere e scrivere nel percorso di condivisione.  
  
5.  Aggiungere le credenziali dell'account di dominio di backup a PDW.  
  
    Ad esempio:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Per ulteriori informazioni, vedere le stored procedure seguenti:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="step-5-start-backing-up-your-data"></a><a name="Step5"></a>Passaggio 5: iniziare a eseguire il backup dei dati  
A questo punto è possibile iniziare a eseguire il backup dei dati nel server di backup.  
  
Per eseguire il backup dei dati, utilizzare un client di query per connettersi a SQL Server PDW e quindi inviare i comandi BACKUP database o RESTOre DATABASE. Utilizzare la clausola DISK = per specificare il server di backup e il percorso di backup.  
  
> [!IMPORTANT]  
> Ricordarsi di usare l'indirizzo IP InfiniBand del server di backup. In caso contrario, i dati verranno copiati tramite Ethernet anziché InfiniBand.  
  
Ad esempio:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Per altre informazioni, vedere: 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)   
  
-   [RIPRISTINA DATABASE](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016)  
  
## <a name="security-notices"></a><a name="Security"></a>Avvisi sulla sicurezza  
Il server di backup non è stato aggiunto al dominio privato per l'appliance. Si trova nella propria rete e non esiste alcuna relazione di trust tra il dominio e il dominio Appliance privato.  
  
Poiché i backup PDW non sono archiviati nell'appliance, il team IT è responsabile della gestione di tutti gli aspetti della sicurezza del backup. Questo include ad esempio la gestione della sicurezza dei dati di backup, la sicurezza del server usato per archiviare i backup e la sicurezza dell'infrastruttura di rete che connette il server di backup al dispositivo APS.  
  
### <a name="manage-network-credentials"></a>Gestire le credenziali di rete  
  
L'accesso di rete alla directory di backup è basato sulla sicurezza di condivisione dei file di Windows standard. Prima di eseguire un backup, è necessario creare o designare un account di Windows che verrà usato per l'autenticazione di PDW nella directory di backup. L'account di Windows deve avere le autorizzazioni per accedere, creare e scrivere nella directory di backup.  
  
> [!IMPORTANT]  
> Per ridurre i rischi di sicurezza dei dati, è consigliabile impostare un account di Windows dedicato esclusivamente all'esecuzione delle operazioni di backup e ripristino. Concedere all'account le autorizzazioni solo per il percorso di backup.  
  
Per archiviare il nome utente e la password in PDW, usare il [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) stored procedure. PDW usa Gestione credenziali di Windows per archiviare e crittografare i nomi utente e le password nel nodo di controllo e nei nodi di calcolo. Con il comando BACKUP DATABASE non viene eseguito il backup delle credenziali.  
  
Per rimuovere le credenziali di rete da PDW, usare il stored procedure [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) .  
  
Per elencare tutte le credenziali di rete archiviate in SQL Server PDW, utilizzare la vista a gestione dinamica [sys. dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) .  
  
### <a name="secure-communications"></a>Comunicazioni sicure  
  
Le operazioni sul server di caricamento possono usare un percorso UNC per estrarre i dati dall'esterno della rete interna attendibile. Un utente malintenzionato sulla rete o la possibilità di influenzare la risoluzione dei nomi può intercettare o modificare i dati inviati al PDW. Questa operazione presenta un rischio per la divulgazione di informazioni e manomissioni. Per ridurre il rischio di manomissione:

- Richiedere l'accesso alla connessione. 
- Nel server di caricamento, impostare l'opzione di criteri di gruppo seguente in Security protezione\Criteri locali\Opzioni Options: Microsoft Network client: Digitally sign Communications (always): Enabled.  
  
## <a name="see-also"></a>Vedere anche  
[Backup e ripristino](backup-and-restore-overview.md)  
