---
title: Attività Trasferisci database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ddf838269932c19b0614d5a5219a7f03daed17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62830150"
---
# <a name="transfer-database-task"></a>Attività Trasferisci database
  L'attività Trasferisci database trasferisce un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A differenza di altre attività che trasferiscono oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo eseguendone una copia, l'attività Trasferisci database può copiare o spostare un database. Tramite questa attività è inoltre possibile copiare un database all'interno dello stesso server.  
  
## <a name="offline-and-online-modes"></a>Modalità offline e online  
 Il database può essere trasferito in modalità online o offline. Nella modalità online il database rimane collegato e viene trasferito tramite SQL Management Object (SMO) per la copia degli oggetti di database. Nella modalità offline il database viene scollegato, i corrispondenti file vengono copiati o spostati e il database viene quindi collegato alla destinazione dopo essere stato trasferito correttamente. Se il database viene copiato, viene ricollegato automaticamente all'origine, quando la copia ha esito positivo. Nella modalità offline la copia del database viene eseguita più rapidamente, ma durante il trasferimento il database non è disponibile agli utenti.  
  
 Quando si utilizza la modalità offline, è necessario specificare le condivisioni file di rete del server di origine e di destinazione in cui si trovano i file di database. Se la cartella è condivisa e accessibile dall'utente, è possibile fare riferimento alla condivisione di rete in base alla sintassi \\\nomecomputer\Programmi\cartellapersonale\\. In caso contrario, è necessario adottare la sintassi \\\nomecomputer\c$\Programmi\cartellapersonale\\. Per poter utilizzare questa seconda sintassi, l'utente deve disporre dell'accesso in scrittura alle condivisioni di rete nell'origine e nella destinazione.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Trasferimento di database tra versioni di SQL Server  
 L'attività Trasferisci database consente di trasferire un database tra istanze di versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci database non visualizza lo stato incrementale del trasferimento di messaggi di errore, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà `ExecutionValue` dell'attività, restituisce il valore 1, in quanto a differenza di altre attività di trasferimento, l'attività Trasferisci database può trasferire un solo database.  
  
 Tramite l'assegnazione di una variabile definita dall'utente alla proprietà `ExecValueVariable` dell'attività, le informazioni sul trasferimento dei messaggi di errore possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci database include le voci di log personalizzate seguenti:  
  
-   SourceSQLServer    Indica il nome del server di origine.  
  
-   DestSQLServer    Indica il nome del server di destinazione.  
  
-   SourceDB    Indica il nome del database trasferito.  
  
 Viene scritta inoltre una voce di log per l'evento `OnInformation` quando il database di destinazione viene sovrascritto.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 Per poter trasferire un database in modalità offline, l'utente che esegue il pacchetto deve essere membro del ruolo del server _sysadmin.  
  
 Per poter trasferire un database in modalità online, l'utente che esegue il pacchetto deve essere membro del ruolo del server sysadmin o il proprietario (dbo) del database selezionato.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configurazione dell'attività Trasferisci database  
 È possibile specificare se, in caso di trasferimento non riuscito, deve essere eseguito un altro tentativo di collegamento del database di origine.  
  
 È inoltre possibile configurare l'attività Trasferisci database in modo da consentire la sovrascrittura di un database di destinazione avente lo stesso nome.  
  
 Il database di origine può essere inoltre rinominato durante il processo di trasferimento. Se si desidera trasferire un database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è presente un database avente lo stesso nome, per consentire il trasferimento è necessario rinominare il database di origine. È tuttavia necessario che anche i nomi dei file di database siano diversi. Se hanno lo stesso nome di altri file presenti nella destinazione, l'attività ha esito negativo.  
  
 Quando si copia un database, le dimensioni del database non possono essere inferiori alle dimensioni del database **model** sul server di destinazione. È possibile incrementare le dimensioni del database da copiare oppure ridurre le dimensioni di **model**.  
  
 In fase di esecuzione, l'attività Trasferisci database si connette ai server di origine e di destinazione utilizzando una o più gestioni connessioni SMO. Quando si crea la copia di un database nello stesso server, è richiesta una sola gestione connessione SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci database, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare durante l'accesso dell'attività al server. Per altre informazioni, vedere [Gestione connessione file](../connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Trasferisci database &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Trasferisci database &#40;pagina database&#41;](../transfer-database-task-editor-databases-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configurazione a livello di codice dell'attività Trasferisci database  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
