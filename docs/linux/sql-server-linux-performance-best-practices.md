---
title: Procedure consigliate per le prestazioni per SQL Server in Linux
description: Questo articolo illustra le procedure consigliate per le prestazioni e le linee guida per l'esecuzione di SQL Server in Linux.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 10/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ddeb5d106de872b507c88a199050cfc883a63a4c
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005684"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Procedure consigliate per le prestazioni e linee guida per la configurazione per SQL Server in Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Questo articolo fornisce procedure consigliate e suggerimenti per ottimizzare le prestazioni per le applicazioni di database che si connettono a SQL Server in Linux. Questi suggerimenti sono specifici per l'esecuzione nella piattaforma Linux. Tutte i normali suggerimenti per SQL Server, ad esempio la progettazione degli indici, sono comunque validi.

Le linee guida seguenti contengono suggerimenti per la configurazione sia di SQL Server che del sistema operativo Linux.

## <a name="sql-server-configuration"></a>Configurazione di SQL Server

È consigliabile eseguire le attività di configurazione seguenti dopo l'installazione di SQL Server in Linux per ottenere prestazioni ottimali per l'applicazione.

### <a name="best-practices"></a>Procedure consigliate

- **Usare PROCESS AFFINITY per il nodo e/o le CPU**

   È consigliabile usare `ALTER SERVER CONFIGURATION` per impostare `PROCESS AFFINITY` per tutte le opzioni **NUMANODE** e/o le CPU usate per SQL Server (in genere, per tutti i NODI e le CPU) in un sistema operativo Linux. L'affinità processori consente di mantenere efficiente il comportamento di pianificazione di SQL e Linux. L'uso dell'opzione **NUMANODE** è il metodo più semplice. È consigliabile usare **PROCESS AFFINITY** anche se nel computer è presente un solo nodo NUMA.  Vedere la documentazione di [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) per altre informazioni su come impostare **PROCESS AFFINITY**.

