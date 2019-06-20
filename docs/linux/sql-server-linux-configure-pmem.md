---
title: Come configurare la memoria persistente (PMEM) per SQL Server in Linux | Microsoft Docs
description: Questo articolo fornisce una procedura dettagliata per la configurazione PMEM in Linux.
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5421d42933660843ac51be3d942a94cf47866200
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713237"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Come configurare la memoria persistente (PMEM) per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come configurare la memoria persistente (PMEM) per SQL Server in Linux. Supporto PMEM in Linux è stato introdotto in fase di anteprima di SQL Server 2019.

## <a name="overview"></a>Panoramica

SQL Server 2016 ha introdotto il supporto per moduli DIMM Non-Volatile e un'ottimizzazione denominata [della parte finale del Log memorizzazione nella cache nella memoria NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). Queste ottimizzazioni ridotto il numero di operazioni necessarie per finalizzare un buffer del log in un archivio permanente. Questo consente di sfruttare l'accesso diretto di Windows Server a un dispositivo di memoria persistente in modalità DAX.

Anteprima di SQL Server 2019 estende il supporto per la memoria persistente dispositivi (PMEM) per Linux, fornendo illuminazione completa dei dati e delle transazioni di file di log inseriti in PMEM. Illuminazione fa riferimento al metodo di accesso al dispositivo di archiviazione con spazio utente efficiente `memcpy()` operazioni. Anziché passare attraverso lo stack di sistema e l'archiviazione file, SQL Server Usa il supporto DAX in Linux per inserire i dati direttamente in dispositivi, riducendo la latenza.

## <a name="enable-enlightenment-of-database-files"></a>Abilitare illuminazione dei file di database
Per abilitare l'illuminazione di file di database in SQL Server in Linux, seguire i passaggi seguenti:

1. Configurare i dispositivi.

  In Linux, usare il `ndctl` utilità.

  - Installare `ndctl` configurare PMEM dispositivo. È possibile trovarlo [qui](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Per creare uno spazio dei nomi, usare [ndctl].

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >Se si usa `ndctl` versioni precedenti a 59, usare `--mode=memory`.

  Usare `ndctl` per verificare lo spazio dei nomi. Output di esempio seguente:

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

  - Creare e montare PMEM dispositivo

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

  Una volta che il dispositivo è stato configurato con ndctl, formattato e montato, è possibile inserire i file di database in esso. È anche possibile creare un nuovo database 

1. Poiché i dispositivi PMEM sono O_DIRECT sicura, abilitare il flag di traccia 3979 per disabilitare il meccanismo di scaricamento forzato. Questo flag di traccia è un flag di traccia di avvio e di conseguenza deve essere abilitato tramite l'utilità mssql-conf. Si noti che si tratta di una modifica della configurazione a livello di server e non si deve utilizzare questo flag di traccia se si dispone di eventuali dispositivi non conformi O_DIRECT che richiedono il meccanismo di scaricamento forzato per garantire l'integrità dei dati. Per ulteriori informazioni, vedere https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux.

1. Riavviare SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
