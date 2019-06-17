---
title: Opzioni di configurazione del server Server Memory | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4447d7df594e9542982d6ba05de05f42b0628a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810064"
---
# <a name="server-memory-server-configuration-options"></a>Opzioni di configurazione del server Server Memory
  Usare le due opzioni per la memoria del server **min server memory** e **max server memory**per riconfigurare la quantità di memoria, in megabyte, gestita con Gestione memoria di SQL Server per un processo di SQL Server usato da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 L'impostazione predefinita per **min server memory** è 0, mentre quella per **max server memory** è 2147483647 MB. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i requisiti di memoria possono variare dinamicamente in base alle risorse di sistema disponibili.  
  
> [!NOTE]  
>  L'impostazione di **max server memory** sul valore minimo provoca un grave peggioramento delle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fino a impedirne l'avvio. Se non è possibile avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dopo la modifica di questa opzione, eseguire l'avvio con l'opzione di avvio **-f** e reimpostare **max server memory** sul valore precedente. Per altre informazioni, vedere [Opzioni di avvio del servizio del motore di database](database-engine-service-startup-options.md).  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza la memoria in modo dinamico, esegue query periodiche sul sistema per determinare la quantità di memoria libera disponibile. Il mantenimento di tale memoria libera impedisce il paging del sistema operativo. Se è disponibile una quantità minore di memoria libera, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rilascia memoria al sistema operativo. Se è disponibile una quantità maggiore di memoria libera, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere allocata più memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aggiunge memoria solo se richiesto dal relativo carico di lavoro. In un server non operativo non vengono aumentate le dimensioni del proprio spazio degli indirizzi virtuali.  
  
 Vedere l'esempio B per una query che restituisce la memoria usata attualmente. **max server memory** controlla l'allocazione di memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , compresi il pool di buffer, la memoria per la compilazione, tutte le cache, le concessioni di memoria qe, la memoria per la gestione blocchi e la memoria clr (in particolare i clerk di memoria presenti in **sys.dm_os_memory_clerks**). La memoria per gli stack di thread, gli heap di memoria, i provider di server collegati diversi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e la memoria allocata da una DLL non di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono controllati da max server memory.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa l'API di notifica di memoria **QueryMemoryResourceNotification** per determinare i casi in cui è possibile allocare e rilasciare memoria con Gestione memoria di SQL Server.  
  
 È consigliabile consentire a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di usare la memoria in modo dinamico. È possibile, tuttavia, impostare manualmente le opzioni per la memoria e limitare la quantità di memoria a cui può accedere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Prima di impostare la quantità di memoria per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determinare l'impostazione appropriata per la memoria sottraendo dalla memoria fisica totale la memoria necessaria per il sistema operativo e per qualsiasi altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nonché per eventuali altri utilizzi del sistema se il computer non è completamente dedicato a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La differenza così ottenuta rappresenta la quantità di memoria massima assegnabile a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="setting-the-memory-options-manually"></a>Impostazione manuale delle opzioni per la memoria  
 Impostare **min server memory** e **max server memory** per estendere l'intervallo di valori di memoria. Questo metodo è utile per gli amministratori di sistema o di database che desiderano configurare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insieme ai requisiti di memoria di altre applicazioni eseguite nello stesso computer.  
  
 Usare **min server memory** per garantire una quantità minima di memoria disponibile per Gestione memoria di SQL Server per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non alloca immediatamente la quantità di memoria specificata in **min server memory** all'avvio. Se, tuttavia, l'utilizzo della memoria raggiunge tale valore a causa del carico di lavoro del client, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può liberare memoria solo se si riduce il valore di **min server memory** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esegue necessariamente l'allocazione della quantità di memoria specificata in **min server memory**. Se il carico sul server non richiede mai l'allocazione della quantità di memoria specificata in **min server memory**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà eseguito con una quantità di memoria inferiore.  
  
|Tipo di sistema operativo|Consentita quantità di memoria minima per **numero massimo di memoria del server**|  
|-------------|----------------------------------------------------------------|  
|32 bit|64 MB|  
|64 bit|128 MB|  
  
## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>Come configurare le opzioni per la memoria tramite SQL Server Management Studio  
 Usare le due opzioni per la memoria del server **min server memory** e **max server memory**per riconfigurare la quantità di memoria, in megabyte, gestita tramite Gestione memoria di SQL Server per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i requisiti di memoria possono variare dinamicamente in base alle risorse di sistema disponibili.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>Procedura per la configurazione di una quantità di memoria fissa  
 **Per impostare una quantità fissa di memoria:**  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Memoria** .  
  
