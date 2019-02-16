---
title: Configurare condivisioni cartella snapshot della replica di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive come configurare la replica di SQL Server condivisioni cartella snapshot in Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b8ca6bbe8c8ae3bb07a6f0470cf2f6f8d648ea03
ms.sourcegitcommit: 769b71f01052ec9b4fc5eb02d9da9a1a58118029
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56319332"
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

'Server3' è in ascolto sulla porta 6549 su Windows con nome server Server3 e il nome dell'istanza di MSSQL2017. Per configurare 'Server3' come sottoscrittore, eseguire la `sp_addsubscription` con `@subscriber`. Esempio:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Passaggi successivi

[Concetti: Replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

