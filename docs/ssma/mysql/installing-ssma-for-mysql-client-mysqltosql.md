---
title: Installazione di SSMA per il client MySQL (MySQLToSQL) | Microsoft Docs
description: Informazioni sui prerequisiti di installazione per il SQL Server Migration Assistant (SSMA) per il client MySQL e su come installare.
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
ms.openlocfilehash: bf1a3c8c5a01bb2553f773d5b650805667c116a3
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293898"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Installazione di SSMA per il client MySQL (MySQLToSQL)
Il client SSMA per MySQL è costituito dai file di programma che eseguono le attività seguenti:  
  
-   Connettersi a un database MySQL.  
  
-   Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Convertire gli oggetti di database MySQL negli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti o SQL Azure.  
  
-   Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
Questo argomento illustra i prerequisiti di installazione e le istruzioni per l'installazione di SSMA per il client MySQL.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA per MySQL è progettato per funzionare con MySQL 4,1 o versioni successive e tutte le edizioni di SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 e il database SQL di Azure.  
  
Prima di installare SSMA, verificare che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versione successiva.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Versione 4,0 o successiva. La [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4,0 è disponibile sul supporto del prodotto SQL Server. È anche possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Driver MySQL ODBC 5,1 e connettività ai database MySQL di cui si vuole eseguire la migrazione. È possibile installare MySQL dal sito web MySQL. Per informazioni sulla connettività, vedere la pagina relativa [alla connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Accesso a e autorizzazioni sufficienti per il computer che ospita l'istanza di destinazione di SQL Server in cui si eseguirà la migrazione di dati e oggetti di database. Per ulteriori informazioni, vedere [connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   In caso di SQL Azure progetti, accedere a e a autorizzazioni sufficienti per l'istanza del database SQL di Azure in cui si eseguirà la migrazione di dati e oggetti di database. Per altre informazioni, vedere [connessione al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB di RAM consigliata.  
  
## <a name="installing-ssma-for-mysql-client"></a>Installazione di SSMA per il client MySQL  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download SQL Server Migration Assistant](https://aka.ms/ssmaformysql).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.  
  
**Per installare il client di SSMA**  
  
1.  Fare doppio clic su SSMA per MySQL *n*.Install.exe, dove *n* è il numero di Build.  
  
2.  Nella pagina di benvenuto fare clic su **Avanti**.  
  
    Se i prerequisiti non sono installati, verrà visualizzato un messaggio che indica che è necessario prima installare i componenti necessari. Assicurarsi di aver installato tutti i prerequisiti prima di eseguire di nuovo il programma di installazione.  
  
3.  Leggere il contratto di licenza con l'utente finale. Se si accettano le condizioni, selezionare Accetto **i termini del contratto di licenza**e quindi fare clic su **Avanti**.  
  
4.  Nella pagina Selezione tipo di installazione fare clic su **tipico**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Disinstallare tutte le versioni precedenti di SSMA per MySQL prima di installare la nuova versione.  
  
Il percorso di installazione predefinito è C:\Programmi\Microsoft SQL Server Migration Assistant per MySQL.  
  
Nel computer Windows a 64 bit il prodotto viene installato in C:\Programmi\Microsoft SQL Server Migration Assistant per MySQL.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database MySQL a SQL Server-database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
