---
title: Esportare e importare un database in Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: f99ff799ec91ea455cc37bd994c8555330a8ff0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105548"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Esportare e importare un database in Linux con SQL Server Management Studio o SqlPackage.exe su Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come usare [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) e [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) per esportare e importare un database in SQL Server in Linux. SQL Server Management Studio e SqlPackage.exe sono applicazioni di Windows, quindi usare questa tecnica quando si dispone di un computer Windows che può connettersi a un'istanza remota di SQL Server in Linux.

È sempre necessario installare e usare la versione più recente di SQL Server Management Studio (SSMS) come descritto in [usare SSMS in Windows per connettersi a SQL Server in Linux](sql-server-linux-manage-ssms.md)

> [!NOTE]
> Se si esegue la migrazione di un database da un'istanza di SQL Server a un altro, è consigliabile usare [Backup e ripristino](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Esportare un database con SSMS

1. Avviare SSMS digitare **Microsoft SQL Server Management Studio** in Windows la casella di ricerca e quindi fare clic sull'app desktop.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Connettersi al database di origine in Esplora oggetti. Il database di origine può essere in Microsoft SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker e Database SQL di Azure o Azure SQL Data Warehouse.

3. Fare doppio clic su database di origine in Esplora oggetti, scegliere **attività**, fare clic su **Esporta applicazione livello dati...**

4. Nell'esportazione guidata, fare clic su **successivo**e quindi scegliere il **impostazioni** , configurare l'esportazione per salvare il file BACPAC su un percorso disco locale o in un blob di Azure.

5. Per impostazione predefinita, vengono esportati tutti gli oggetti nel database. Scegliere il **scheda Avanzate** e scegliere gli oggetti di database che si desiderano esportare.

6. Fare clic su **Avanti** , quindi su **Fine**.

Il *. File BACPAC viene creato in corrispondenza della posizione che scelta e si è pronti per l'importazione in un database di destinazione.

## <a name="import-a-database-with-ssms"></a>Importare un database con SSMS

1. Avviare SSMS digitare **Microsoft SQL Server Management Studio** in Windows la casella di ricerca e quindi fare clic sull'app desktop.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Connettersi al server di destinazione in Esplora oggetti. Il server di destinazione può essere Microsoft SQL Server in esecuzione in locale o nel cloud, in Linux, Windows o Docker e Database SQL di Azure o Azure SQL Data Warehouse.

3. Fare doppio clic il **database** cartella in Esplora oggetti e fare clic su **Importa applicazione livello dati...**

4. Per creare il database nel server di destinazione, specificare un file BACPAC dal disco locale oppure selezionare l'account di archiviazione di Azure e il contenitore a cui è stato caricato il file BACPAC.

5. Specificare il nuovo nome di database per il database. Se si importa un database in Database SQL di Azure, impostare l'edizione di Microsoft Azure SQL Database (livello di servizio), massime del database e l'obiettivo di servizio (livello di prestazioni).

6. Fare clic su **successivo** e quindi fare clic su **fine** per importare il file BACPAC in un nuovo database nel server di destinazione.

Il *. File BACPAC viene importato per creare un nuovo database nel server di destinazione specificato.

## <a id="sqlpackage"></a> Opzione della riga di comando SqlPackage

È anche possibile usare lo strumento della riga di comando di SQL Server Data Tools (SSDT), [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)per esportare e importare file BACPAC.

Il comando seguente esporta un file BACPAC:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Usare il comando seguente per importare i dati dello schema e utente database da una. File BACPAC:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Vedere anche
Per altre informazioni su come usare SQL Server Management Studio, vedere [usano SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Per altre informazioni su SqlPackage.exe, vedere la [documentazione di riferimento SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx).
