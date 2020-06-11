---
title: Installazione di SSMA per il client SAP ASE (SybaseToSQL) | Microsoft Docs
description: Informazioni sui prerequisiti di installazione per SQL Server Migration Assistant (SSMA) per SAP Adaptive Server Enterprise (ASE) e su come installare.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1325e9ba882bed76ecfc1b11f8ca1c379ca74bb4
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306250"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>Installazione di SSMA per il client SAP ASE (SybaseToSQL)

Il client SSMA è costituito dai file di programma usati per connettersi a un server di database di SAP Adaptive Server Enterprise (ASE) e a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o al database SQL di Azure, convertire gli oggetti di database dell'ambiente del servizio app in o la sintassi del database SQL di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure, caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel database SQL di Azure e quindi migrare i dati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database SQL di Azure  
  
In questo argomento vengono forniti i prerequisiti e le istruzioni per l'installazione di SSMA.  
  
## <a name="prerequisites"></a>Prerequisiti

SSMA è progettato per funzionare con l'ambiente del servizio app 11.9.2 o versioni successive e tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Prima di installare SSMA, verificare che il computer soddisfi i requisiti seguenti:  
  
- Windows 7 o versioni successive o Windows Server 2008 o versioni successive.  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versione successiva.  
- Il [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versione 4,0 o successiva. Il .NET Framework versione 4,0 è disponibile sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporto del prodotto. È anche possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
- Provider OLEDB/ADO.Net/ODBC Sybase e connettività al server di database Sybase ASE che contiene i database di cui si desidera eseguire la migrazione. È possibile installare i provider dal supporto del prodotto Sybase ASE. Per informazioni sulla connettività, vedere [connessione a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
- Accesso a e autorizzazioni sufficienti per il computer che ospita l'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione di dati e oggetti di database. Per altre informazioni, vedere [connessione a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)la / [connessione al database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
- 4 GB di RAM consigliata.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Installazione di SSMA per il client Sybase

SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download SQL Server Migration Assistant](https://aka.ms/ssmaforsybase).  
  
Dopo aver scaricato la versione più recente, è necessario estrarre i file di installazione da prima di poter installare SSMA.  
  
**Per installare il client di SSMA**
  
1. Fare doppio clic su SSMA per Sybase *n*.Install.exe, dove *n* è il numero di Build.  
  
2. Nella pagina di benvenuto fare clic su **Avanti**.  
  
    Se i prerequisiti non sono installati, verrà visualizzato un messaggio che indica che è necessario prima installare i componenti necessari. Assicurarsi di aver installato tutti i prerequisiti, quindi eseguire di nuovo il programma di installazione.  
  
3. Leggere il contratto di licenza con l'utente finale. Se si accettano le condizioni, selezionare Accetto **i termini del contratto di licenza**e quindi fare clic su **Avanti**.  
  
4. Nella pagina Selezione tipo di installazione fare clic su **tipico**.  
  
5. Fare clic su **Installa**.  
  
> [!IMPORTANT]  
> 1. Disinstallare tutte le versioni precedenti di SSMA per Sybase prima di installare la nuova versione.
  
Il percorso di installazione predefinito è C:\Programmi\Microsoft SQL Server Migration Assistant per Sybase.  
  
Oltre ai file di programma SSMA, è necessario installare anche SSMA per Sybase Extension Pack in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni, vedere [installazione dei componenti SSMA in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche

[Installazione dei componenti di SSMA in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrazione dei database Sybase ASE a SQL Server-database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
