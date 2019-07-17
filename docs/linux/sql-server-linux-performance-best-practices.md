---
title: Procedure consigliate sulle prestazioni per SQL Server in Linux
description: Questo articolo offre linee guida e procedure consigliate sulle prestazioni per l'esecuzione di SQL Server in Linux.
author: rgward
ms.author: bobward
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 543488eada46a088f3c634ce2326c7e2db2a97a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105445"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Prestazioni le procedure consigliate e linee guida per la configurazione per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo fornisce le procedure consigliate e consigli per ottimizzare le prestazioni per le applicazioni di database che si connettono a SQL Server in Linux. Questi suggerimenti sono specifici per l'esecuzione sulla piattaforma Linux. Tutte le raccomandazioni di SQL Server normali, ad esempio la progettazione di indici, vengono mantenuti.

Le linee guida seguenti sono inclusi suggerimenti per la configurazione di SQL Server e il sistema operativo Linux.

## <a name="sql-server-configuration"></a>Configurazione di SQL Server

È consigliabile eseguire le attività di configurazione seguenti dopo aver installato SQL Server in Linux per ottenere prestazioni ottimali per l'applicazione.

### <a name="best-practices"></a>Procedure consigliate

- **Utilizzare l'AFFINITÀ di processo per nodo e/o CPU**

   È consigliabile usare `ALTER SERVER CONFIGURATION` per impostare `PROCESS AFFINITY` per tutte le **NUMANODEs** e/o CPU in uso per SQL Server, ovvero in genere per tutti i nodi e la CPU, in un sistema operativo Linux. Affinità processori aiuta a mantenere il comportamento di Linux e la pianificazione di SQL efficiente. Usando il **NUMANODE** opzione è il metodo più semplice. Si noti che è consigliabile usare **AFFINITÀ del processo** anche se si dispone di un solo nodo NUMA nel computer.  Vedere le [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) per altre informazioni su come impostare **AFFINITÀ del processo**.

- **Configurare più file di dati di tempdb**

   Poiché SQL Server nell'installazione Linux non offre un'opzione per configurare più file di tempdb, è consigliabile prendere in considerazione la creazione di file di dati tempdb più dopo l'installazione. Per altre informazioni, vedere le indicazioni fornite nell'articolo [consigli per ridurre il conflitto di allocazione nel database tempdb di SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configurazione avanzata

Le raccomandazioni seguenti sono le impostazioni di configurazione facoltativi che è possibile scegliere di eseguire dopo l'installazione di SQL Server in Linux. Queste opzioni si basano sui requisiti del carico di lavoro e configurazione del sistema operativo Linux.

- **Impostare un limite di memoria con mssql-conf**

   Per assicurare che vi sia sufficiente memoria fisica libera per il sistema operativo Linux, il processo di SQL Server Usa solo l'80% della RAM fisica per impostazione predefinita. Per alcuni sistemi quali grande quantità di RAM fisica, 20% potrebbe essere un numero significativo. Ad esempio, in un sistema con 1 TB di RAM, l'impostazione predefinita la lascia circa 200 GB di RAM inutilizzati. In questo caso, è possibile configurare il limite di memoria su un valore superiore. Vedere la documentazione sul **mssql-conf** dello strumento e il [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) l'impostazione che controlla la memoria visibile a SQL Server (in unità di MB).

   Quando si modifica questa impostazione, prestare attenzione a non impostare un valore troppo elevato. Se non si lascia memoria sufficiente, si potrebbero verificare problemi con il sistema operativo Linux e altre applicazioni di Linux.

## <a name="linux-os-configuration"></a>Configurazione del sistema operativo Linux

È consigliabile usare le seguenti impostazioni di configurazione di sistema operativo Linux per sperimentare le migliori prestazioni per un'installazione SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Impostazioni del kernel per garantire prestazioni elevate
Si tratta di prestazioni correlati ad alta le impostazioni di sistema operativo Linux e velocità effettiva per un'installazione di SQL Server consigliati. Vedere la documentazione del sistema operativo Linux per il processo configurare queste impostazioni.



> [!Note]
> Per gli utenti di Red Hat Enterprise Linux (RHEL), il profilo delle prestazioni di velocità effettiva verrà configurare queste impostazioni automaticamente (ad eccezione di C-state).

La tabella seguente fornisce indicazioni per le impostazioni della CPU:

| Impostazione | Value | Altre informazioni |
|---|---|---|
| Governor frequenza della CPU | prestazioni | Vedere le **cpupower** comando |
| ENERGY_PERF_BIAS | prestazioni | Vedere le **x86_energy_perf_policy** comando |
| min_perf_pct | 100 | Vedere la documentazione di intel. p-stato |
| Stati C | Solo C1 | Vedere la documentazione di sistema Linux o su come ottenere gli stati C sono impostato solo su C1 |

La tabella seguente fornisce indicazioni per le impostazioni del disco:

| Impostazione | Value | Altre informazioni |
|---|---|---|
| Read-ahead disco | 4096 | Vedere le **blockdev** comando |
| impostazioni sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>VM.swappiness = 10 | Vedere le **sysctl** comando |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Bilanciamento del carico per i sistemi a più nodi NUMA kernel impostazione automaticamente numa

Se si installa SQL Server in un multinodo **NUMA** sistemi, di seguito **kernel.numa_balancing** kernel è attivata per impostazione predefinita. Per consentire a SQL Server su cui operare alla massima efficienza un' **NUMA** system, disabilita automaticamente numa bilanciamento del carico in un sistema NUMA a più nodi:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Impostazioni del kernel per spazio degli indirizzi virtuali

L'impostazione predefinita **vm.max_map_count** potrebbe non essere sufficientemente elevato per un'installazione di SQL Server (ovvero 65536). Modificare questo valore, ovvero un limite superiore, a 256K.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Disabilitare la data/ora dell'ultimo accesso nei file System per i file di log e dati di SQL Server

Usare la **opzione noatime** attributo con qualsiasi file system che viene usato per archiviare i dati di SQL Server e i file di log. Consultare la documentazione di Linux su come impostare questo attributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Lasciare Transparent Huge Page (THP) abilitato

La maggior parte delle installazioni di Linux devono avere questa opzione per impostazione predefinita. È consigliabile per l'esperienza con prestazioni più coerente mantenere abilitata questa opzione di configurazione.

### <a name="swapfile"></a>file di scambio

Assicurarsi di che disporre di un file di scambio configurati correttamente per evitare eventuali problemi di memoria insufficiente. Consultare la documentazione di Linux per informazioni su come creare e impostare correttamente le dimensioni di un file di scambio.

### <a name="virtual-machines-and-dynamic-memory"></a>Le macchine virtuali e la memoria dinamica

Se si esegue SQL Server in Linux in una macchina virtuale, assicurarsi di che selezionare le opzioni per risolvere la quantità di memoria riservata per la macchina virtuale. Non usare funzionalità come la memoria dinamica di Hyper-V.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle funzionalità di SQL Server che consentono di migliorare le prestazioni, vedere [Introduzione alle funzionalità di prestazioni](sql-server-linux-performance-get-started.md).

Per altre informazioni su SQL Server in Linux, vedere [Panoramica di SQL Server in Linux](sql-server-linux-overview.md).