- **Configurare più file di dati tempdb**

   Poiché un'installazione di SQL Server in Linux non offre un'opzione per la configurazione di più file tempdb, è consigliabile creare più file di dati tempdb dopo l'installazione. Per altre informazioni, vedere le linee guida nell'articolo [Suggerimenti per ridurre la contesa per l'allocazione nel database tempdb di SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configurazione avanzata

I suggerimenti seguenti sono impostazioni di configurazione facoltative che è possibile scegliere di eseguire dopo l'installazione di SQL Server in Linux. Queste scelte sono basate sui requisiti del carico di lavoro e sulla configurazione del sistema operativo Linux.

- **Impostare un limite di memoria con mssql-conf**

   Per assicurarsi che la memoria fisica disponibile sia sufficiente per il sistema operativo Linux, per impostazione predefinita, il processo SQL Server usa solo l'80% della RAM fisica. Per alcuni sistemi con una grande quantità di RAM fisica, il 20% potrebbe essere un numero significativo. Ad esempio, in un sistema con 1 TB di RAM, l'impostazione predefinita lascerà circa 200 GB di RAM inutilizzata. In questo caso, potrebbe essere necessario configurare il limite di memoria su un valore superiore. Vedere la documentazione sullo strumento **mssql-conf** e sull'impostazione [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) che controlla la memoria visibile a SQL Server (in unità di MB).

   Quando si modifica questa impostazione, cercare di non impostare un valore troppo elevato. Se non si lascia memoria sufficiente, è possibile che si verifichino problemi con il sistema operativo Linux e con altre applicazioni Linux.

## <a name="linux-os-configuration"></a>Configurazione del sistema operativo Linux

Provare a usare le impostazioni di configurazione del sistema operativo Linux seguenti per ottenere prestazioni ottimali per un'installazione di SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Impostazioni del kernel per prestazioni elevate
Queste sono le impostazioni consigliate per il sistema operativo Linux per ottenere prestazioni e velocità effettiva elevate per un'installazione di SQL Server. Per il processo di configurazione di queste impostazioni, vedere la documentazione del sistema operativo Linux.



> [!Note]
> Per gli utenti di Red Hat Enterprise Linux (RHEL), il profilo delle prestazioni della velocità effettiva [ottimizzato](https://tuned-project.org) configurerà automaticamente queste impostazioni (tranne C-States). A partire da RHEL 8.0, è stato sviluppato un profilo predefinito mssql /usr/lib/tuned in collaborazione con Red Hat, che offre ottimizzazioni più dettagliate correlate alle prestazioni di Linux per i carichi di lavoro di SQL Server. Questo profilo include il profilo di prestazioni per la velocità effettiva RHEL e le definizioni sono presentate di seguito per poterle confrontare con altre distribuzioni di Linux e versioni di RHEL senza questo profilo.

La tabella seguente fornisce suggerimenti per le impostazioni della CPU:

| Impostazione | valore | Ulteriori informazioni |
|---|---|---|
| CPU frequency governor | prestazioni | Vedere il comando **cpupower** |
| ENERGY_PERF_BIAS | prestazioni | Vedere il comando **x86_energy_perf_policy** |
| min_perf_pct | 100 | Vedere la documentazione su Intel p-state |
| C-States | C1 only | Vedere la documentazione di Linux o del sistema su come verificare che C-States sia impostato su C1 only |

La tabella seguente fornisce suggerimenti per le impostazioni del disco:

| Impostazione | valore | Ulteriori informazioni |
|---|---|---|
| readahead del disco | 4096 | Vedere il comando **blockdev** |
| impostazioni sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | Vedere il comando **sysctl** |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Impostazione del kernel per il bilanciamento numa automatico per i sistemi NUMA a più nodi

Se si installa SQL Server in un sistema **NUMA** a più nodi, l'impostazione del kernel **kernel.numa_balancing** seguente è abilitata per impostazione predefinita. Per consentire a SQL Server di operare alla massima efficienza in un sistema **NUMA**, disabilitare il bilanciamento numa automatico in un sistema NUMA a più nodi:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Impostazioni del kernel per lo spazio indirizzi virtuali

L'impostazione predefinita di **vm.max_map_count** (65536) potrebbe non essere sufficientemente elevata per un'installazione di SQL Server. Per questo motivo, cambiare il valore **vm.max_map_count** in almeno 262144 per una distribuzione di SQL Server e vedere la sezione [Impostazioni di Linux proposte con un profilo mssql ottimizzato](#proposed-linux-settings-using-a-tuned-mssql-profile) per altre ottimizzazioni di questi parametri del kernel. Il valore massimo per vm.max_map_count è 2147483647.

```bash
sysctl -w vm.max_map_count=1600000
```

### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Impostazioni di Linux proposte con un profilo mssql ottimizzato

```bash
#
# A tuned configuration for SQL Server on Linux
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

Per abilitare questo profilo ottimizzato, salvare le definizioni in un file **tuned.conf** in una cartella/usr/lib/tuned/mssql e abilitare il profilo usando

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

Verificarne l'abilitazione con

```bash
tuned-adm active
```
oppure
```bash
tuned-adm list
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Disabilitare la data e ora dell'ultimo accesso nei file system per i file di dati e di log di SQL Server

Usare l'attributo **noatime** con qualsiasi file system usato per archiviare i file di dati e di log di SQL Server. Per informazioni su come impostare questo attributo, vedere la documentazione di Linux.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Lasciare abilitate le pagine THP (Transparent Huge Page)

Nella maggior parte delle installazioni Linux questa opzione dovrebbe essere attiva per impostazione predefinita. Per prestazioni più coerenti, è consigliabile lasciare abilitata questa opzione di configurazione. Tuttavia, nel caso di un'attività di paging della memoria consistente nelle distribuzioni di SQL Server con più istanze, ad esempio, o in caso di esecuzione di SQL Server con altre applicazioni con requisiti elevati di memoria nel server, è consigliabile testare le prestazioni delle applicazioni dopo l'esecuzione del comando seguente 

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```
o modificare il profilo ottimizzato mssql con la linea

```bash
vm.transparent_hugepages=madvise
```
e rendere attivo il profilo mssql dopo la modifica
```bash
tuned-adm off
tuned-adm profile mssql
```

### <a name="swapfile"></a>File di scambio

Assicurarsi di avere un file di scambio configurato correttamente per evitare problemi di memoria insufficiente. Per informazioni sulla creazione e il corretto dimensionamento di un file di scambio, vedere la documentazione di Linux.

### <a name="virtual-machines-and-dynamic-memory"></a>Macchine virtuali e memoria dinamica

Se si esegue SQL Server in Linux in una macchina virtuale, assicurarsi di selezionare le opzioni per correggere la quantità di memoria riservata per la macchina virtuale. Non usare funzionalità come la memoria dinamica di Hyper-V.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle funzionalità di SQL Server che migliorano le prestazioni, vedere [Introduzione alle funzionalità relative alle prestazioni](sql-server-linux-performance-get-started.md).

Per altre informazioni su SQL Server in Linux, vedere [Panoramica di SQL Server in Linux](sql-server-linux-overview.md).
