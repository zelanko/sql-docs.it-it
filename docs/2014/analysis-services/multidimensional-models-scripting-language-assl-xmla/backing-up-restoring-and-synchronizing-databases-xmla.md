---
title: Backup, ripristino e sincronizzazione di database (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702274"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Backup, ripristino e sincronizzazione di database (XMLA)
  In XML for Analysis sono disponibili i tre comandi seguenti per l'esecuzione del backup, del ripristino e della sincronizzazione dei database:  
  
-   Il [comando backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) esegue il backup di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un database utilizzando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un file di backup (con estensione abf), come descritto nella sezione backup dei [database](#backing_up_databases).  
  
-   Tramite il comando [Restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) viene ripristinato un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database da un file con estensione abf, come descritto nella sezione [ripristino dei database](#restoring_databases).  
  
-   Il comando [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) sincronizza un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database con i dati e i metadati di un altro database, come descritto nella sezione sincronizzazione dei [database](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a>Esecuzione del backup dei database  
 Come indicato in precedenza, il comando `Backup` consente di eseguire il backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificato in un file di backup. Al comando `Backup` sono associate varie proprietà che consentono di specificare il database di cui eseguire il backup, il file di backup da utilizzare, le modalità di esecuzione del backup delle definizioni di sicurezza e le partizioni remote di cui eseguire il backup.  
  
> [!IMPORTANT]  
>  L'account del servizio Analysis Services deve disporre delle autorizzazioni per scrivere nel percorso di backup specificato per ogni file. L'utente deve inoltre avere uno dei ruoli seguenti: ruolo di amministratore per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) per il database di cui eseguire il backup.  
  
### <a name="specifying-the-database-and-backup-file"></a>Specifica del database e del file di backup  
 Per specificare il database di cui eseguire il backup, impostare la proprietà dell' [oggetto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) del `Backup` comando. La proprietà `Object` deve contenere un identificatore di oggetto per un database. In caso contrario, si verifica un errore.  
  
 Per specificare il file che deve essere creato e usato dal processo di backup, impostare la proprietà [file](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) del `Backup` comando. La proprietà `File` deve essere impostata su un percorso UNC e su un nome di file relativi al file di backup da creare.  
  
 Oltre a indicare il file da utilizzare per il backup, per il file di backup specificato è possibile impostare le opzioni seguenti:  
  
-   Se si imposta la proprietà [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) su true, il `Backup` comando sovrascrive il file di backup se il file specificato esiste già. Se invece si imposta la proprietà `AllowOverwrite` su false, qualora il file di backup esista già si verifica un errore.  
  
-   Se si imposta la proprietà [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) su true, il file di backup viene compresso dopo la creazione del file.  
  
-   Se si imposta la proprietà [password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) su un valore non vuoto, il file di backup viene crittografato utilizzando la password specificata.  
  
    > [!IMPORTANT]  
    >  Se le proprietà `ApplyCompression` e `Password` non vengono specificate, nel file di backup i nomi utente e le password contenuti nelle stringhe di connessione vengono archiviati in testo non crittografato. I dati archiviati in testo non crittografato possono essere recuperati. Per aumentare la sicurezza, utilizzare le impostazioni relative a `ApplyCompression` e `Password` sia per comprimere che per crittografare il file di backup.  
  
### <a name="backing-up-security-settings"></a>Backup delle impostazioni di sicurezza  
 La proprietà di [sicurezza](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina se `Backup` il comando esegue il backup delle definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un database. La proprietà `Security` determina inoltre se nel file di backup vengono inclusi gli account utente e i gruppi di Windows definiti come membri delle definizioni di sicurezza.  
  
 Il valore della proprietà `Security` è limitato a una delle stringhe elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel file di backup le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel file di backup le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal file di backup.|  
  
### <a name="backing-up-remote-partitions"></a>Backup di partizioni remote  
 Per eseguire il backup delle partizioni remote [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nel database, impostare la proprietà [backupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) del `Backup` comando su true. In questo modo il comando `Backup` crea un file di backup remoto per ogni origine dati remota utilizzata per archiviare partizioni remote per il database.  
  
 Per ogni origine dati remota di cui eseguire il `Backup` backup, è possibile specificare il file di backup corrispondente includendo un elemento [location](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) nella proprietà [locations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) del comando. L' `Location` elemento deve avere la `File` proprietà impostata sul percorso UNC e il nome file del file di backup remoto e la relativa proprietà [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) è impostata sull'identificatore dell'origine dati remota definita nel database.  
  
##  <a name="restoring_databases"></a>Ripristino dei database  
 Il comando `Restore` consente di ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificato da un file di backup. Al comando `Restore` sono associate varie proprietà che consentono di specificare il database da ripristinare, il file di backup da utilizzare, le modalità di ripristino delle definizioni di sicurezza, le partizioni remote da archiviare e la rilocazione di oggetti OLAP relazionali (ROLAP).  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database da ripristinare.  
  
> [!NOTE]  
>  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
### <a name="specifying-the-database-and-backup-file"></a>Specifica del database e del file di backup  
 La proprietà `DatabaseName` del comando `Restore` deve contenere un identificatore di oggetto per un database. In caso contrario, si verifica un errore. Se il database specificato esiste già, la proprietà `AllowOverwrite` determina se il database esistente viene sovrascritto. Se la proprietà `AllowOverwrite` è impostata su false e il database specificato esiste già, si verifica un errore.  
  
 È necessario impostare la proprietà `File` del comando `Restore` su un percorso UNC e su un nome di file relativi al file di backup da ripristinare nel database specificato. È inoltre possibile impostare la proprietà `Password` per il file di backup specificato. Se la proprietà `Password` è impostata su un valore non vuoto, il file di backup viene decrittografato tramite la password specificata. Se il file di backup non è crittografato o se la password specificata non corrisponde a quella utilizzata per crittografare il file di backup, si verifica un errore.  
  
### <a name="restoring-security-settings"></a>Ripristino delle impostazioni di sicurezza  
 La proprietà `Security` determina se il comando `Restore` esegue il ripristino delle definizioni di sicurezza, ad esempio ruoli e autorizzazioni, specificate in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La proprietà `Security` determina inoltre se nel comando `Restore` sono inclusi come parte del processo di ripristino gli account utente e i gruppi di Windows definiti come membri delle definizioni di sicurezza.  
  
 Il valore di questo elemento è limitato a una delle stringhe elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database.|  
  
### <a name="restoring-remote-partitions"></a>Ripristino di partizioni remote  
 Per ogni file di backup remoto creato durante un comando `Backup` precedente, è possibile ripristinare la relativa partizione remota associata includendo un elemento `Location` nella proprietà `Locations` del comando `Restore`. La proprietà [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) di ogni `Location` elemento deve essere esclusa o impostata in modo esplicito su *Remote*.  
  
 Per ogni elemento `Location` specificato, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contatta l'origine dati remota indicata nella proprietà `DataSourceID` per ripristinare le partizioni definite nel file di backup remoto specificato nella proprietà `File`. Oltre alle proprietà `DataSourceID` e `File`, per ogni elemento `Location` utilizzato per ripristinare una partizione remota sono disponibili le proprietà seguenti:  
  
-   Per sovrascrivere la stringa di connessione per l'origine dati remota specificata in `DataSourceID`, è possibile impostare la proprietà `ConnectionString` dell'elemento `Location` su una stringa di connessione diversa. Il comando `Restore` utilizzerà pertanto la stringa di connessione contenuta nella proprietà `ConnectionString`. Se la proprietà `ConnectionString` non viene specificata, il comando `Restore` utilizza la stringa di connessione archiviata nel file di backup per l'origine dati remota specificata. È possibile utilizzare l'impostazione relativa a `ConnectionString` per spostare una partizione remota in un'istanza remota diversa. Non è possibile tuttavia utilizzare l'impostazione relativa a `ConnectionString` per ripristinare una partizione remota alla stessa istanza che contiene il database ripristinato. In altri termini, non è possibile utilizzare la proprietà `ConnectionString` per rendere locale una partizione remota.  
  
-   Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota, è possibile specificare un elemento [Folder](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) per indicare la nuova cartella in cui ripristinare tutte le partizioni remote archiviate nella cartella originale. Se non è specificato alcun elemento `Folder`, il comando `Restore` utilizza le cartelle originali specificate per le partizioni remote contenute nel file di backup remoto.  
  
### <a name="relocating-rolap-objects"></a>Rilocazione di oggetti ROLAP  
 Il comando `Restore` non è in grado di ripristinare aggregazioni o dati per oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate in tabelle in un'origine dati relazionale sottostante. È possibile tuttavia ripristinare i metadati per gli oggetti ROLAP. Per eseguire questa operazione, il comando `Restore` ricrea la struttura della tabella in un'origine dati relazionale.  
  
 Per rilocare oggetti ROLAP, è possibile utilizzare l'elemento `Location` in un comando `Restore`. Per ogni `Location` elemento utilizzato per spostare un'origine dati, la `DataSourceType` proprietà deve essere impostata in modo esplicito su *local*. È inoltre necessario impostare la proprietà `ConnectionString` dell'elemento `Location` sulla stringa di connessione del nuovo percorso. Durante il ripristino, il comando `Restore` sostituirà la stringa di connessione per l'origine dati identificata dalla proprietà `DataSourceID` dell'elemento `Location` con il valore della proprietà `ConnectionString` dell'elemento `Location`.  
  
##  <a name="synchronizing_databases"></a>Sincronizzazione dei database  
 Il comando `Synchronize` consente di sincronizzare i dati e i metadati di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificato con un altro database. Al comando `Synchronize` sono associate varie proprietà che consentono di specificare il database di origine, le modalità di sincronizzazione delle definizioni di sicurezza, le partizioni remote da sincronizzare e la sincronizzazione degli oggetti ROLAP.  
  
> [!NOTE]  
>  Il comando `Synchronize` può essere eseguito solo dagli amministratori del server e del database. Sia il database di origine sia quello di destinazione devono disporre dello stesso livello di compatibilità.  
  
### <a name="specifying-the-source-database"></a>Specifica del database di origine  
 La proprietà [source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) del `Synchronize` comando contiene due proprietà, `ConnectionString` e. `Object` Nella proprietà `ConnectionString` è inclusa la stringa di connessione dell'istanza in cui è contenuto il database di origine, mentre nella proprietà `Object` è contenuto l'identificatore di oggetto per il database di origine.  
  
 Il database di destinazione è il database corrente per la sessione in cui viene eseguito il comando `Synchronize`.  
  
 Se la proprietà `ApplyCompression` del comando `Synchronize` è impostata su true, le informazioni inviate dal database di origine a quello di destinazione vengono compresse prima dell'invio.  
  
### <a name="synchronizing-security-settings"></a>Sincronizzazione delle impostazioni di sicurezza  
 La proprietà [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina se il `Synchronize` comando Sincronizza le definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definite nel database di origine. La proprietà `SynchronizeSecurity` determina inoltre se nel comando `Sychronize` vengono inclusi gli account utente e i gruppi di Windows definiti come membri delle definizioni di sicurezza.  
  
 Il valore di questo elemento è limitato a una delle stringhe elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database di destinazione le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database di destinazione le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database di destinazione.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizzazione di partizioni remote  
 Per ogni origine dati remota presente nel database di origine, è possibile sincronizzare ogni partizione remota associata includendo un elemento `Location` nella proprietà `Locations` del comando `Synchronize`. Per ogni `Location` elemento, la `DataSourceType` proprietà deve essere esclusa o impostata in modo esplicito su *Remote*.  
  
 Per definire un'origine dati remota nel database di destinazione e stabilire una connessione a essa, il comando `Synchronize` utilizza la stringa di connessione definita nella proprietà `ConnectionString` dell'elemento `Location`. Il comando `Synchronize` utilizza quindi la proprietà `DataSourceID` dell'elemento `Location` per identificare le partizioni remote da sincronizzare. Il `Synchronize`comando Sincronizza le partizioni remote nell'origine dati remota specificata nella `DataSourceID` proprietà del database di origine con l'origine dati remota specificata nella `DataSourceID` proprietà del database di destinazione.  
  
 Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota del database di origine, è possibile inoltre specificare un elemento `Folder` nell'elemento `Location`. L'elemento `Folder` indica la nuova cartella per il database di destinazione in cui sincronizzare tutte le partizioni remote archiviate nella cartella originale nell'origine dati remota. Se non è specificato alcun elemento `Folder`, il comando Synchronize utilizza le cartelle originali specificate per le partizioni remote contenute nel database di origine.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizzazione di oggetti ROLAP  
 Il comando `Synchronize` non è in grado di sincronizzare aggregazioni o dati per oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate in tabelle in un'origine dati relazionale sottostante. È possibile tuttavia sincronizzare i metadati per gli oggetti ROLAP. Per eseguire questa operazione, il comando `Synchronize` ricrea la struttura della tabella in un'origine dati relazionale.  
  
 Per sincronizzare oggetti ROLAP, è possibile utilizzare l'elemento `Location` in un comando Synchronize. Per ogni `Location` elemento utilizzato per spostare un'origine dati, la `DataSourceType` proprietà deve essere impostata in modo esplicito su *local*. . È inoltre necessario impostare la proprietà `ConnectionString` dell'elemento `Location` sulla stringa di connessione del nuovo percorso. Durante la sincronizzazione, il comando `Synchronize` sostituirà la stringa di connessione per l'origine dati identificata dalla proprietà `DataSourceID` dell'elemento `Location` con il valore della proprietà `ConnectionString` dell'elemento `Location`.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento backup &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento Restore &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Elemento Synchronize &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Backup e ripristino di database di Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
