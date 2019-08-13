---
title: Configurare condivisioni di cartelle snapshot per la replica di SQL Server in Linux
description: Questo articolo descrive come configurare condivisioni di cartelle snapshot per la replica di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6959b2073871f70fb33823b50419c208a23df2dd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68093178"
---
# <a name="configure-replication-with-non-default-ports"></a>Configurare la replica con porte non predefinite

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile configurare la replica con istanze di SQL Server in Linux in ascolto su qualsiasi porta configurata con l'impostazione network.tcpport mssql-conf. È necessario accodare la porta al nome del server durante la configurazione se le condizioni seguenti sono soddisfatte:

1. La configurazione della replica interessa un'istanza di SQL Server in Linux
2. Una qualsiasi istanza (Windows o Linux) è in ascolto su una porta non predefinita. 

Per trovare il nome del server di un'istanza è possibile eseguire @@servername per l'istanza stessa.

## <a name="examples"></a>Esempi

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare 'Server1' per la distribuzione, eseguire `sp_adddistributor` con `@distributor`. Esempio: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare un server di pubblicazione per il database di distribuzione, eseguire `sp_adddistpublisher` con `@publisher`. Esempio:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' è in ascolto sulla porta 6549 in Linux. Per configurare 'Server2' come sottoscrittore, eseguire `sp_addsubscription` con `@subscriber`. Esempio:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' è in ascolto sulla porta 6549 in Windows con nome del server Server3 e nome dell'istanza MSSQL2017. Per configurare 'Server3' come sottoscrittore, eseguire `sp_addsubscription` con `@subscriber`. Esempio:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Passaggi successivi

[Concetti: replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure per la replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

