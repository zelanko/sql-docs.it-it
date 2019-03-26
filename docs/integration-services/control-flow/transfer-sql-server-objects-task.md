---
title: Attività Trasferisci oggetti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 911aa8f873f43245e92b4524c1633a4e55e82a72
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277290"
---
# <a name="transfer-sql-server-objects-task"></a>Attività Trasferisci oggetti di SQL Server
  L'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasferisce uno o più tipi di oggetti di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio, tabelle e stored procedure. A seconda della versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usata come origine, sono disponibili per la copia tipi di oggetti diversi. Ad esempio, schemi e aggregati definiti dall'utente sono inclusi solo nei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="objects-to-transfer"></a>Oggetti trasferibili  
 È possibile copiare ruoli del server, ruoli e utenti del database specificato, oltre alla autorizzazioni associate agli oggetti trasferiti. La copia degli utenti, dei ruoli e delle autorizzazioni associate insieme agli oggetti consente di rendere gli oggetti trasferiti immediatamente utilizzabili nel server di destinazione.  
  
 Nella tabella seguente sono elencati i tipi di oggetti che è possibile copiare.  
  
|Object|  
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
  
 I tipi definiti dall'utente (UDT) creati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hanno dipendenze su assembly CLR (Common Language Runtime). Se si utilizza l'attività Trasferisci oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per trasferire UDT, è inoltre necessario configurarla per trasferire anche gli oggetti dipendenti. Per trasferire oggetti dipendenti, impostare la proprietà **IncludeDependentObjects** su **True**.  
  
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
 Il valore di esecuzione, archiviato nella proprietà **ExecutionValue** dell'attività, restituisce il numero degli oggetti trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà **ExecValueVariable** dell'attività Trasferisci oggetti di SQL Server, le informazioni sul trasferimento di oggetti possono essere rese disponibili anche ad altri oggetti nel pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci oggetti di SQL Server include le voci di log personalizzate seguenti:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects   Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento **OnInformation** riporta il numero di oggetti del tipo specificato selezionati per il trasferimento, il numero di oggetti trasferiti e le azioni, quale il troncamento delle tabelle, eseguite quando insieme alle tabelle vengono trasferiti anche i dati. Viene scritta una voce di log per l'evento **OnWarning** per ogni oggetto sovrascritto nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 L'utente deve disporre dell'autorizzazione per l'esplorazione degli oggetti nel server di origine e l'autorizzazione per l'eliminazione e creazione di oggetti nel server di destinazione. Deve inoltre avere accesso al database e agli oggetti di database specificati.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Configurazione dell'attività Trasferisci oggetti di SQL Server  
 È possibile configurare l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il trasferimento di tutti gli oggetti, degli oggetti di un tipo specifico o soltanto degli oggetti specificati di un determinato tipo. È possibile, ad esempio, impostare la copia solo delle tabelle selezionate nel database AdventureWorks.  
  
 Se l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasferisce tabelle, è possibile specificare i tipi di oggetti correlati alle tabelle da copiare insieme alle tabelle. È possibile, ad esempio, specificare che insieme alle tabelle vengano copiate le chiavi primarie.  
  
 Per migliorare ulteriormente la funzionalità degli oggetti trasferiti, è possibile configurare l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo da includere nel trasferimento i nomi degli schemi, i dati, le proprietà estese degli oggetti trasferiti e gli oggetti dipendenti. Per la copia di dati, è possibile specificare se sostituire o appendere gli eventuali dati esistenti.  
  
 In fase di esecuzione, l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si connette al server di origine e di destinazione tramite due gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che vi fa quindi riferimento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Configurazione a livello di codice dell'attività Trasferisci oggetti di SQL Server  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>Editor attività Trasferisci oggetti di SQL Server (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività Trasferisci oggetti di SQL Server** per assegnare un nome e una descrizione all'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  L'utente che crea l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre di autorizzazioni appropriate sugli oggetti del server di origine per selezionarli a scopo di copia, nonché dell'autorizzazione necessaria per accedere al database del server di destinazione in cui verranno trasferiti gli oggetti in questione.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor attività Trasferisci oggetti di SQL Server (pagina Oggetti)
  Utilizzare la pagina **Oggetti** della finestra di dialogo **Editor attività Trasferisci oggetti di SQL Server** per impostare le proprietà relative alla copia di uno o più oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra. Tabelle, viste, stored procedure e funzioni definite dall'utente rappresentano solo alcuni esempi di oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile copiare.  
  