3.  In **Opzioni per la memoria del server**immettere la quantità da usare per **Memoria minima per il server** e **Memoria massima per il server**.  
  
     Usare le impostazioni predefinite per consentire a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di modificare i requisiti di memoria in base alle risorse di sistema disponibili. L'impostazione predefinita per **min server memory** è 0, mentre quella per **max server memory** è 2147483647 MB.  
  
## <a name="maximize-data-throughput-for-network-applications"></a>Ottimizzare la velocità effettiva dei dati per applicazioni di rete  
 Per ottimizzare l'utilizzo della memoria di sistema per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario limitare la quantità di memoria usata dal sistema per la memorizzazione dei file nella cache. Per limitare la cache del file system, assicurarsi che l'opzione **Massimizza la velocità di trasmissione dati per condivisione file** non sia selezionata. Per specificare la quantità minima di cache del file system, è possibile selezionare **Minimizza la quantità di memoria usata** o **Bilanciamento**.  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>Per controllare l'impostazione corrente nel sistema operativo  
  
1.  Fare clic su **Start**, scegliere **Pannello di controllo**, fare doppio clic su **Connessioni di rete**, quindi su **Connessione alla rete locale (LAN)** .  
  
2.  Nella scheda **Generale** fare clic su **Proprietà**, selezionare l'opzione **Condivisione file e stampanti per reti Microsoft**e quindi scegliere **Proprietà**.  
  
3.  Se l'opzione **Massimizza la velocità di trasmissione dati per le applicazioni di rete** è selezionata, scegliere un'altra opzione, fare clic su **OK**, quindi chiudere tutte le finestre di dialogo rimanenti.  
  
## <a name="lock-pages-in-memory"></a>Blocco di pagine in memoria  
 Questi criteri di Windows determinano gli account autorizzati a usare un processo per mantenere i dati nella memoria fisica, impedendo al sistema di eseguire il paging dei dati nella memoria virtuale su disco. Il blocco delle pagine in memoria può garantire il corretto funzionamento del server quando si verifica il paging della memoria su disco. SQL Server **Lock Pages in Memory** opzione è impostata su ON nelle istanze a 32 e 64 bit di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard edition ed edizioni superiori quando l'account con privilegi per eseguire sqlservr.exe dispone di Windows "Locked pagine in Diritto utente di memoria (LPIM). In versioni precedenti di SQL Server, l'impostazione dell'opzione Blocco pagine per un'istanza a 32 bit di SQL Server richiede che l'account con i privilegi per eseguire sqlservr.exe disponga del diritto utente LPIM e che l'opzione "awe_enabled"sia impostata su ON.  
  
 Per disabilitare il **Lock Pages In Memory** opzione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], rimuovere l'utente "Blocco di pagine in memoria" a destra per l'account di avvio di SQL Server.  
  
### <a name="to-disable-lock-pages-in-memory"></a>Per disabilitare l'opzione Blocco di pagine in memoria  
 **Per disabilitare il lock pages in memory-opzione:**  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**. Nel **aperto** , digitare `gpedit.msc`.  
  
     Viene visualizzata la finestra di dialogo **Criteri gruppo** .  
  
2.  Nella console **Criteri di gruppo** espandere **Configurazione computer**e quindi espandere **Impostazioni di Windows**.  
  
3.  Espandere **Impostazioni sicurezza**e quindi espandere **Criteri locali**.  
  
4.  Selezionare la cartella **Assegnazione diritti utente** .  
  
     I criteri verranno visualizzati nel riquadro dei dettagli.  
  
5.  Nel riquadro fare doppio clic su **Blocco di pagine in memoria**.  
  
6.  Nella finestra di dialogo **Impostazioni criteri di sicurezza locali** selezionare l'account con i privilegi per eseguire sqlservr.exe e fare clic su **Rimuovi**.  
  
