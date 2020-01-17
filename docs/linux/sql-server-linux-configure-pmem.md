---
title: Configurare la memoria persistente per SQL Server in Linux
description: Questo articolo descrive la procedura dettagliata per la configurazione della memoria persistente in Linux.
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.reviewer: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b5f86dac62c371a9e4dda607cbd9ec7533a187a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558613"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Come configurare la memoria persistente per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come configurare la memoria persistente per SQL Server in Linux. Il supporto della memoria persistente in Linux è stato introdotto in SQL Server 2019.

## <a name="overview"></a>Panoramica

SQL Server 2016 ha introdotto il supporto per i DIMM non volatili e un'ottimizzazione denominata [Memorizzazione della cache del file LDF in NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). Queste ottimizzazioni riducono il numero di operazioni necessarie per finalizzare i buffer dei log in una risorsa di archiviazione permanente. Questa operazione sfrutta l'accesso diretto di Windows Server a un dispositivo di memoria permanente in modalità DAX.

SQL Server 2019 estende il supporto dei dispositivi con memoria persistente a Linux, garantendo il riconoscimento completo dei file di dati e dei log delle transazioni all'interno della memoria persistente. Per riconoscimento si intende il metodo di accesso al dispositivo di archiviazione tramite operazioni `memcpy()` efficienti sullo spazio utente. Invece di passare attraverso il file system e lo stack di archiviazione, SQL Server si avvale del supporto DAX in Linux per inserire direttamente i dati nei dispositivi, riducendo la latenza.

## <a name="enable-enlightenment-of-database-files"></a>Abilitare il riconoscimento dei file di database
Per abilitare il riconoscimento dei file di database in SQL Server in Linux, seguire questa procedura:

1. Configurare i dispositivi.

  In Linux usare l'utilità `ndctl`.

  - Installare `ndctl` per configurare il dispositivo con memoria persistente. L'utilità è disponibile [qui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Usare [ndctl] per creare uno spazio dei nomi.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >Se si usa una versione di `ndctl` precedente alla 59, usare `--mode=memory`.

  Usare `ndctl` per verificare lo spazio dei nomi. Di seguito è riportato output di esempio:

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - Creare e montare il dispositivo con memoria persistente

    Ad esempio, con XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    Ad esempio, con EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  Dopo che il dispositivo è stato configurato con ndctl, formattato e montato, è possibile inserire file di database all'interno di esso. È anche possibile creare un nuovo database 

1. Poiché i dispositivi con memoria persistente sono protetti da O_DIRECT, abilitare il flag di traccia 3979 per disabilitare il meccanismo di scaricamento forzato. Questo è un flag di traccia di avvio e come tale deve essere abilitato tramite l'utilità mssql-conf. Si noti che questa è una modifica della configurazione a livello di server e che questo flag di traccia non deve essere usato se sono presenti dispositivi non conformi a O_DIRECT che richiedono il meccanismo di scaricamento forzato per garantire l'integrità dei dati. Per ulteriori informazioni, vedere https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux.

1. Riavviare SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
