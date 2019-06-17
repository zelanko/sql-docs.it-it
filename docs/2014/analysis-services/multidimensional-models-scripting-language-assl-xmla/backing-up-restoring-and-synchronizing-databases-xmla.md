---
title: Il backup, ripristino e sincronizzazione di database (XMLA) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702274"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Backup, ripristino e sincronizzazione di database (XMLA)
  In XML for Analysis sono disponibili i tre comandi seguenti per l'esecuzione del backup, del ripristino e della sincronizzazione dei database:  
  
-   Il [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) comando esegue il backup di un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database usando un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] file di backup (con estensione ABF), come descritto nella sezione [backup dei database](#backing_up_databases).  
  
-   Il [ripristinare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) comando Ripristina un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database da un file con estensione ABF, come descritto nella sezione [ripristino di database](#restoring_databases).  
  
-   Il [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) comando viene sincronizzato uno [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database con i dati e i metadati di un altro database, come descritto nella sezione [sincronizzazione di database](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a> Backup dei database  
 Come indicato in precedenza, il comando `Backup` consente di eseguire il backup di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificato in un file di backup. Al comando `Backup` sono associate varie proprietà che consentono di specificare il database di cui eseguire il backup, il file di backup da utilizzare, le modalità di esecuzione del backup delle definizioni di sicurezza e le partizioni remote di cui eseguire il backup.  
  
> [!IMPORTANT]  
>  L'account del servizio Analysis Services deve disporre delle autorizzazioni per scrivere nel percorso di backup specificato per ogni file. L'utente deve inoltre avere uno dei ruoli seguenti: ruolo di amministratore per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) per il database di cui eseguire il backup.  
  
### <a name="specifying-the-database-and-backup-file"></a>Specifica del database e del file di backup  
 Per specificare il database da sottoporre a backup, impostare il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà del `Backup` comando. La proprietà `Object` deve contenere un identificatore di oggetto per un database. In caso contrario, si verifica un errore.  
  
 Per specificare il file che deve essere creato e usato dal processo di backup, impostare il [File](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) proprietà del `Backup` comando. La proprietà `File` deve essere impostata su un percorso UNC e su un nome di file relativi al file di backup da creare.  
  
 Oltre a indicare il file da utilizzare per il backup, per il file di backup specificato è possibile impostare le opzioni seguenti:  
  
-   Se si impostano i [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) su true, il `Backup` comando sovrascrive il file di backup se il file specificato esiste già. Se invece si imposta la proprietà `AllowOverwrite` su false, qualora il file di backup esista già si verifica un errore.  
  
-   Se si impostano i [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) proprietà su true, il file di backup viene compresso dopo aver creato il file.  
  
-   Se si impostano i [Password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) impostandola su qualsiasi valore non vuoto, il file di backup viene crittografato usando la password specificata.  
  
    > [!IMPORTANT]  
    >  Se le proprietà `ApplyCompression` e `Password` non vengono specificate, nel file di backup i nomi utente e le password contenuti nelle stringhe di connessione vengono archiviati in testo non crittografato. I dati archiviati in testo non crittografato possono essere recuperati. Per aumentare la sicurezza, utilizzare le impostazioni relative a `ApplyCompression` e `Password` sia per comprimere che per crittografare il file di backup.  
  
### <a name="backing-up-security-settings"></a>Backup delle impostazioni di sicurezza  
 Il [sicurezza](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) proprietà determina se il `Backup` comando esegue il backup delle definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definiti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. La proprietà `Security` determina inoltre se nel file di backup vengono inclusi gli account utente e i gruppi di Windows definiti come membri delle definizioni di sicurezza.  
  
 Il valore della proprietà `Security` è limitato a una delle stringhe elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel file di backup le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel file di backup le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal file di backup.|  
  
### <a name="backing-up-remote-partitions"></a>Backup di partizioni remote  
 Per eseguire il backup di partizioni remote nel [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database, impostare il [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) proprietà del `Backup` comando su true. In questo modo il comando `Backup` crea un file di backup remoto per ogni origine dati remota utilizzata per archiviare partizioni remote per il database.  
  
 Per ogni origine dati remota eseguire il backup, è possibile specificare il file di backup corrispondente includendo un [posizione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) elemento il [posizioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) proprietà del `Backup` comando. Il `Location` l'elemento deve contenere relativi `File` proprietà impostato sul nome di file e percorso UNC del file di backup remoto e i relativi [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) proprietà impostato sull'identificatore dell'origine dati remota definita nel database.  
  
##  <a name="restoring_databases"></a> Il ripristino dei database  
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
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database.|  
  
### <a name="restoring-remote-partitions"></a>Ripristino di partizioni remote  
 Per ogni file di backup remoto creato durante un comando `Backup` precedente, è possibile ripristinare la relativa partizione remota associata includendo un elemento `Location` nella proprietà `Locations` del comando `Restore`. Il [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) proprietà per ogni `Location` elemento deve essere escluso o impostato in modo esplicito *remoto*.  
  
 Per ogni elemento `Location` specificato, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contatta l'origine dati remota indicata nella proprietà `DataSourceID` per ripristinare le partizioni definite nel file di backup remoto specificato nella proprietà `File`. Oltre alle proprietà `DataSourceID` e `File`, per ogni elemento `Location` utilizzato per ripristinare una partizione remota sono disponibili le proprietà seguenti:  
  
-   Per sovrascrivere la stringa di connessione per l'origine dati remota specificata in `DataSourceID`, è possibile impostare la proprietà `ConnectionString` dell'elemento `Location` su una stringa di connessione diversa. Il comando `Restore` utilizzerà pertanto la stringa di connessione contenuta nella proprietà `ConnectionString`. Se la proprietà `ConnectionString` non viene specificata, il comando `Restore` utilizza la stringa di connessione archiviata nel file di backup per l'origine dati remota specificata. È possibile utilizzare l'impostazione relativa a `ConnectionString` per spostare una partizione remota in un'istanza remota diversa. Non è possibile tuttavia utilizzare l'impostazione relativa a `ConnectionString` per ripristinare una partizione remota alla stessa istanza che contiene il database ripristinato. In altri termini, non è possibile utilizzare la proprietà `ConnectionString` per rendere locale una partizione remota.  
  
-   Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota, è possibile specificare una [cartella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) elemento per indicare la nuova cartella in cui ripristinare tutte le partizioni remote archiviate nella cartella originale. Se non è specificato alcun elemento `Folder`, il comando `Restore` utilizza le cartelle originali specificate per le partizioni remote contenute nel file di backup remoto.  
  
### <a name="relocating-rolap-objects"></a>Rilocazione di oggetti ROLAP  
 Il comando `Restore` non è in grado di ripristinare aggregazioni o dati per oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate in tabelle in un'origine dati relazionale sottostante. È possibile tuttavia ripristinare i metadati per gli oggetti ROLAP. Per eseguire questa operazione, il comando `Restore` ricrea la struttura della tabella in un'origine dati relazionale.  
  
 Per rilocare oggetti ROLAP, è possibile utilizzare l'elemento `Location` in un comando `Restore`. Per ognuno `Location` elemento utilizzato per rilocare un'origine dati, il `DataSourceType` proprietà deve essere impostata in modo esplicito *locale*. È inoltre necessario impostare la proprietà `ConnectionString` dell'elemento `Location` sulla stringa di connessione del nuovo percorso. Durante il ripristino, il comando `Restore` sostituirà la stringa di connessione per l'origine dati identificata dalla proprietà `DataSourceID` dell'elemento `Location` con il valore della proprietà `ConnectionString` dell'elemento `Location`.  
  
##  <a name="synchronizing_databases"></a> La sincronizzazione dei database  
 Il comando `Synchronize` consente di sincronizzare i dati e i metadati di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificato con un altro database. Al comando `Synchronize` sono associate varie proprietà che consentono di specificare il database di origine, le modalità di sincronizzazione delle definizioni di sicurezza, le partizioni remote da sincronizzare e la sincronizzazione degli oggetti ROLAP.  
  
> [!NOTE]  
>  Il comando `Synchronize` può essere eseguito solo dagli amministratori del server e del database. Sia il database di origine sia quello di destinazione devono disporre dello stesso livello di compatibilità.  
  
### <a name="specifying-the-source-database"></a>Specifica del database di origine  
 Il [origine](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) proprietà delle `Synchronize` comando contiene due proprietà, `ConnectionString` e `Object`. Nella proprietà `ConnectionString` è inclusa la stringa di connessione dell'istanza in cui è contenuto il database di origine, mentre nella proprietà `Object` è contenuto l'identificatore di oggetto per il database di origine.  
  
 Il database di destinazione è il database corrente per la sessione in cui viene eseguito il comando `Synchronize`.  
  
 Se la proprietà `ApplyCompression` del comando `Synchronize` è impostata su true, le informazioni inviate dal database di origine a quello di destinazione vengono compresse prima dell'invio.  
  
### <a name="synchronizing-security-settings"></a>Sincronizzazione delle impostazioni di sicurezza  
 Il [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) proprietà determina se il `Synchronize` comando Sincronizza le definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definite nel database di origine. La proprietà `SynchronizeSecurity` determina inoltre se nel comando `Sychronize` vengono inclusi gli account utente e i gruppi di Windows definiti come membri delle definizioni di sicurezza.  
  
 Il valore di questo elemento è limitato a una delle stringhe elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database di destinazione le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database di destinazione le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database di destinazione.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizzazione di partizioni remote  
 Per ogni origine dati remota presente nel database di origine, è possibile sincronizzare ogni partizione remota associata includendo un elemento `Location` nella proprietà `Locations` del comando `Synchronize`. Per ognuno `Location` elemento, il `DataSourceType` proprietà deve essere escluso o impostata in modo esplicito *remoto*.  
  
 Per definire un'origine dati remota nel database di destinazione e stabilire una connessione a essa, il comando `Synchronize` utilizza la stringa di connessione definita nella proprietà `ConnectionString` dell'elemento `Location`. Il comando `Synchronize` utilizza quindi la proprietà `DataSourceID` dell'elemento `Location` per identificare le partizioni remote da sincronizzare. Il `Synchronize`comando consente di sincronizzare le partizioni remote nell'origine dati remota specificata nella `DataSourceID` nel database di origine con l'origine dati remota specificata nella proprietà di `DataSourceID` proprietà nel database di destinazione.  
  
 Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota del database di origine, è possibile inoltre specificare un elemento `Folder` nell'elemento `Location`. L'elemento `Folder` indica la nuova cartella per il database di destinazione in cui sincronizzare tutte le partizioni remote archiviate nella cartella originale nell'origine dati remota. Se non è specificato alcun elemento `Folder`, il comando Synchronize utilizza le cartelle originali specificate per le partizioni remote contenute nel database di origine.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizzazione di oggetti ROLAP  
 Il comando `Synchronize` non è in grado di sincronizzare aggregazioni o dati per oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate in tabelle in un'origine dati relazionale sottostante. È possibile tuttavia sincronizzare i metadati per gli oggetti ROLAP. Per eseguire questa operazione, il comando `Synchronize` ricrea la struttura della tabella in un'origine dati relazionale.  
  
 Per sincronizzare oggetti ROLAP, è possibile utilizzare l'elemento `Location` in un comando Synchronize. Per ognuno `Location` elemento utilizzato per rilocare un'origine dati, il `DataSourceType` proprietà deve essere impostata in modo esplicito *locale*. . È inoltre necessario impostare la proprietà `ConnectionString` dell'elemento `Location` sulla stringa di connessione del nuovo percorso. Durante la sincronizzazione, il comando `Synchronize` sostituirà la stringa di connessione per l'origine dati identificata dalla proprietà `DataSourceID` dell'elemento `Location` con il valore della proprietà `ConnectionString` dell'elemento `Location`.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento Backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Backup e ripristino di database di Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
