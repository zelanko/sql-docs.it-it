---
title: Procedure consigliate per le prestazioni per SQL Server in Linux
description: Questo articolo illustra le procedure consigliate per le prestazioni e le linee guida per l'esecuzione di SQL Server in Linux.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 12/11/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 89b8a7c087fb87ed911be640126ec81021b045a7
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323508"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Procedure consigliate per le prestazioni e linee guida per la configurazione per SQL Server in Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Questo articolo fornisce procedure consigliate e suggerimenti per ottimizzare le prestazioni per le applicazioni di database che si connettono a SQL Server in Linux. Questi suggerimenti sono specifici per l'esecuzione nella piattaforma Linux. Tutte i normali suggerimenti per SQL Server, ad esempio la progettazione degli indici, sono comunque validi.

Le linee guida seguenti contengono suggerimenti per la configurazione sia di SQL Server che del sistema operativo Linux.

## <a name="linux-os-configuration"></a>Configurazione del sistema operativo Linux

Provare a usare le impostazioni di configurazione del sistema operativo Linux seguenti per ottenere prestazioni ottimali per un'installazione di SQL Server.

### <a name="storage-configuration-recommendation"></a>Raccomandazione sulla configurazione dello spazio di archiviazione

#### <a name="use-storage-subsystem-with-appropriate-iops-throughput-and-redundancy"></a>Usare il sottosistema di archiviazione con i valori appropriati per operazioni di I/O al secondo, velocità effettiva e ridondanza

Il sottosistema di archiviazione che ospita dati, log delle transazioni e altri file associati (ad esempio, i file di checkpoint per OLTP in memoria) deve riuscire a gestire il carico di lavoro medio e di picco in modo normale. Negli ambienti locali il fornitore dello spazio di archiviazione supporta in genere la configurazione hardware RAID appropriata con striping su più dischi per garantire i valori appropriati di operazioni di I/O al secondo, velocità effettiva e ridondanza. Questa configurazione può tuttavia variare a seconda del fornitore e dell'offerta di spazio di archiviazione in base alle diverse architetture.

Per SQL Server in Linux distribuito in Macchine virtuali di Azure, valutare l'opportunità di usare RAID software per assicurarsi che vengano soddisfatti i requisiti di operazioni di I/O al secondo e velocità effettiva appropriati. Quando si configura SQL Server in Macchine virtuali di Azure, vedere l'articolo seguente per considerazioni simili sull'archiviazione: [Configurazione dell'archiviazione per le VM di SQL Server](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/storage-configuration)

Il seguente è un esempio di come creare RAID software in Linux in Macchine virtuali di Azure. Di seguito è riportato un esempio, ma è consigliabile usare il numero appropriato di dischi dati per la velocità effettiva e le operazioni di I/O al secondo necessarie per i volumi in base ai requisiti relativi ai dati, al log delle transazioni e alle operazioni di I/O di tempdb. In questo esempio otto dischi dati sono stati collegati alla macchina virtuale di Azure: quattro ai file di dati dell'host, due per i log delle transazioni e due per il carico di lavoro tempdb.

```bash
# To locate the devices (for example /dev/sdc) for RAID creation, use the lsblk command
# For Data volume, using 4 devices, in RAID 5 configuration with 8KB stripes
mdadm --create --verbose /dev/md0 --level=raid5 --chunk=8K --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf

# For Log volume, using 2 devices in RAID 10 configuration with 64KB stripes
mdadm --create --verbose /dev/md1 --level=raid10 --chunk=64K --raid-devices=2 /dev/sdg /dev/sdh

# For tempdb volume, using 2 devices in RAID 0 configuration with 64KB stripes
mdadm --create --verbose /dev/md2 --level=raid0 --chunk=64K --raid-devices=2 /dev/sdi /dev/sdj
```

#### <a name="file-system-configuration-recommendation"></a>Raccomandazione sulla configurazione del file system

SQL Server supporta i file system EXT4 e XFS per ospitare il database, i log delle transazioni e i file aggiuntivi, ad esempio i file di checkpoint per OLTP in memoria in SQL Server. Microsoft consiglia di usare il file system XFS per ospitare i file di dati e di log delle transazioni di SQL Server.

```bash
# Formatting the volume with XFS filesystem
mkfs.xfs /dev/md0 -f -L datavolume
mkfs.xfs /dev/md1 -f -L logvolume
mkfs.xfs /dev/md2 -f -L tempdb
```

