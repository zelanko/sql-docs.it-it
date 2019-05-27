---
title: Installare PolyBase in Linux | Microsoft Docs
description: Questo articolo descrive come installare la ricerca full-text di SQL Server in Linux.
author: aboke
ms.author: aboke
manager: craigg
ms.date: 4/12/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 69c256ef52d9c302d55ef1499059d959ed55b528
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759068"
---
# <a name="install-polybase-on-linux"></a>Installare PolyBase in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Usare la procedura seguente per installare [PolyBase](../../relational-databases/search/full-text-search.md) (**mssql-server-polybase**) in Linux. PolyBase consente di eseguire query esterne su origini dati remote. 

>[!NOTE]
> Prima di installare Polybase, [installare SQL Server](../../linux/sql-server-linux-setup.md#platforms). In questo modo verranno configurate le chiavi e i repository usati durante l'installazione del pacchetto **mssql-server-polybase**.

> Lo scale-out non è attualmente disponibile per PolyBase in Linux.


Installare PolyBase per il sistema operativo in uso:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name="RHEL">Eseguire l'installazione in RHEL</a>

Usare il comando seguente per installare **mssql-server-polybase** in Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).

Se è necessaria un'installazione offline, individuare il download del pacchetto di PolyBase nelle [Note sulla versione](../../linux/sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name="ubuntu">Eseguire l'installazione in Ubuntu</a>

Usare il comando seguente per installare **mssql-server-polybase** in Ubuntu. 

```bash
sudo apt-get install mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).

Se è necessaria un'installazione offline, individuare il download del pacchetto di PolyBase nelle [Note sulla versione](../../linux/sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name="SLES">Eseguire l'installazione in SLES</a>

Usare i comandi seguenti per installare **mssql-server-polybase** in SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).


Se è necessaria un'installazione offline, individuare il download del pacchetto di PolyBase nelle [Note sulla versione](../../linux/sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](../../linux/sql-server-linux-setup.md#offline).


## <a name="enable">Abilitare PolyBase</a> 

Dopo l'installazione, è necessario abilitare PolyBase per accedere alle relative funzionalità. Connettersi all'istanza installata di SQL Server e usare il comando di Transact-SQL seguente per eseguire l'abilitazione.

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [WITH OVERRIDE];
```

## <a name="update-polybase"></a>Aggiornare PolyBase

Se il pacchetto **mssql-server-polybase** è già installato, è possibile eseguire l'aggiornamento all'ultima versione con i comandi seguenti:

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

Verrà richiesto di riavviare l'istanza di SQL Server. Usare il comando seguente per eseguire questa operazione.

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>Dopo l'installazione, è necessario [abilitare la funzionalità PolyBase](#enable).

## <a name="next-steps"></a>Passaggi successivi

### <a name="supported-external-data-sources-on-linux"></a>Origini dati esterne supportate in Linux

PolyBase in Linux può accedere alle origini dati seguenti. Vedere i collegamenti forniti per altre informazioni su come creare una tabella esterna da queste origini quando PolyBase è abilitato. 

- [SQL Server (e SQL DB, Azure SQL DW)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (e Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

Per altre informazioni su come usare questa funzionalità, vedere l'articolo di riferimento per Transact-SQL per [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).