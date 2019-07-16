---
title: Installazione di SSMA per DB2 Client (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d67b52a75f3c5b2a96bf17b5ee039e08a38a5875
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989484"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Installazione di SSMA per DB2 Client (DB2ToSQL)
Il client SSMA include i file di programma che eseguono le attività seguenti:  
  
-   Connettersi a un database DB2.  
  
-   Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Convertire gli oggetti di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi.  
  
-   Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   La migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
In questo argomento fornisce i prerequisiti di installazione e istruzioni sull'installazione di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA è progettato per funzionare con DB2 su z/OS versione 9.0 e 10.0 o DB2 su LUW 9,8 e 10.1 o versioni successive e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Prima di installare SSMA, assicurarsi che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4.0 o versione successiva. Il [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] è disponibile nella versione 4.0 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto del prodotto. È inoltre possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Provider Microsoft OLEDB per DB2 versione 5 o versione successiva e la connettività ai database di DB2 che si desidera eseguire la migrazione.  
  
-   Accesso a e autorizzazioni sufficienti nel computer che ospita l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione dei dati e oggetti di database. Per altre informazioni, vedere [connessione a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
-   4 GB di RAM consigliato.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Provider Microsoft OLE DB per DB2  
Per scaricare il provider OLE DB per DB2 versione 5.0, visitare [Microsoft® SQL Server® 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295).  
  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download di SQL Server Migration Assistant](https://aka.ms/ssmafordb2).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione prima di poter installare SSMA.  
  
**Per installare il client SSMA**  
  
1.  Fare doppio clic su SSMA per DB2 *n*. Install.exe, dove *n* è il numero di build.  
  
2.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
    Se non hai installati i prerequisiti, verrà visualizzato un messaggio che indica che è necessario innanzitutto installare i componenti necessari. Assicurarsi che si sono installati tutti i prerequisiti e quindi eseguire nuovamente il programma di installazione.  
  
3.  Leggere il contratto di licenza utente finale. Se si accetta, selezionare **accetto i termini del contratto di licenza**, quindi fare clic su **successivo**.  
  
4.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per DB2.  
  
Il percorso di installazione predefinito è C:\Program Files\Microsoft SQL Server Migration Assistant per DB2.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di componenti SSMA in SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