> [!NOTE]
> È possibile configurare il file system XFS in modo che non venga fatta distinzione tra maiuscole e minuscole durante la creazione e la formattazione del volume XFS. Non è la configurazione più usata nell'ecosistema Linux, ma può essere usata per motivi di compatibilità.
>
> Esempio: mkfs.xfs /dev/md0 -f -n version=ci -L datavolume
>
> Nell'esempio vengono usati i parametri `-n version=ci` per configurare il file system XFS in modo che non venga fatta distinzione tra maiuscole e minuscole.

##### <a name="persistent-memory-filesystem-recommendation"></a>Raccomandazione sul filesystem PMEM

Per la configurazione del file system nei dispositivi PMEM, l'allocazione dei blocchi per il file system sottostante deve essere pari a 2 MB. Per altre informazioni su questo argomento, vedere l'articolo [Considerazioni tecniche](sql-server-linux-configure-pmem.md#technical-considerations).

#### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Disabilitare la data e ora dell'ultimo accesso nei file system per i file di dati e di log di SQL Server

Per assicurarsi che le unità collegate al sistema vengano rimontate automaticamente dopo un riavvio, è necessario aggiungerle al file `/etc/fstab`. È anche consigliabile che l'UUID (Universally Unique IDentifier) usato in `/etc/fstab` faccia riferimento all'unità invece che al solo nome del dispositivo, ad esempio `/dev/sdc1`.

L'uso dell'attributo **noatime** con qualsiasi file system usato per archiviare i file di dati e di log di SQL Server è vivamente consigliato. Per informazioni su come impostare questo attributo, vedere la documentazione di Linux. Di seguito è riportato un esempio di come abilitare l'opzione **noatime** per un volume montato nella macchina virtuale di Azure.

Voce del punto di montaggio in **_/etc/fstab_* _

```bash
UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" /data1 xfs,rw,attr2,noatime 0 0
```

Nell'esempio precedente UUID rappresenta il dispositivo che è possibile trovare usando il comando _*_blkid_*_.

#### <a name="sql-server-and-forced-unit-access-fua-io-subsystem-capability"></a>SQL Server e funzionalità del sottosistema di I/O FUA (Forced Unit Access)

Alcune versioni di distribuzioni Linux supportate forniscono supporto per la funzionalità del sottosistema di I/O FUA per garantire la durabilità dei dati. SQL Server usa la funzionalità FUA per garantire operazioni di I/O estremamente efficienti e affidabili per il carico di lavoro di SQL Server. Per altre informazioni sul supporto di FUA nella distribuzione Linux e sull'impatto per SQL Server, vedere il blog seguente: [SQL Server On Linux: Forced Unit Access (FUA) Internals](https://bobsql.com/sql-server-on-linux-forced-unit-access-fua-internals/) (SQL Server in Linux: elementi interni di FUA - Forced Unit Access)

SUSE Linux Enterprise Server 12 SP5 e Red Hat Enterprise Linux 8.0 e versioni successive supportano la funzionalità FUA nel sottosistema di I/O. Se si usa SQL Server 2017 CU6 e versioni successive o SQL Server 2019, è consigliabile usare la configurazione seguente per un'implementazione a prestazioni elevate ed efficiente dell'input/output con FUA tramite SQL Server.

Usare la configurazione consigliata riportata di seguito se sono soddisfatte le condizioni seguenti.

- Uso di SQL Server 2017 CU6 o versione successiva oppure di SQL Server 2019
- Uso di una distribuzione e una versione di Linux che supportano la funzionalità FUA (Red Hat Enterprise Linux 8.0 o versione successiva oppure SUSE Linux Enterprise Server 12 SP5)
- Sottosistema di archiviazione e/o hardware che supporta ed è configurato per la funzionalità FUA

Configurazione consigliata:

1. Abilitare il flag di traccia 3979 come parametro di avvio
2. Usare _ *mssql-conf** per configurare `control.writethrough = 1` e `control.alternatewritethrough = 0`

Per quasi tutte le altre configurazioni che non soddisfano le condizioni precedenti, la configurazione consigliata è la seguente:

1. Abilitare il flag di traccia 3982 come parametro di avvio (impostazione predefinita per SQL Server nell'ecosistema Linux), assicurandosi al contempo che il flag di traccia 3979 non sia abilitato come parametro di avvio
2. Usare **mssql-conf** per configurare `control.writethrough = 1` e `control.alternatewritethrough = 1`

### <a name="kernel-and-cpu-settings-for-high-performance"></a>Impostazioni del kernel e della CPU per prestazioni elevate

La sezione seguente descrive le impostazioni consigliate per il sistema operativo Linux per ottenere prestazioni e velocità effettiva elevate per un'installazione di SQL Server. Per il processo di configurazione di queste impostazioni, vedere la documentazione del sistema operativo Linux. L'uso di [**_Tuned_* _](https://tuned-project.org) indicato consente di configurare diverse configurazioni delle CPU e del kernel descritte di seguito.

#### <a name="using-__tuned__-to-configure-kernel-settings"></a>Uso di _*_Tuned_*_ per configurare le impostazioni del kernel

Per gli utenti di Red Hat Enterprise Linux (RHEL), il profilo delle prestazioni della velocità effettiva di [Tuned](https://tuned-project.org) configurerà automaticamente alcune impostazioni del kernel e della CPU (tranne C-States). A partire da RHEL 8.0, è stato sviluppato in collaborazione con Red Hat un profilo di _*_Tuned_*_ denominato _ *mssql**, che offre ottimizzazioni più dettagliate correlate alle prestazioni di Linux per i carichi di lavoro di SQL Server. Questo profilo include il profilo di prestazioni per la velocità effettiva RHEL e le definizioni sono presentate di seguito per poterle confrontare con altre distribuzioni di Linux e versioni di RHEL senza questo profilo.

Per SUSE Linux Enterprise Server 12 SP5, Ubuntu 18.04 e Red Hat Enterprise Linux 7.x, il pacchetto **_Tuned_ *_ può essere installato manualmente. Può essere usato per creare e configurare il profilo _* mssql** descritto di seguito.

##### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Impostazioni di Linux proposte con un profilo mssql di Tuned

```bash
#
# A Tuned configuration for SQL Server on Linux
#

[main]
summary=Optimize for Microsoft SQL Server
include=throughput-performance

[cpu]
force_latency=5

[sysctl]
vm.swappiness = 1
vm.dirty_background_ratio = 3
vm.dirty_ratio = 80
vm.dirty_expire_centisecs = 500
vm.dirty_writeback_centisecs = 100
vm.transparent_hugepages=always
# For multi-instance SQL deployments, use
# vm.transparent_hugepages=madvise
vm.max_map_count=1600000
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
kernel.numa_balancing=0
kernel.sched_latency_ns = 60000000
kernel.sched_migration_cost_ns = 500000
kernel.sched_min_granularity_ns = 15000000
kernel.sched_wakeup_granularity_ns = 2000000
```

Per abilitare questo profilo di Tuned, salvare le definizioni in un file **tuned.conf** in una cartella `/usr/lib/tuned/mssql` e abilitare il profilo usando i comandi seguenti:

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

Per verificare che sia abilitato, eseguire il comando seguente:

```bash
tuned-adm active
```

oppure

```bash
tuned-adm list
```

#### <a name="cpu-settings-recommendation"></a>Raccomandazione sulle impostazioni della CPU

La tabella seguente fornisce suggerimenti per le impostazioni della CPU:

| Impostazione | valore | Ulteriori informazioni |
|---|---|---|
| CPU frequency governor | prestazioni | Vedere il comando **cpupower** |
| ENERGY_PERF_BIAS | prestazioni | Vedere il comando **x86_energy_perf_policy** |
| min_perf_pct | 100 | Vedere la documentazione su Intel p-state |
| C-States | C1 only | Vedere la documentazione di Linux o del sistema su come verificare che C-States sia impostato su C1 only |

L'uso di **_Tuned_ *_ descritto in precedenza configura automaticamente e in modo appropriato le impostazioni del gestore della frequenza della CPU, di ENERGY_PERF_BIAS e di min_perf_pct grazie al profilo delle prestazioni della velocità effettiva usato come base per il profilo _* mssql**. Il parametro C-States deve essere configurato manualmente in base alla documentazione fornita da Linux o dal distributore del sistema.

#### <a name="disk-settings-recommendations"></a>Raccomandazioni sulle impostazioni del disco

La tabella seguente fornisce suggerimenti per le impostazioni del disco:

| Impostazione | valore | Ulteriori informazioni |
|---|---|---|
| `readahead` del disco | 4096 | Vedere il comando `blockdev` |
| impostazioni sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 1 | Vedere il comando **sysctl** |

**Descrizione:**

- **vm.swappiness**: questo parametro controlla il peso relativo assegnato allo scambio della memoria di runtime limitando il kernel allo scambio delle pagine di memoria del processo di SQL Server.

- **vm.dirty_\** _: gli accessi in scrittura dei file di SQL Server non vengono memorizzati nella cache, soddisfacendo i requisiti di integrità dei dati. Questi parametri consentono di ottenere prestazioni elevate di scrittura asincrona e di ridurre l'impatto delle operazioni di scrittura nella cache di Linux sulle operazioni di input/output di archiviazione, consentendo una memorizzazione nella cache sufficiente limitando al contempo lo svuotamento.

- _*kernel.sched_\**_: Questi valori del parametro rappresentano la raccomandazione corrente per la modifica dell'algoritmo CFS (Completely Fair Scheduling) nel kernel di Linux, per migliorare la velocità effettiva delle chiamate di I/O di rete e di archiviazione rispetto alla precedenza e al ripristino dei thread tra processi.

L'uso del profilo _*mssql** di **_Tuned_*_ configura le impostazioni _*vm.swappiness**, **vm.dirty_\* *_ e _* kernel.sched_\**_. La configurazione `readahead` del disco tramite il comando `blockdev` deve essere eseguita manualmente per ogni dispositivo.

#### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Impostazione del kernel per il bilanciamento numa automatico per i sistemi NUMA a più nodi

Se si installa SQL Server in un sistema _ *NUMA** a più nodi, l'impostazione del kernel **kernel.numa_balancing** seguente è abilitata per impostazione predefinita. Per consentire a SQL Server di operare alla massima efficienza in un sistema **NUMA**, disabilitare il bilanciamento numa automatico in un sistema NUMA a più nodi:

```bash
sysctl -w kernel.numa_balancing=0
```

L'uso del profilo **mssql** di **_Tuned_ *_ configura l'opzione _* kernel.numa_balancing**.

#### <a name="kernel-settings-for-virtual-address-space"></a>Impostazioni del kernel per lo spazio indirizzi virtuali

L'impostazione predefinita di **vm.max_map_count** (65536) potrebbe non essere sufficientemente elevata per un'installazione di SQL Server. Per questo motivo, cambiare il valore **vm.max_map_count** in almeno 262144 per una distribuzione di SQL Server e vedere la sezione [Impostazioni di Linux proposte con un profilo mssql di Tuned](#proposed-linux-settings-using-a-tuned-mssql-profile) per altre ottimizzazioni di questi parametri del kernel. Il valore massimo per vm.max_map_count è 2147483647.

```bash
sysctl -w vm.max_map_count=1600000
```

L'uso del profilo **mssql** di **_Tuned_ *_ configura l'opzione _* vm.max_map_count**.

#### <a name="leave-transparent-huge-pages-thp-enabled"></a>Lasciare abilitate le pagine THP (Transparent Huge Page)

Nella maggior parte delle installazioni Linux questa opzione dovrebbe essere attiva per impostazione predefinita. Per prestazioni più coerenti, è consigliabile lasciare abilitata questa opzione di configurazione. Se tuttavia è presente un'attività di paging della memoria consistente nelle distribuzioni di SQL Server con più istanze, ad esempio, o in caso di esecuzione di SQL Server con altre applicazioni con requisiti elevati di memoria nel server, è consigliabile testare le prestazioni delle applicazioni dopo l'esecuzione del comando seguente:

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```

In alternativa, modificare il profilo **mssql** * *di _Tuned_* _ con la riga:

```bash
vm.transparent_hugepages=madvise
```

Rendere attivo il profilo _ *mssql** dopo la modifica:

```bash
tuned-adm off
tuned-adm profile mssql
```

L'uso del profilo **mssql** di **_Tuned_ *_ configura l'opzione _* transparent_hugepage**.

#### <a name="additional-advanced-kernelos-configuration"></a>Configurazione aggiuntiva avanzata del kernel/sistema operativo

1. Per ottimizzare le prestazioni di I/O di archiviazione, è consigliabile usare la pianificazione a più code di Linux per i dispositivi a blocchi, che rende le prestazioni a livello di blocco facilmente scalabili in base alle unità SSD e ai sistemi multicore. Controllare nella documentazione se è abilitata per impostazione predefinita nelle distribuzioni di Linux. Nella maggior parte degli altri casi, viene abilitata avviando il kernel con **scsi_mod.use_blk_mq=y**, ma la documentazione della distribuzione di Linux in uso potrebbe contenere indicazioni aggiuntive. Ciò è coerente con il kernel di Linux upstream.

1. Poiché Multipath I/O viene spesso usato per le distribuzioni di SQL Server, è consigliabile configurare anche la destinazione Multipath del mapper dispositivi per l'uso dell'infrastruttura `blk-mq` abilitando l'opzione di avvio del kernel **dm_mod.use_blk_mq=y**. Il valore predefinito è `n` (disabilitato). Questa impostazione, quando i dispositivi SCSI sottostanti usano `blk-mq`, riduce l'overhead dei blocchi a livello di mapper dispositivi. Per indicazioni aggiuntive su come configurarla, vedere la documentazione della distribuzione di Linux in uso.

#### <a name="configure-swapfile"></a>Configurare un file di scambio

Assicurarsi di avere un file di scambio configurato correttamente per evitare problemi di memoria insufficiente. Per informazioni sulla creazione e il corretto dimensionamento di un file di scambio, vedere la documentazione di Linux.

#### <a name="virtual-machines-and-dynamic-memory"></a>Macchine virtuali e memoria dinamica

Se si esegue SQL Server in Linux in una macchina virtuale, assicurarsi di selezionare le opzioni per correggere la quantità di memoria riservata per la macchina virtuale. Non usare funzionalità come la memoria dinamica di Hyper-V.

## <a name="sql-server-configuration"></a>Configurazione di SQL Server

È consigliabile eseguire le attività di configurazione seguenti dopo l'installazione di SQL Server in Linux per ottenere prestazioni ottimali per l'applicazione.

### <a name="best-practices"></a>Procedure consigliate

- **Usare PROCESS AFFINITY per il nodo e/o le CPU**

   È consigliabile usare `ALTER SERVER CONFIGURATION` per impostare `PROCESS AFFINITY` per tutte le opzioni **NUMANODE** e/o le CPU usate per SQL Server (in genere, per tutti i NODI e le CPU) in un sistema operativo Linux. L'affinità processori consente di mantenere efficiente il comportamento di pianificazione di SQL e Linux. L'uso dell'opzione **NUMANODE** è il metodo più semplice. Usare **PROCESS AFFINITY** anche se nel computer è presente un solo nodo NUMA. Per altre informazioni su come impostare **PROCESS AFFINITY**, vedere l'articolo [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md).

- **Configurare più file di dati tempdb**

   Poiché un'installazione di SQL Server in Linux non offre un'opzione per la configurazione di più file tempdb, è consigliabile creare più file di dati tempdb dopo l'installazione. Per altre informazioni, vedere le linee guida nell'articolo [Suggerimenti per ridurre la contesa per l'allocazione nel database tempdb di SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configurazione avanzata

I suggerimenti seguenti sono impostazioni di configurazione facoltative che è possibile scegliere di eseguire dopo l'installazione di SQL Server in Linux. Queste scelte sono basate sui requisiti del carico di lavoro e sulla configurazione del sistema operativo Linux.

- **Impostare un limite di memoria con mssql-conf**

   Per assicurarsi che la memoria fisica disponibile sia sufficiente per il sistema operativo Linux, per impostazione predefinita, il processo SQL Server usa solo l'80% della RAM fisica. Per alcuni sistemi con una grande quantità di RAM fisica, il 20% potrebbe essere un numero significativo. Ad esempio, in un sistema con 1 TB di RAM, l'impostazione predefinita lascerà circa 200 GB di RAM inutilizzata. In questo caso, potrebbe essere necessario configurare il limite di memoria su un valore superiore. Vedere la documentazione sullo strumento **mssql-conf** e sull'impostazione [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) che controlla la memoria visibile a SQL Server (in unità di MB).

   Quando si modifica questa impostazione, cercare di non impostare un valore troppo elevato. Se non si lascia memoria sufficiente, è possibile che si verifichino problemi con il sistema operativo Linux e con altre applicazioni Linux.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle funzionalità di SQL Server che migliorano le prestazioni, vedere [Introduzione alle funzionalità relative alle prestazioni](sql-server-linux-performance-get-started.md).

Per altre informazioni su SQL Server in Linux, vedere [Panoramica di SQL Server in Linux](sql-server-linux-overview.md).
