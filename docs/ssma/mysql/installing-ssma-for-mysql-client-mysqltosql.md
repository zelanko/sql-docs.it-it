---
title: Installazione di SSMA per il Client MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d9317b63b01a4d1e78f5c8d4818c63d9974be4f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187192"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Installazione di SSMA per il client MySQL (MySQLToSQL)
SSMA per MySQL client include i file di programma che eseguono le attività seguenti:  
  
-   Connettersi a un database MySQL.  
  
-   Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Convertire gli oggetti di database MySQL per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure.  
  
-   Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   La migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
In questo argomento fornisce i prerequisiti di installazione e istruzioni sull'installazione di SSMA per il client MySQL.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA per MySQL è progettato per funzionare con MySQL 4.1 o versioni successive e tutte le edizioni di SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 e database SQL di Azure.  
  
Prima di installare SSMA, assicurarsi che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4.0 o versione successiva. Il [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4.0 è disponibile nel supporto del prodotto SQL Server. È inoltre possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   5.1 Driver ODBC di MySQL e connettività ai database che si desidera eseguire la migrazione di MySQL. È possibile installare MySQL dal sito Web di MySQL. Per informazioni sulla connettività, vedere [connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Accesso a e autorizzazioni sufficienti nel computer che ospita l'istanza di destinazione di SQL Server in cui si eseguirà la migrazione dei dati e oggetti di database. Per altre informazioni, vedere [connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   In caso di progetti di SQL Azure, l'accesso a e autorizzazioni sufficienti per l'istanza di database SQL di Azure in cui eseguirà la migrazione di database oggetti e dati. Per altre informazioni, vedere [la connessione al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB di RAM consigliato.  
  
## <a name="installing-ssma-for-mysql-client"></a>Installazione di SSMA per il client MySQL  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download di SQL Server Migration Assistant](https://aka.ms/ssmaformysql).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.  
  
**Per installare il client SSMA**  
  
1.  Fare doppio clic su SSMA per MySQL *n*. Install.exe, dove *n* è il numero di build.  
  
2.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
    Se non hai installati i prerequisiti, verrà visualizzato un messaggio che indica che è necessario innanzitutto installare i componenti necessari. Assicurarsi di avere installato tutti i prerequisiti prima di eseguire nuovamente il programma di installazione.  
  
3.  Leggere il contratto di licenza utente finale. Se si accetta, selezionare **accetto i termini del contratto di licenza**, quindi fare clic su **successivo**.  
  
4.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per MySQL.  
  
Il percorso di installazione predefinito è C:\Program Files\Microsoft SQL Server Migration Assistant per MySQL.  
  
Nel computer Windows a 64 bit il prodotto sia installato in C:\Microsoft SQL Server Migration Assistant per MySQL.  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
