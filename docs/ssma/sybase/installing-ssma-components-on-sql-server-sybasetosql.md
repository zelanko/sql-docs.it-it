---
title: Installazione di componenti SSMA in SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6121c75390e7493052a16b2e898eac69283e41ec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294564"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Installazione di componenti SSMA in SQL Server (SybaseToSQL)
Oltre a installare SSMA per l'uso di migrazione dei dati lato Server, è necessario installare anche i componenti nel computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e provider Sybase per abilitare la connettività server-to-server.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA per Sybase Extension Pack  
Il pacchetto di estensione SSMA consente di aggiungere i database **sysdb** e **ssmatesterdb_syb**, per l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il **sysdb** database contiene tabelle e stored procedure necessarie per la migrazione dei dati. Il **ssmatester_syb** contiene lo schema **ssma_sybase_utilities**, in cui vengono creati gli oggetti (tabelle, trigger, viste) utilizzati dal componente di tester di SSMA.  
  
Inoltre, quando si esegue la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], crea SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent i processi quando il modulo di migrazione dei dati lato server viene usato per la migrazione dei dati.  
  
### <a name="installing-the-extension-pack"></a>Installare il pacchetto di estensione  
È possibile installare qualsiasi momento prima della migrazione dei dati per il pacchetto di estensione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del ruolo del server sysadmin nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per installare il pacchetto di estensione**  
  
1.  Copiare SSMA per Sybase Extension Pack. *n*. Install.exe, dove *n* è il numero di build, al computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Fare doppio clic su SSMA per Sybase Extension Pack. *n*. Install.exe.  
  
3.  Nella pagina di benvenuto, fare clic su **successivo**.  
  
4.  Nella pagina Contratto di licenza leggere il contratto di licenza. Se si accetta, selezionare la **accetto i termini del contratto di licenza** casella di controllo e quindi fare clic su **successivo**.  
  
5.  Nella pagina Selezione tipo di installazione, fare clic su **tipica**.  
  
6.  Nella pagina pronto per installare, fare clic su **installare**.  
  
7.  Nella pagina il primo passaggio dell'installazione di completato, fare clic su **successivo**.  
  
    Verrà visualizzata una nuova finestra di dialogo, in cui si seleziona l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'installazione del pacchetto di estensione.  
  
8.  Selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui faranno la migrazione dei database di ambiente del servizio App e quindi fare clic **successivo**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e il nome dell'istanza.  
  
9. Nella pagina parametri per la connessione, selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome account di accesso e la password.  
  
10. Nella pagina di gestione Server, selezionare **installare Database Utilities** *n*, dove *n* è il numero di versione e quindi fare clic su **Avanti**.  
  
    Il **sysdb** database viene creato e le stored procedure vengono create in tale database.  
  
    Se **installare Database Tester** sia selezionata l'opzione il tester **ssmatesterdb_syb** database verrà creato.  
  
11. Per installare le utilità in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare **restituire istanze**, quindi fare clic su **successivo**. Per uscire dalla procedura guidata, fare clic **uscire**.  
  
### <a name="sql-server-database-objects"></a>Oggetti di Database SQL Server  
Dopo aver installato il pacchetto di estensione, sarà possibile vedere un **ssma_syb.bcp_migration_packages** nella tabella di **sysdb** database. Noterete anche le stored procedure seguenti:  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
Ogni volta che si esegue la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA consente di creare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente. Questi processi sono denominati **pacchetto di migrazione dati ssma_syb {GUID}** e sono visibili nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo dell'agente di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nella cartella processi.  
  
## <a name="sybase-providers"></a>Provider Sybase  
Quando si esegue la migrazione dei dati dall'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di SQL Azure, i dati viene eseguita la migrazione diretta tra l'ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure. Non passa attraverso SSMA perché questo rallenterebbe la migrazione dei dati.  
  
### <a name="installing-the-sybase-providers"></a>Installare i provider di Sybase  
Le istruzioni seguenti illustrano i passaggi di installazione di base per l'installazione di provider di Sybase. Le istruzioni esatte variano a seconda della versione del programma di installazione di Sybase.  
  
> [!IMPORTANT]  
> Prima di eseguire il programma di installazione, verificare che non si stanno violando i contratti di licenza.  
  
1.  Eseguire il programma di installazione di ASE Sybase.  
  
2.  Selezionare il programma di installazione personalizzato.  
  
3.  Nella pagina Selezione funzionalità selezionare i provider di dati ODBC, OLE DB e ADO.NET.  
  
4.  Verificare le funzionalità selezionate e quindi fare clic su **fine** per installare il provider di dati.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
