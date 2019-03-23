---
title: Connessione di SQL Server per la creazione dell'istanza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bebeec974bff46333662708952d0a8b6fa841a87
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375619"
---
# <a name="sql-server-connection-for-instance-creation"></a>Connessione di SQL Server per la creazione dell'istanza
  Uno dei primi passaggi della creazione di un'istanza di Oracle CDC consiste nella creazione di un database CDC nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione. Questo database CDC viene abilitato per SQL Server CDC. Questa operazione richiede un account di accesso che sia un membro del ruolo predefinito del server `sysadmin` .  
  
 Se un utente che avvia la procedura guidata **Create an Oracle CDC Instance** non è un membro del ruolo predefinito del server `sysadmin` , viene visualizzata la finestra di dialogo **Connect to SQL Server** e vengono richieste le credenziali per un membro del ruolo `sysadmin` per eseguire l'attività Enable the database for SQL Server CDC. Quando viene creato il database CDC, l'account di accesso `sysadmin` viene eliminato e viene ripreso l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] originale utilizzato al momento dell'accesso a Oracle Designer Console.  
  
## <a name="task-list"></a>Elenco attività  
 Immettere le informazioni riportate di seguito nella finestra di dialogo **Connect to SQL Server** .  
  
 **Nome server**  
 Digitare il nome del server in cui si trova [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Autenticazione**  
 Selezionare una delle opzioni seguenti:  
  
-   **Autenticazione di Windows**  
  
-   **Autenticazione di SQL Server**: Se si seleziona questa opzione, è necessario digitare il **account di accesso** e **Password** per l'utente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ci si connette a.  
  
 L'account di accesso deve disporre di un ruolo del database che consenta l'accesso al database MSXCDCDB. L'account di accesso deve inoltre disporre dell'accesso a eventuali database aggiuntivi in uso, in caso contrario l'utente non sarà in grado di visualizzare i dati in quei database.  
  
 **Opzioni**  
 Fare clic sulla freccia per visualizzare le opzioni disponibili da configurare. È possibile scegliere di non modificare il valore predefinito per queste opzioni. Sono disponibili le opzioni seguenti:  
  
-   **Timeout della connessione**: Digitare il tempo, in secondi, di attesa del servizio CDC per Oracle per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima che si verifichi un errore di timeout. Il valore predefinito è **15**.  
  
-   **Timeout esecuzione**: Digitare il tempo, in secondi, di attesa del servizio Windows Oracle CDC per l'esecuzione di un comando prima che si verifichi un errore di timeout. Il valore predefinito è **30**.  
  
-   **Crittografa connessione**: Selezionare **Encrypt Connection** per la comunicazione tra il servizio Oracle CDC e l'obiettivo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza utilizzando una connessione crittografata.  
  
-   **Avanzate**: Fare clic su **Advanced** e digitare eventuali proprietà di connessione aggiuntive nella finestra di dialogo Advanced Connection Properties.  
  
     Per informazioni sulla finestra di dialogo Advanced Connection Properties, vedere [Advanced Connection Properties](advanced-connection-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare il database delle modifiche di SQL Server](create-the-sql-server-change-database.md)   
 [Autorizzazioni necessarie della connessione di SQL Server per la finestra di progettazione di CDC](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
