---
title: Connessione a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 09d597cb7776362c44ca53e8d544f66608d8d37c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62837001"
---
# <a name="connection-to-sql-server"></a>Connessione a SQL Server
  Quando si tenta di creare un'istanza di Oracle CDC con un account di accesso senza un ruolo del database che include l'autorizzazione di scrittura (ad esempio il ruolo **db_owner** ) per il database MSXDBCDC, viene visualizzata la finestra di dialogo Connetti a SQL Server.  
  
 In questa finestra di dialogo è necessario immettere le credenziali per un account di accesso con autorizzazione di scrittura per il database MSXDBCDC, ad esempio il ruolo del database **db_owner** , per creare la nuova istanza di Oracle CDC.  
  
 Immettere le informazioni riportate di seguito nella finestra di dialogo Connect to SQL Server.  
  
### <a name="server-name"></a>Server Name  
 Digitare il nome del server in cui si trova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Authentication  
 Selezionare uno degli elementi seguenti:  
  
-   Autenticazione di Windows  
  
-   **Autenticazione di SQL Server**: se si seleziona questa opzione, è necessario digitare **Login** e **Password** per l'utente nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si esegue la connessione.  
  
### <a name="options"></a>Opzioni  
 Fare clic sulla freccia per visualizzare le opzioni disponibili da configurare. È possibile scegliere di non modificare il valore predefinito per queste opzioni. Sono disponibili le opzioni seguenti:  
  
-   **Timeout connessione**: digitare il tempo, in secondi, di attesa del programma per la connessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da stabilire prima che venga generato un errore di timeout. Il valore predefinito è **15**.  
  
-   **Timeout esecuzione**: digitare il tempo, in secondi, di attesa del programma per l'esecuzione del comando SQL da terminare prima che venga generato un errore di timeout. Il valore predefinito è **30**.  
  
-   **Crittografa connessione**: selezionare **Crittografa connessione** per assicurare che la connessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da stabilire venga crittografata per garantire la privacy.  
  
-   **Advanced**: fare clic su **Advanced** e digitare eventuali proprietà di connessione aggiuntive nella finestra di dialogo Advanced Connection Properties, se necessario.  
  
## <a name="see-also"></a>Vedere anche  
 [Autorizzazioni necessarie per la connessione a SQL per il servizio CDC](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