> [!NOTE]  
>  L'utente che crea l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre di autorizzazioni sufficienti per gli oggetti del server di origine per selezionarli e copiarli, nonché dell'autorizzazione per l'accesso al database del server di destinazione in cui gli oggetti verranno trasferiti.  
  
### <a name="static-options"></a>Opzioni statiche  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **SourceDatabase**  
 Consente di selezionare un database nel server di origine dal quale verranno copiati gli oggetti.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **DestinationDatabase**  
 Consente di selezionare un database nel server di destinazione nel quale verranno copiati gli oggetti.  
  
 **DropObjectsFirst**  
 Consente di indicare se gli oggetti selezionati verranno eliminati nel server di destinazione prima della copia.  
  
 **IncludeExtendedProperties**  
 Consente di indicare se le proprietà estese devono essere incluse nella copia degli oggetti dal server di origine a quello di destinazione.  
  
 **CopyData**  
 Consente di indicare se i dati devono essere inclusi nella copia degli oggetti dal server di origine a quello di destinazione.  
  
 **ExistingData**  
 Consente di specificare la modalità di copia dei dati nel server di destinazione. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Sostituisci**|I dati nel server di destinazione verranno sovrascritti.|  
|**Accoda**|I dati copiati dal server di origine verranno accodati a quelli esistenti nel server di destinazione.|  
  
> [!NOTE]  
>  L'opzione **ExistingData** è disponibile solo se **CopyData** è impostata su **True**.  
  
 **CopySchema**  
 Consente di indicare se lo schema deve essere copiato durante l'attività Trasferisci oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  **CopySchema** è disponibile solo per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UseCollation**  
 Consente di indicare se il trasferimento degli oggetti deve includere le regole di confronto specificate nel server di origine.  
  
 **IncludeDependentObjects**  
 Consente di indicare se la copia degli oggetti selezionati deve essere propagata in modo da includere eventuali oggetti dipendenti da quelli selezionati.  
  
 **CopyAllObjects**  
 Consente di indicare se, durante l'attività, devono essere copiati tutti gli oggetti nel database di origine specificato o solo quelli selezionati.  Se questa opzione viene impostata su False, è possibile selezionare gli oggetti da trasferire e vengono visualizzate le opzioni dinamiche nella sezione **CopyAllObjects**.  
  
 **ObjectsToCopy**  
 Espandere **ObjectsToCopy** per specificare quali oggetti devono essere copiati dal database di origine a quello di destinazione.  
  
> [!NOTE]  
>  **ObjectsToCopy** è disponibile solo se **CopyAllObjects** è impostata su **False**.  
  
 Le opzioni per la copia dei tipi di oggetti seguenti sono supportate solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 Assembly  
  
 Funzioni di partizione  
  
 Schemi di partizione  
  
 Schemi  
  
 Funzioni di aggregazione definite dall'utente  
  
 Tipi definiti dall'utente  
  
 Raccolte di XML Schema  
  
 **CopyDatabaseUsers**  
 Consente di indicare se gli utenti del database devono essere inclusi nel trasferimento.  
  
 **CopyDatabaseRoles**  
 Consente di indicare se i ruoli del database devono essere inclusi nel trasferimento.  
  
 **CopySqlServerLogins**  
 Consente di indicare se gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere inclusi nel trasferimento.  
  
 **CopyObjectLevelPermissions**  
 Consente di indicare se le autorizzazioni a livello di oggetto devono essere incluse nel trasferimento.  
  
 **CopyIndexes**  
 Consente di indicare se gli indici devono essere inclusi nel trasferimento.  
  
 **CopyTriggers**  
 Consente di indicare se i trigger devono essere inclusi nel trasferimento.  
  
 **CopyFullTextIndexes**  
 Consente di indicare se gli indici full-text devono essere inclusi nel trasferimento.  
  
 **CopyPrimaryKeys**  
 Consente di indicare se le chiavi primarie devono essere incluse nel trasferimento.  
  
 **CopyForeignKeys**  
 Consente di indicare se le chiavi esterne devono essere incluse nel trasferimento.  
  
 **GenerateScriptsInUnicode**  
 Consente di indicare se gli script di trasferimento generati sono in formato Unicode.  
  
