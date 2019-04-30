---
title: Installazione di SSMA per il Client Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 27e5c0ef0c834806351bda73eb69dbe783d78db2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223574"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Installazione di SSMA per il client Oracle (OracleToSQL)
Il client SSMA include i file di programma che eseguono le attività seguenti:  
  
-   Connettersi a un database Oracle.  
  
-   Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Convertire gli oggetti di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi.  
  
-   Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   La migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
In questo argomento fornisce i prerequisiti di installazione e istruzioni sull'installazione di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA è progettato per funzionare con Oracle 9 o versioni successive e tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Prima di installare SSMA, assicurarsi che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4.0 o versione successiva. Il [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] è disponibile nella versione 4.0 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto del prodotto. È inoltre possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Client Oracle 9.0 o versione successiva e la connettività ai database di Oracle che vuoi eseguire la migrazione. La versione del client Oracle deve essere la stessa versione o una versione successiva, la versione del database Oracle.  
  
    È possibile installare il Client Oracle dal supporto del prodotto Oracle o dal sito Web Oracle. Per informazioni sulla connettività, vedere [connessione a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Accesso a e autorizzazioni sufficienti nel computer che ospita l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione dei dati e oggetti di database. Per altre informazioni, vedere [connessione a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB di RAM consigliato.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Installazione di SSMA per Oracle Client  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download di SQL Server Migration Assistant](https://aka.ms/ssmafororacle).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.  
  
**Per installare il client SSMA**  
  
1.  Fare doppio clic su SSMA per Oracle *n*. Install.exe, dove *n* è il numero di build.  
  
2.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
    Se non hai installati i prerequisiti, verrà visualizzato un messaggio che indica che è necessario innanzitutto installare i componenti necessari. Assicurarsi che si sono installati tutti i prerequisiti e quindi eseguire nuovamente il programma di installazione.  
  
3.  Leggere il contratto di licenza utente finale. Se si accetta, selezionare **accetto i termini del contratto di licenza**, quindi fare clic su **successivo**.  
  
4.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per Oracle.  
  
Il percorso di installazione predefinito è C:\Program Files\Microsoft SQL Server Migration Assistant per Oracle.  
  
Oltre ai file di programma SSMA, è necessario anche installare SSMA per il pacchetto di estensioni di Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [installazione dei componenti SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di componenti SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
