---
title: Installazione di SSMA per il client Oracle (OracleToSQL) | Microsoft Docs
description: Informazioni sui prerequisiti di installazione per il SQL Server Migration Assistant (SSMA) per il client Oracle e su come installare.
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
manager: shamikg
ms.openlocfilehash: be5f48508c44dc456c2d19e1ff1eba985b982111
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293918"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Installazione di SSMA per il client Oracle (OracleToSQL)
Il client SSMA è costituito dai file di programma che eseguono le attività seguenti:  
  
-   Connettersi a un database Oracle.  
  
-   Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Convertire gli oggetti di database Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Syntax.  
  
-   Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
In questo argomento vengono forniti i prerequisiti e le istruzioni per l'installazione di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti  
SSMA è progettato per funzionare con Oracle 9 o versioni successive e tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Prima di installare SSMA, verificare che il computer soddisfi i requisiti seguenti:  
  
-   Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versione successiva.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Versione 4,0 o successiva. La [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versione 4,0 è disponibile sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto del prodotto. È anche possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Oracle client 9,0 o versione successiva e connettività ai database Oracle di cui si vuole eseguire la migrazione. La versione del client Oracle deve essere della stessa versione di o di una versione successiva alla versione del database Oracle.  
  
    È possibile installare il client Oracle dal supporto del prodotto Oracle o dal sito Web Oracle. Per informazioni sulla connettività, vedere [connessione a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Accesso a e autorizzazioni sufficienti per il computer che ospita l'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione di dati e oggetti di database. Per ulteriori informazioni, vedere [connessione a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB di RAM consigliata.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Installazione di SSMA per il client Oracle  
SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download SQL Server Migration Assistant](https://aka.ms/ssmafororacle).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione da prima di poter installare SSMA.  
  
**Per installare il client di SSMA**  
  
1.  Fare doppio clic su SSMA per Oracle *n*.Install.exe, dove *n* è il numero di Build.  
  
2.  Nella pagina di benvenuto fare clic su **Avanti**.  
  
    Se i prerequisiti non sono installati, verrà visualizzato un messaggio che indica che è necessario prima installare i componenti necessari. Assicurarsi di aver installato tutti i prerequisiti, quindi eseguire di nuovo il programma di installazione.  
  
3.  Leggere il contratto di licenza con l'utente finale. Se si accettano le condizioni, selezionare Accetto **i termini del contratto di licenza**e quindi fare clic su **Avanti**.  
  
4.  Nella pagina Selezione tipo di installazione fare clic su **tipico**.  
  
5.  Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1.  Prima di installare la nuova versione, disinstallare tutte le versioni precedenti di SSMA per Oracle.  
  
Il percorso di installazione predefinito è C:\Programmi\Microsoft SQL Server Migration Assistant per Oracle.  
  
Oltre ai file di programma SSMA, è necessario installare anche SSMA per Oracle Extension Pack in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni, vedere [installazione dei componenti SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Installazione dei componenti di SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
