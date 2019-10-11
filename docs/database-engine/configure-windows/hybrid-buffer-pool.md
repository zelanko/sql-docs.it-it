---
title: Pool di buffer ibrido | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: d03c66219330df3cca892bd005d1e9a456959c83
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823565"
---
# <a name="hybrid-buffer-pool"></a>Pool di buffer ibrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il pool di buffer ibrido consente al motore di database di accedere direttamente alle pagine di dati nei file di database archiviati nei dispositivi con memoria persistente. Questa funzionalità è stata introdotta in [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)].

In un sistema tradizionale senza memoria persistente SQL Server memorizza nella cache le pagine di dati del pool di buffer. Con il pool di buffer ibrido, SQL Server non esegue una copia della pagina nella parte di memoria basata su DRAM del pool di buffer, ma accede alla pagina direttamente nel file di database che si trova nel dispositivo con memoria persistente. L'accesso in lettura ai file di dati nei dispositivi PMEM per il pool di buffer ibrido viene eseguito direttamente seguendo un puntatore alle pagine di dati nel dispositivo PMEM.  

In un dispositivo con memoria persistente è possibile accedere direttamente solo alle pagine clean. Quando una pagina è contrassegnata come dirty, viene prima copiata nel pool di buffer DRAM e poi riscritta nel dispositivo con memoria persistente e contrassegnata nuovamente come clean. Ciò si verifica durante le normali operazioni di checkpoint. Il meccanismo per copiare il file dal dispositivo PMEM alla DRAM è l'I/O mappato alla memoria (MMIO, Memory-Mapped I/O) diretto ed è noto anche come *riconoscimento* dei file di dati all'interno di SQL Server.


La funzionalità di pool di buffer ibrido è disponibile sia per Windows che per Linux. Il dispositivo con memoria persistente deve essere formattato con un file system che supporti DAX (DirectAccess). I file system XFS, EXT4 e NTFS supportano tutti DAX. SQL Server rileverà automaticamente se i file di dati si trovano in un dispositivo PMEM formattato in modo appropriato ed eseguirà il mapping di memoria nello spazio utente. Questo mapping si verifica all'avvio, quando un nuovo database viene collegato, ripristinato, creato o quando la funzionalità di pool di buffer ibrido viene abilitata per un database.

Per altre informazioni sul supporto di Windows Server per PMEM, vedere [Distribuire la memoria persistente in Windows Server](/windows-server/storage/storage-spaces/deploy-pmem/).

Per altre informazioni sulla configurazione di SQL Server in Linux per i dispositivi PMEM, vedere [Distribuire la memoria persistente](../../linux/sql-server-linux-configure-pmem.md).

## <a name="enable-hybrid-buffer-pool"></a>Abilitare il pool di buffer ibrido

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] introduce il linguaggio dei dati dinamici per controllare il pool di buffer ibrido.

Nell'esempio seguente viene abilitato il pool di buffer ibrido per un'istanza di SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

Per impostazione predefinita, il pool di buffer ibrido è disabilitato nell'ambito dell'istanza. Si noti che è necessario riavviare l'istanza di SQL Server per rendere effettiva la modifica dell'impostazione. È necessario un riavvio per facilitare l'allocazione di pagine hash sufficienti tenendo conto della capacità PMEM totale nel server.

Nell'esempio seguente viene abilitato il pool di buffer ibrido per un database specifico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

Per impostazione predefinita, il pool di buffer ibrido è abilitato nell'ambito del database.

## <a name="disable-hybrid-buffer-pool"></a>Disabilitare il pool di buffer ibrido

Nell'esempio seguente viene disabilitato il pool di buffer ibrido per un'istanza di SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

Per impostazione predefinita, il pool di buffer ibrido è disabilitato nell'ambito dell'istanza. Si noti che è necessario riavviare l'istanza di SQL Server per rendere effettiva la modifica dell'impostazione. È necessario un riavvio per impedire l'allocazione eccessiva di pagine hash, perché non occorre tenere conto della capacità PMEM nel server.

Nell'esempio seguente viene disabilitato il pool di buffer ibrido per un database specifico.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

Per impostazione predefinita, il pool di buffer ibrido è abilitato nell'ambito del database.

## <a name="view-hybrid-buffer-pool-configuration"></a>Visualizzare la configurazione pool di buffer ibrido

L'esempio seguente restituisce lo stato corrente della configurazione di sistema del pool di buffer ibrido per un'istanza di SQL Server.

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

Nell'esempio seguente vengono restituite due tabelle:

- Nella prima viene illustrato lo stato corrente della configurazione di sistema del pool di buffer ibrido per un'istanza di SQL Server.
- Nella seconda vengono elencati i database e l'impostazione del livello di database per il pool di buffer ibrido (`is_memory_optimized_enabled`).

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>Procedure consigliate per il pool di buffer ibrido

Quando si formatta un dispositivo PMEM in Windows, usare le dimensioni di unità di allocazione più grandi disponibili per NTFS (2 MB in Windows Server 2019) e assicurarsi che il dispositivo sia stato formattato per DAX (Direct Access).

Per ottenere prestazioni ottimali, abilitare [Blocco di pagine in memoria](./enable-the-lock-pages-in-memory-option-windows.md) in Windows.

Le dimensioni dei file devono essere un multiplo di 2 MB (modulo 2 MB deve essere uguale a zero).

Se l'impostazione con ambito server per il pool di buffer ibrido è disabilitata, il pool di buffer ibrido non verrà usato da alcun database utente.

Se l'impostazione con ambito server per il pool di buffer ibrido è abilitata, è possibile disabilitare l'uso per i database utente singoli seguendo la procedura per disabilitare il pool di buffer ibrido a livello configurazione con ambito database per i database utente.
