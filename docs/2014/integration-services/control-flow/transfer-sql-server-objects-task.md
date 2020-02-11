---
title: Attività Trasferisci oggetti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b985a1bb818e7b3d3612596bb4e2b7fa6fd393
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62829467"
---
# <a name="transfer-sql-server-objects-task"></a>Attività Trasferisci oggetti di SQL Server
  L'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasferisce uno o più tipi di oggetti di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio, tabelle e stored procedure. A seconda della versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usata come origine, sono disponibili per la copia tipi di oggetti diversi. Ad esempio, schemi e aggregati definiti dall'utente sono inclusi solo nei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="objects-to-transfer"></a>Oggetti trasferibili  
 È possibile copiare ruoli del server, ruoli e utenti del database specificato, oltre alla autorizzazioni associate agli oggetti trasferiti. La copia degli utenti, dei ruoli e delle autorizzazioni associate insieme agli oggetti consente di rendere gli oggetti trasferiti immediatamente utilizzabili nel server di destinazione.  
  
 Nella tabella seguente sono elencati i tipi di oggetti che è possibile copiare.  
  
|Oggetto|  
|------------|  
|Tabelle|  
|Viste|  
|Stored procedure|  
|Funzioni definite dall'utente|  
|Valori predefiniti|  
|Tipi di dati definiti dall'utente|  
|Funzioni di partizione|  
|Schemi di partizione|  
|Schemi|  
|Assembly|  
|Funzioni di aggregazione definite dall'utente|  
|Tipi definiti dall'utente|  
|Raccolta di XML Schema|  
  
 I tipi definiti dall'utente (UDT) creati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hanno dipendenze su assembly CLR (Common Language Runtime). Se si utilizza l'attività Trasferisci oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per trasferire UDT, è inoltre necessario configurarla per trasferire anche gli oggetti dipendenti. Per trasferire oggetti dipendenti, impostare la proprietà `IncludeDependentObjects` su `True`.  
  
### <a name="table-options"></a>Opzioni tabella  
 Per la copia di tabelle è possibile indicare i tipi degli elementi correlati da includere nel processo di copia. Insieme alla tabella correlata è possibile copiare i tipi di elementi seguenti:  
  
-   Indici  
  
-   Trigger  
  
-   Indici full-text  
  
-   Chiavi primarie  
  
-   Chiavi esterne  
  
 È inoltre possibile indicare se lo script generato dall'attività deve essere in formato Unicode.  
  
## <a name="destination-options"></a>Opzioni destinazione  
 È possibile configurare l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo da includere nel trasferimento i nomi degli schemi, i dati, le proprietà estese degli oggetti trasferiti e gli oggetti dipendenti. Per la copia di dati, è possibile specificare se sostituire o appendere gli eventuali dati esistenti.  
  
 Alcune opzioni sono valide solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, gli schemi sono supportati solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="security-options"></a>Opzioni relative alla sicurezza  
 L'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può includere le impostazioni relative a utenti e ruoli a livello di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili nell'origine, gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le autorizzazioni per gli oggetti trasferiti. Nel trasferimento è possibile includere, ad esempio, le autorizzazioni per le tabelle trasferite.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>Trasferimento di oggetti tra istanze di SQL Server  
 L'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta un'origine e una destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività genera un evento informativo in cui è indicato il numero di oggetti trasferiti. Genera inoltre un evento di avviso quando un oggetto viene sovrascritto. Viene generato un evento informativo anche in corrispondenza di azioni quale il troncamento delle tabelle di database.  
  
 L'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non riporta lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, archiviato nella proprietà `ExecutionValue` dell'attività, restituisce il numero degli oggetti trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà `ExecValueVariable` dell'attività Trasferisci oggetti di SQL Server, le informazioni sul trasferimento di oggetti possono essere rese disponibili anche ad altri oggetti nel pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci oggetti di SQL Server include le voci di log personalizzate seguenti:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects   Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento `OnInformation` riporta il numero di oggetti del tipo specificato selezionati per il trasferimento, il numero di oggetti trasferiti e le azioni, quale il troncamento delle tabelle, eseguite quando insieme alle tabelle vengono trasferiti anche i dati. Viene scritta una voce di log per l'evento `OnWarning` per ogni oggetto sovrascritto nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 L'utente deve disporre dell'autorizzazione per l'esplorazione degli oggetti nel server di origine e l'autorizzazione per l'eliminazione e creazione di oggetti nel server di destinazione. Deve inoltre avere accesso al database e agli oggetti di database specificati.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Configurazione dell'attività Trasferisci oggetti di SQL Server  
 È possibile configurare l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il trasferimento di tutti gli oggetti, degli oggetti di un tipo specifico o soltanto degli oggetti specificati di un determinato tipo. È possibile, ad esempio, impostare la copia solo delle tabelle selezionate nel database AdventureWorks.  
  
 Se l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasferisce tabelle, è possibile specificare i tipi di oggetti correlati alle tabelle da copiare insieme alle tabelle. È possibile, ad esempio, specificare che insieme alle tabelle vengano copiate le chiavi primarie.  
  
 Per migliorare ulteriormente la funzionalità degli oggetti trasferiti, è possibile configurare l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo da includere nel trasferimento i nomi degli schemi, i dati, le proprietà estese degli oggetti trasferiti e gli oggetti dipendenti. Per la copia di dati, è possibile specificare se sostituire o appendere gli eventuali dati esistenti.  
  
 In fase di esecuzione, l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al server di origine e di destinazione tramite due gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che vi fa quindi riferimento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Trasferisci oggetti SQL Server &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Trasferisci oggetti di SQL Server &#40;pagina Oggetti&#41;](../transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Configurazione a livello di codice dell'attività Trasferisci oggetti di SQL Server  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
