---
title: Configurare la cartella snapshot delle repliche (porte non predefinite)
titleSuffix: SQL Server on Linux
description: Informazioni su come configurare le condivisioni della cartella snapshot con porte non predefinite per la replica di SQL Server in Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikerayW
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb715e2a0a056c18352361b58ce8ffd67e3da78e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558596"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>Configurare la replica con porte non predefinite (SQL Server in Linux)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile configurare la replica con istanze di SQL Server in Linux in ascolto su qualsiasi porta configurata con l'impostazione network.tcpport mssql-conf. È necessario accodare la porta al nome del server durante la configurazione se le condizioni seguenti sono soddisfatte:

1. La configurazione della replica interessa un'istanza di SQL Server in Linux
2. Una qualsiasi istanza (Windows o Linux) è in ascolto su una porta non predefinita. 

Per trovare il nome del server di un'istanza è possibile eseguire @@servername per l'istanza stessa.

## <a name="examples"></a>Esempi

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare 'Server1' per la distribuzione, eseguire `sp_adddistributor` con `@distributor`. Ad esempio: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' è in ascolto sulla porta 1500 in Linux. Per configurare un server di pubblicazione per il database di distribuzione, eseguire `sp_adddistpublisher` con `@publisher`. Ad esempio:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' è in ascolto sulla porta 6549 in Linux. Per configurare 'Server2' come sottoscrittore, eseguire `sp_addsubscription` con `@subscriber`. Ad esempio:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' è in ascolto sulla porta 6549 in Windows con nome del server Server3 e nome dell'istanza MSSQL2017. Per configurare 'Server3' come sottoscrittore, eseguire `sp_addsubscription` con `@subscriber`. Ad esempio:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Passaggi successivi

[Concetti: replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure per la replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

