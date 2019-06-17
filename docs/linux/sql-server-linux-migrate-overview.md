---
title: Eseguire la migrazione di database a SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive le diverse opzioni per la migrazione di database e i dati da SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: 2443611a63bee3f62ae8225384d79d34dfcb18e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705301"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Eseguire la migrazione di dati strutturati e i database di SQL Server in Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile migrare i database e i dati in SQL Server in esecuzione in Linux. Il metodo che si sceglie di usare dipende dai dati di origine e uno scenario specifico. Le sezioni seguenti descrivono le procedure consigliate per vari scenari di migrazione.

## <a name="migrate-from-sql-server-on-windows"></a>Eseguire la migrazione da SQL Server in Windows
Se si desidera eseguire la migrazione di database SQL Server in Windows per SQL Server in Linux, la tecnica consigliata è usare backup di SQL Server e il ripristino.

1. Creare un backup del database nel computer Windows.
2. Trasferire il file di backup nel computer di destinazione SQL Server su Linux.
3. Ripristinare il backup nella macchina Linux. 

Per un'esercitazione sulla migrazione di un database tramite backup e ripristino, vedere l'argomento seguente:

- [Ripristinare un database di SQL Server da Windows a Linux](sql-server-linux-migrate-restore-database.md).

È anche possibile esportare il database in un file BACPAC (un file compresso che contiene lo schema del database e dati). Se si dispone di un file BACPAC, è possibile trasferire il file nel computer Linux e quindi importarlo in SQL Server. Per altre informazioni, vedere i seguenti argomenti:

- [Esportare e importare un database con SSMS o SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Eseguire la migrazione da altri server di database
È possibile eseguire la migrazione di database in altri sistemi di database a SQL Server in Linux. Sono inclusi i database Microsoft Access, DB2, MySQL, Oracle e Sybase. In questo scenario, usare il SQL Server Management Assistant (SSMA) per automatizzare la migrazione a SQL Server in Linux. Per altre informazioni, vedere [uso di SSMA per la migrazione dei database di SQL Server in Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Eseguire la migrazione di dati strutturati
Esistono anche tecniche per l'importazione di dati non elaborati. Si potrebbero avere strutturati i file di dati che sono stati esportati da altri database o origini dati. In questo caso, è possibile utilizzare lo strumento bcp per l'inserimento bulk dei dati. In alternativa, è possibile eseguire SQL Server Integration Services in Windows per importare i dati in un database di SQL Server in Linux. SQL Server Integration Services consente di eseguire trasformazioni più complesse sui dati durante l'importazione. 

Per altre informazioni su queste tecniche, vedere gli argomenti seguenti:

- [Copia bulk di dati con bcp](sql-server-linux-migrate-bcp.md)
- [Estrarre, trasformare e caricare i dati per SQL Server in Linux con SSIS](sql-server-linux-migrate-ssis.md) 