## <a name="virtual-memory-manager"></a>Virtual Memory Manager  
 I sistemi operativi a 32 bit consentono di accedere a 4 GB di spazio degli indirizzi virtuali. 2 GB di memoria virtuale sono riservati a singoli processi e disponibili per l'utilizzo da parte delle applicazioni. 2 GB sono riservati all'utilizzo da parte del sistema operativo. In tutte le edizioni del sistema operativo è disponibile un'opzione che consente alle applicazioni di accedere a un massimo di 3 GB di spazio degli indirizzi virtuali, limitando il sistema operativo a 1 GB. Per altre informazioni su come usare l'opzione di configurazione della memoria, vedere la documentazione di Windows sull'ottimizzazione a 4 gigabyte. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 32 bit viene eseguito in un sistema operativo a 64 bit, lo spazio degli indirizzi virtuali disponibile per gli utenti corrisponde a tutti i 4 GB.  
  
 Viene eseguito il mapping delle aree di cui è stato eseguito il commit dello spazio degli indirizzi alla memoria fisica disponibile tramite Virtual Memory Manager (VMM) di Windows.  
  
 Per altre informazioni sulla quantità di memoria fisica supportata dai diversi sistemi operativi, vedere la documentazione di Windows relativa ai limiti di memoria per le versioni di Windows.  
  
 I sistemi con memoria virtuale consentono il commit in eccesso della memoria fisica, per cui il rapporto tra memoria virtuale e memoria fisica può essere maggiore di 1:1. Di conseguenza, i computer con diverse configurazioni di memoria fisica consentono l'esecuzione di programmi di dimensioni elevate. Tuttavia l'utilizzo di una quantità di memoria virtuale di molto superiore alla combinazione dei set di lavoro medi per tutti i processi determina un peggioramento delle prestazioni.  
  
 **min server memory** e **max server memory** sono opzioni avanzate. Se si utilizza la stored procedure di sistema **sp_configure** per modificare queste impostazioni, è possibile modificarle solo se il valore di **show advanced options** è impostato su 1. Queste impostazioni diventano effettive immediatamente e non richiedono il riavvio del server.  
  
## <a name="running-multiple-instances-of-sql-server"></a>Esecuzione di più istanze di SQL Server  
 Quando si eseguono più istanze di [!INCLUDE[ssDE](../../includes/ssde-md.md)], è possibile gestire la memoria in tre modi:  
  
-   Controllare l'utilizzo di memoria usando **max server memory** . Stabilire le impostazioni massime per ogni istanza, accertandosi che il totale non sia superiore alla memoria fisica disponibile sul computer. È possibile rendere la memoria di ogni istanza proporzionale al relativo carico di lavoro previsto o alle dimensioni del database. Questo approccio presenta il vantaggio di rendere la memoria libera immediatamente disponibile ad ogni nuovo processo o istanza. Lo svantaggio è che se non vengono eseguite tutte le istanze, parte della memoria resterà inusata.  
  
-   Controllare l'utilizzo di memoria usando **min server memory** . Stabilire le impostazioni minime per ogni istanza, in modo che la somma di tali minimi sia 1-2 GB inferiore alla memoria fisica totale del computer. Anche questi minimi possono essere resi proporzionali al carico previsto dell'istanza. Con questo approccio, quando non vengono eseguite tutte le istanze contemporaneamente, quelle in esecuzione potranno usare la memoria libera rimanente. Questo approccio consente inoltre di riservare a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una quantità ragionevole di memoria quando sullo stesso computer vengono eseguiti anche altri processi particolarmente onerosi. Lo svantaggio è che quando vengono avviati una nuova istanza o altri processi, le istanze eseguite rilasceranno la memoria con un certo ritardo, in particolare quando a tale scopo dovranno riscrivere le pagine modificate nei rispettivi database.  
  
-   Non intervenire in alcun modo (non consigliato). Le prime istanze sottoposte a carico di lavoro tenderanno ad allocare tutta la memoria. Alle istanze inattive o a quelle avviate in un secondo momento verrà destinata solo una minima quantità di memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene ripartita in alcun modo la memoria tra le diverse istanze. Tutte le istanze, tuttavia, risponderanno ai segnali di Windows Memory Notification correggendo di conseguenza le dimensioni dei rispettivi footprint di memoria. In Windows la memoria non viene bilanciata tra le applicazioni tramite l'API di Windows Memory Notification. Offre invece un semplice feedback globale sulla disponibilità di memoria nel sistema.  
  
 Poiché è possibile modificare queste impostazioni senza riavviare le istanze, sarà possibile provare agevolmente valori diversi fino a individuare quelli più adatti alle esigenze.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>Assegnazione della quantità massima di memoria a SQL Server  
  
||32 bit|64 bit|  
|-|-------------|-------------|  
|Memoria convenzionale|In tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fino al limite dello spazio degli indirizzi virtuali di processo:<br /><br /> 2 GB<br /><br /> 3 GB con **3 gb** avvio parametro *<br /><br /> 4 GB su WOW64\*\*|In tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fino al limite dello spazio degli indirizzi virtuali di processo:<br /><br /> 8 TB in sistemi con architettura x64|  
  
 * **/3gb** è un parametro di avvio del sistema operativo. Per altre informazioni, consultare [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
 \* * WOW64 (Windows on Windows 64) è una modalità che 32 bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito in un sistema operativo a 64 bit. Per altre informazioni, consultare [MSDN Library](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
## <a name="examples"></a>Esempi  
  
### <a name="example-a"></a>Esempio A  
 Nell'esempio seguente viene impostata l'opzione `max server memory` su 4 GB.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>Esempio B: Determinazione dell'allocazione di memoria corrente  
 La query seguente restituisce le informazioni sulla memoria attualmente allocata.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
