---
title: Installazione dei componenti di SSMA in SQL Server (MySQLToSql) | Microsoft Docs
description: Installare i componenti nel server che esegue SQL Server per supportare la conversione del database MySQL con SSMA, inclusi i provider di estensioni SSMA e MySQL.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 502f42a961cfbd64b0dcd6ac6c6867d0cdcf501a
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293788"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Installazione dei componenti SSMA in SQL Server (MySQLToSql)
Oltre a installare SSMA, è necessario installare anche i componenti nel computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e i provider MySQL, per abilitare la connettività da server a server.  
  
## <a name="ssma-for-mysql-extension-pack"></a>Pacchetto di estensione SSMA per MySQL  
Il pacchetto di estensione SSMA aggiunge un database, **sysdb**, all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo database contiene le tabelle e le stored procedure necessarie per eseguire la migrazione dei dati.  
  
Inoltre, quando si esegue la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , SSMA crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i processi di Agent, quando viene utilizzato il motore di migrazione dei dati lato server per la migrazione dei dati.  
  
### <a name="prerequisites"></a>Prerequisiti  
Prima di installare i componenti di SSMA per MySQL server in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verificare che il computer soddisfi i requisiti seguenti:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versione successiva.  
  
-   Il provider client MySQL e la connettività al database MySQL di cui si vuole eseguire la migrazione. È possibile installare i provider dal supporto del prodotto MySQL o dal sito web MySQL.  
  
-   Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser deve essere in esecuzione durante l'installazione. Viene utilizzato per popolare un elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell'installazione guidata di. È possibile disabilitare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser dopo l'installazione.  
  
    > [!NOTE]  
    > Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio browser è in esecuzione, ma non viene ancora visualizzato un elenco di istanze nel programma di installazione, è necessario sbloccare la porta UDP 1434. È possibile utilizzare Windows Firewall per sbloccare temporaneamente la porta oppure è possibile disabilitare temporaneamente Windows Firewall. Potrebbe anche essere necessario disabilitare temporaneamente il software antivirus. Assicurarsi di abilitare i firewall e il software antivirus dopo l'installazione.  
  
### <a name="installing-the-extension-pack"></a>Installazione del pacchetto di estensione  
È possibile installare il pacchetto di estensione in qualsiasi momento prima di eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del ruolo del server **sysadmin** nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Per installare il pacchetto di estensione**  
  
1.  Copiare SSMA per MySQL Extension Pack. *n*.Install.exe, dove *n* è il numero di build, nel computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Fare doppio clic su SSMA per MySQL Extension Pack. *n*.Install.exe.  
  
3.  Nella finestra di dialogo di benvenuto fare clic su **Avanti**.  
  
4.  Nella finestra di dialogo contratto di licenza con l'utente finale leggere il contratto di licenza. Se si accetta, selezionare la casella di controllo Accetto **i termini del contratto di licenza** , quindi fare clic su **Avanti**.  
  
5.  Nella finestra di dialogo Scegli tipo di installazione fare clic su **tipico**.  
  
6.  Nella finestra di dialogo pronto per l'installazione fare clic su **Installa**.  
  
7.  Nella finestra di dialogo completato il primo passaggio dell'installazione fare clic su **Avanti**.  
  
    Verrà visualizzata una nuova finestra di dialogo in cui è possibile selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'installazione del pacchetto di estensione.  
  
8.  Selezionare l'istanza di in cui verrà eseguita la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migrazione degli schemi MySQL e quindi fare clic su **Avanti**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e dal nome dell'istanza.  
  
9. Nella finestra di dialogo connessione selezionare il metodo di autenticazione e quindi fare clic su **Avanti**.  
  
    L'autenticazione di Windows utilizzerà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome di account di accesso e una password.  
  
10. Nella finestra di dialogo successiva selezionare **Install Utilities database** *n*, dove *n* è il numero di versione, quindi fare clic su **Avanti**.  
  
    Il database **sysdb** viene creato con le tabelle e le stored procedure necessarie per la migrazione dei dati (tramite il motore di migrazione dei dati sul lato server) in tale database.  
  
11. Per installare le utilità in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare **Sì**e quindi fare clic su **Avanti**. In alternativa, fare clic su **No**per uscire dalla procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per il client MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migrazione di database MySQL a SQL Server-database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