### <a name="dynamic-options"></a>Opzioni dinamiche  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le tabelle nel database di origine specificato o solo le tabelle selezionate.  
  
 **TablesList**  
 Fare clic per aprire la finestra di dialogo **Selezione tabelle** .  
  
 **CopyAllViews**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le viste nel database di origine specificato o solo quelle selezionate.  
  
 **ViewsList**  
 Fare clic per aprire la finestra di dialogo **Selezione viste** .  
  
 **CopyAllStoredProcedures**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le stored procedure definite dall'utente nel database di origine specificato o solo le stored procedure selezionate.  
  
 **StoredProceduresList**  
 Fare clic per aprire la finestra di dialogo **Selezione stored procedure** .  
  
 **CopyAllUserDefinedFunctions**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le funzioni definite dall'utente nel database di origine specificato o solo le funzioni selezionate.  
  
 **UserDefinedFunctionsList**  
 Fare clic per aprire la finestra di dialogo **Selezione funzioni definite dall'utente** .  
  
 **CopyAllDefaults**  
 Consente di indicare se, durante l'attività, verranno copiati tutti i valori predefiniti nel database di origine specificato o solo i valori predefiniti selezionati.  
  
 **DefaultsList**  
 Fare clic per aprire la finestra di dialogo **Selezione valori predefiniti** .  
  
 **CopyAllUserDefinedDataTypes**  
 Consente di indicare se, durante l'attività, verranno copiati tutti i tipi di dati definiti dall'utente nel database di origine specificato o solo i tipi selezionati.  
  
 **UserDefinedDataTypesList**  
 Fare clic per aprire la finestra di dialogo **Selezione tipi di dati definiti dall'utente** .  
  
 **CopyAllPartitionFunctions**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le partizioni definite dall'utente nel database di origine specificato o solo le partizioni selezionate. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionFunctionsList**  
 Fare clic per aprire la finestra di dialogo **Selezione funzioni di partizione** .  
  
 **CopyAllPartitionSchemes**  
 Consente di indicare se, durante l'attività, verranno copiati tutti gli schemi di partizione nel database di origine specificato o solo gli schemi selezionati. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **PartitionSchemesList**  
 Fare clic per aprire la finestra di dialogo **Selezione schemi di partizione** .  
  
 **CopyAllSchemas**  
 Consente di indicare se, durante l'attività, verranno copiati tutti gli schemi nel database di origine specificato o solo quelli selezionati. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SchemasList**  
 Fare clic per aprire la finestra di dialogo **Seleziona schemi** .  
  
 **CopyAllSqlAssemblies**  
 Consente di indicare se, durante l'attività, verranno copiati tutti gli assembly SQL nel database di origine specificato o solo quelli selezionati. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SqlAssembliesList**  
 Fare clic per aprire la finestra di dialogo **Select SQL Assemblies** (Selezione assembly SQL).  
  
 **CopyAllUserDefinedAggregates**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le funzioni di aggregazione definite dall'utente nel database di origine specificato o solo le funzioni selezionate. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedAggregatesList**  
 Fare clic per aprire la finestra di dialogo **Selezione funzioni di aggregazione definite dall'utente** .  
  
 **CopyAllUserDefinedTypes**  
 Consente di indicare se, durante l'attività, verranno copiati tutti i tipi definiti dall'utente nel database di origine specificato o solo quelli selezionati. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **UserDefinedTypes**  
 Fare clic per aprire la finestra di dialogo **Selezione tipi definiti dall'utente** .  
  
 **CopyAllXmlSchemaCollections**  
 Consente di indicare se, durante l'attività, verranno copiate tutte le raccolte di XML Schema nel database di origine specificato o solo le raccolte di XML Schema selezionate. Opzione supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **XmlSchemaCollectionsList**  
 Fare clic per aprire la finestra di dialogo **Selezionare le raccolte XML Schema** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci oggetti di SQL Server &#40;pagina Generale&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)   
 [Formati di dati per l'importazione o l'esportazione in blocco &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
