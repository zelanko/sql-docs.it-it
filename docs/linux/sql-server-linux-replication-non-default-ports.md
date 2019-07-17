---
title: Configurare condivisioni cartella snapshot della replica di SQL Server in Linux
description: Questo articolo descrive come configurare la replica di SQL Server condivisioni cartella snapshot in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6959b2073871f70fb33823b50419c208a23df2dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093178"
---
# <a name="configure-replication-with-non-default-ports"></a>Configurare la replica con porte non predefinite

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile configurare la replica con SQL Server nelle istanze di Linux in attesa su qualsiasi porta configurata con l'impostazione di network.tcpport mssql-conf. La porta deve essere aggiunto al nome del server durante la configurazione, se vengono soddisfatte le condizioni seguenti:

1. Configurare la replica prevede un'istanza di SQL Server in Linux
2. Qualsiasi istanza (Windows o Linux) è in ascolto su una porta non predefinito. 

Il nome del server di un'istanza è reperibile eseguendo @@servername nell'istanza.

## <a name="examples"></a>Esempi

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare 'Server1' per la distribuzione, eseguire `sp_adddistributor` con `@distributor`. Ad esempio: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare un server di pubblicazione per il server di distribuzione, eseguire `sp_adddistpublisher` con `@publisher`. Ad esempio:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' è in ascolto sulla porta 6549 in Linux. Per configurare 'Server2' come sottoscrittore, eseguire `sp_addsubscription` con `@subscriber`. Ad esempio:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' è in ascolto sulla porta 6549 su Windows con nome server Server3 e il nome dell'istanza di MSSQL2017. Per configurare 'Server3' come sottoscrittore, eseguire la `sp_addsubscription` con `@subscriber`. Ad esempio:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Passaggi successivi

[Concetti: Replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

