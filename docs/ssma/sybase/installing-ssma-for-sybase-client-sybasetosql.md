---
title: Installazione di SSMA per Sybase Client (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cca10f2a54a70e91e46bb8b98e9799885b5f175
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740991"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Installazione di SSMA per Sybase Client (SybaseToSQL)
Il client SSMA è costituito da file di programma vengono utilizzati per connettersi a un server di database di Sybase Adaptive Server Enterprise (ASE) e un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, convertire gli oggetti di database di ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di database SQL di Azure, caricare il gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, quindi eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
In questo argomento fornisce i prerequisiti di installazione e istruzioni sull'installazione di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA è progettato per funzionare con ambiente del servizio App 11.9.2 o versioni successive e tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Prima di installare SSMA, assicurarsi che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versione 4.0 o versione successiva. È disponibile in .NET Framework versione 4.0 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto del prodotto. È inoltre possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Il provider Sybase OLEDB/ADO.Net/ODBC e connettività al server di database Sybase ASE che contiene i database da migrare. È possibile installare i provider dal supporto del prodotto di Sybase ASE. Per informazioni sulla connettività, vedere [la connessione a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Accesso a e autorizzazioni sufficienti nel computer che ospita l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione dei dati e oggetti di database. Per altre informazioni, vedere [connessione a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[la connessione al database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB di RAM consigliato.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Installazione di SSMA per Sybase Client  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download di SQL Server Migration Assistant](https://aka.ms/ssmaforsybase).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.  
  
**Per installare il client SSMA**  
  
1.  Fare doppio clic su SSMA per Sybase *n*. Install.exe, dove *n* è il numero di build.  
  
2.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
    Se non hai installati i prerequisiti, verrà visualizzato un messaggio che indica che è necessario innanzitutto installare i componenti necessari. Assicurarsi che si sono installati tutti i prerequisiti e quindi eseguire nuovamente il programma di installazione.  
  
3.  Leggere il contratto di licenza utente finale. Se si accetta, selezionare **accetto i termini del contratto di licenza**, quindi fare clic su **successivo**.  
  
4.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per Sybase.  
  
Il percorso di installazione predefinito è C:\Program Files\Microsoft SQL Server Migration Assistant per Sybase.  
  
Oltre ai file di programma SSMA, è anche necessario installare SSMA per Sybase Extension Pack su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [installazione dei componenti SSMA in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di componenti SSMA in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
