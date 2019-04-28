---
title: Il backup, ripristino e sincronizzazione di database (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19d311a07eb11f1c5119a3c20d7536b5a2986b49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719894"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Backup, ripristino e sincronizzazione di database (XMLA)
  In XML for Analysis sono disponibili i tre comandi seguenti per l'esecuzione del backup, del ripristino e della sincronizzazione dei database:  
  
-   Il [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) comando esegue il backup di un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database usando un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] file di backup (con estensione ABF), come descritto nella sezione [backup dei database](#backing_up_databases).  
  
-   Il [ripristinare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) comando Ripristina un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database da un file con estensione ABF, come descritto nella sezione [ripristino di database](#restoring_databases).  
  
-   Il [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) comando viene sincronizzato uno [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del database con i dati e i metadati di un altro database, come descritto nella sezione [sincronizzazione di database](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a> Backup dei database  
 Come accennato in precedenza, il **Backup** comando esegue il backup specificato [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database in un file di backup. Il **Backup** comando è associate varie proprietà che consentono di specificare il database da sottoporre a backup, il file di backup da usare, come eseguire il backup delle definizioni di sicurezza e le partizioni remote per il backup.  
  
> [!IMPORTANT]  
>  L'account del servizio Analysis Services deve disporre delle autorizzazioni per scrivere nel percorso di backup specificato per ogni file. L'utente deve inoltre avere uno dei ruoli seguenti: ruolo di amministratore per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) per il database di cui eseguire il backup.  
  
### <a name="specifying-the-database-and-backup-file"></a>Specifica del database e del file di backup  
 Per specificare il database da sottoporre a backup, impostare il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà delle **Backup** comando. Il **oggetto** proprietà deve contenere un identificatore di oggetto per un database o si verifica un errore.  
  
 Per specificare il file che deve essere creato e usato dal processo di backup, impostare il [File](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) proprietà delle **Backup** comando. Il **File** proprietà deve essere impostata su un nome di file e percorso UNC del file di backup da creare.  
  
 Oltre a indicare il file da utilizzare per il backup, per il file di backup specificato è possibile impostare le opzioni seguenti:  
  
-   Se si imposta la [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) su true, il **Backup** comando sovrascrive il file di backup se il file specificato esiste già. Se si impostano i **AllowOverwrite** si verifica un errore la proprietà su false, se il file di backup specificato esiste già.  
  
-   Se si impostano i [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) proprietà su true, il file di backup viene compresso dopo aver creato il file.  
  
-   Se si impostano i [Password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) impostandola su qualsiasi valore non vuoto, il file di backup viene crittografato usando la password specificata.  
  
    > [!IMPORTANT]  
    >  Se **ApplyCompression** e **Password** non siano specificate proprietà, il file di backup vengono archiviati i nomi utente e le password contenuti nelle stringhe di connessione in testo non crittografato. I dati archiviati in testo non crittografato possono essere recuperati. Per una maggiore sicurezza, usare il **ApplyCompression** e **Password** impostazioni sia comprimere e crittografare il file di backup.  
  
### <a name="backing-up-security-settings"></a>Backup delle impostazioni di sicurezza  
 Il [sicurezza](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) proprietà determina se il **Backup** comando esegue il backup delle definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definiti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Il **sicurezza** proprietà determina inoltre se il file di backup include gli account utente di Windows e i gruppi definiti come membri delle definizioni di sicurezza.  
  
 Il valore della **sicurezza** proprietà è limitato a una delle stringhe elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel file di backup le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel file di backup le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal file di backup.|  
  
### <a name="backing-up-remote-partitions"></a>Backup di partizioni remote  
 Per eseguire il backup di partizioni remote nel [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database, impostare il [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) proprietà del **Backup** comando su true. Questa impostazione fa in modo che il **Backup** comando per creare un file di backup remoto per ogni origine dati remota che viene usato per archiviare partizioni remote per il database.  
  
 Per ogni origine dati remota eseguire il backup, è possibile specificare il file di backup corrispondente includendo un [posizione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) elemento il [posizioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) proprietà del **Backup** comando. Il **posizione** l'elemento deve contenere relativo **File** proprietà impostato sul nome di file e percorso UNC del file di backup remoto e il relativo [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceid-element-xmla) impostato sull'identificatore di proprietà l'origine dati remota definita nel database.  
  
##  <a name="restoring_databases"></a> Il ripristino dei database  
 Il **ripristinare** comando Ripristina un determinato [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database da un file di backup. Il **ripristinare** comando è associate varie proprietà che consentono di specificare il database da ripristinare, il file di backup da usare, come ripristinare le definizioni di sicurezza, le partizioni remote da archiviare e la rilocazione OLAP relazionale (ROLAP) oggetti.  
  
> [!IMPORTANT]  
>  Per ogni file di backup, l'utente che esegue il comando di ripristino deve disporre delle autorizzazioni per leggere dal percorso di backup specificato per ogni file. Per ripristinare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non installato nel server, l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica. Per sovrascrivere un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], l'utente deve inoltre essere un membro del ruolo del server per l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure un membro di un ruolo del database con autorizzazioni Controllo completo (amministratore) sul database da ripristinare.  
  
> [!NOTE]  
>  Dopo avere ripristinato un database esistente, l'utente che ha effettuato l'operazione potrebbe perdere l'accesso al database ripristinato. Può verificarsi questa perdita di accesso se, al momento dell’esecuzione del backup, l'utente non era un membro del ruolo del server o non era un membro del ruolo del database con autorizzazioni Controllo completo (amministratore).  
  
### <a name="specifying-the-database-and-backup-file"></a>Specifica del database e del file di backup  
 Il **NomeDatabase** proprietà delle **ripristinare** comando deve contenere un identificatore di oggetto per un database o si verifica un errore. Se il database specificato esiste già, il **AllowOverwrite** proprietà determina se il database esistente viene sovrascritto. Se il **AllowOverwrite** proprietà è impostata su false e il database specificato esiste già, si verifica un errore.  
  
 È consigliabile impostare il **File** proprietà delle **ripristinare** comando a un nome di file e percorso UNC del file di backup da ripristinare nel database specificato. È anche possibile impostare il **Password** proprietà per il file di backup specificato. Se il **Password** è impostata su qualsiasi valore non vuoto, il file di backup viene decrittografato tramite la password specificata. Se il file di backup non è crittografato o se la password specificata non corrisponde a quella utilizzata per crittografare il file di backup, si verifica un errore.  
  
### <a name="restoring-security-settings"></a>Ripristino delle impostazioni di sicurezza  
 Il **sicurezza** proprietà determina se il **ripristinare** comando Ripristina le definizioni di sicurezza, ad esempio ruoli e autorizzazioni, specificate in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Il **sicurezza** proprietà determina anche se il **ripristinare** comando include gli account utente di Windows e i gruppi definiti come membri delle definizioni di sicurezza come parte del processo di ripristino.  
  
 Il valore di questo elemento è limitato a una delle stringhe elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database.|  
  
### <a name="restoring-remote-partitions"></a>Ripristino di partizioni remote  
 Per ogni file di backup remoto creato durante un precedente **Backup** comando, è possibile ripristinare la partizione remota associata includendo un **posizione** elemento il **posizioni**della proprietà di **ripristinare** comando. Il [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourcetype-element-xmla) proprietà per ogni **posizione** elemento deve essere escluso o impostato in modo esplicito *Remote*.  
  
 Per ognuna delle quali specificata **posizione** elemento, il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza contatta l'origine dati remota specificata nella **DataSourceID** proprietà per ripristinare le partizioni definite nel file di backup remoto specificato nella **File** proprietà. Altre origini oltre al **DataSourceID** e **File** le proprietà, le proprietà seguenti sono disponibili per ogni **percorso** elemento usato per ripristinare una partizione remota:  
  
-   Per sostituire la stringa di connessione per l'origine dati remota specificata nella **DataSourceID**, è possibile impostare il **ConnectionString** proprietà del **percorso** elemento a un stringa di connessione diversa. Il **ripristinare** comando userà quindi la stringa di connessione contenute nella **ConnectionString** proprietà. Se **ConnectionString** non viene specificato, il **ripristinare** comando Usa la stringa di connessione archiviata nel file di backup per l'origine dati remota specificata. È possibile usare la **ConnectionString** impostazione per spostare una partizione remota in una diversa istanza remota. Tuttavia, è possibile usare la **ConnectionString** impostazione per ripristinare una partizione remota alla stessa istanza che contiene il database ripristinato. In altre parole, non è possibile utilizzare il **ConnectionString** proprietà per una partizione remota in una partizione locale.  
  
-   Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota, è possibile specificare una [cartella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) elemento per indicare la nuova cartella in cui ripristinare tutte le partizioni remote archiviate nella cartella originale. Se un **cartella** elemento non viene specificato, il **ripristinare** comando utilizza le cartelle originali specificate per le partizioni remote contenute nel file di backup remoto.  
  
### <a name="relocating-rolap-objects"></a>Rilocazione di oggetti ROLAP  
 Il **ripristinare** comando non è possibile ripristinare aggregazioni o dati per gli oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate nelle tabelle in un'origine dati relazionale sottostante. È possibile tuttavia ripristinare i metadati per gli oggetti ROLAP. Per ripristinare i metadati per oggetti ROLAP, le **ripristinare** comando ricrea la struttura della tabella in un'origine dati relazionale.  
  
 È possibile usare la **posizione** elemento in un **ripristinare** comando per rilocare oggetti ROLAP. Per ogni **ubicazione** elemento utilizzato per rilocare un'origine dati, il **DataSourceType** proprietà deve essere impostata in modo esplicito su *locale*. Inoltre necessario impostare il **ConnectionString** proprietà delle **posizione** elemento alla stringa di connessione della nuova posizione. Durante il ripristino, il **ripristinare** comando sostituirà la stringa di connessione per l'origine dati identificata dalle **DataSourceID** proprietà del **percorso** elemento con il valore della **ConnectionString** proprietà delle **posizione** elemento.  
  
##  <a name="synchronizing_databases"></a> La sincronizzazione dei database  
 Il **Synchronize** comando consente di sincronizzare i dati e i metadati di un elemento specificato [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database con un altro database. Il **Synchronize** comando presenta varie proprietà che consentono di specificare il database di origine come sincronizzare definizioni di sicurezza, le partizioni remote da sincronizzare e la sincronizzazione di oggetti ROLAP.  
  
> [!NOTE]  
>  Il **Synchronize** comando può essere eseguito solo dagli amministratori di server e gli amministratori di database. Sia il database di origine sia quello di destinazione devono disporre dello stesso livello di compatibilità.  
  
### <a name="specifying-the-source-database"></a>Specifica del database di origine  
 Il [origine](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) proprietà delle **Sincronizza** comando contiene due proprietà, **ConnectionString** e **oggetto**. Il **ConnectionString** proprietà contiene la stringa di connessione dell'istanza che contiene il database di origine e il **oggetto** proprietà contiene l'identificatore di oggetto per il database di origine.  
  
 Il database di destinazione è il database corrente per la sessione in cui il **Synchronize** comando esegue.  
  
 Se il **ApplyCompression** proprietà delle **Sincronizza** command è impostato su true, le informazioni inviate dall'origine database nel database di destinazione viene compresso prima dell'invio.  
  
### <a name="synchronizing-security-settings"></a>Sincronizzazione delle impostazioni di sicurezza  
 Il [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) proprietà determina se il **Sincronizza** comando Sincronizza le definizioni di sicurezza, ad esempio ruoli e autorizzazioni, definite nel database di origine. Il **SynchronizeSecurity** proprietà determina anche se il **Sincronizza** comando include gli account utente di Windows e i gruppi definiti come membri delle definizioni di sicurezza.  
  
 Il valore di questo elemento è limitato a una delle stringhe elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*SkipMembership*|Include nel database di destinazione le definizioni di sicurezza, ma ne esclude le informazioni sull'appartenenza.|  
|*CopyAll*|Include nel database di destinazione le definizioni di sicurezza e le informazioni sull'appartenenza.|  
|*IgnoreSecurity*|Esclude le definizioni di sicurezza dal database di destinazione.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizzazione di partizioni remote  
 Per ogni origine dati remota presente nel database di origine, è possibile sincronizzare ogni partizione remota associata includendo un **posizione** elemento il **posizioni** proprietà del  **Sincronizzare** comando. Per ogni **posizione** elemento, il **DataSourceType** proprietà deve essere escluso o impostata in modo esplicito *remoto*.  
  
 Per definire e connettersi a un'origine dati remota nel database di destinazione, il **Synchronize** comando Usa la stringa di connessione definita nel **ConnectionString** proprietà del **percorso**  elemento. Il **Synchronize** quindi comando Usa il **DataSourceID** proprietà del **percorso** elemento per identificare le partizioni remote da sincronizzare. Il **Synchronize**comando consente di sincronizzare le partizioni remote nell'origine dati remota specificata nella **DataSourceID** proprietà nel database di origine con l'origine dati remota specificata nella  **Elemento DataSourceID** proprietà nel database di destinazione.  
  
 Per ogni cartella originale utilizzata per archiviare le partizioni remote nell'origine dati remota nel database di origine, è anche possibile specificare una **cartella** elemento le **posizione** elemento. Il **cartella** elemento indica la nuova cartella per il database di destinazione in cui sincronizzare tutte le partizioni remote archiviate nella cartella originale nell'origine dati remota. Se un **cartella** elemento non viene specificato, il comando Synchronize utilizza le cartelle originali specificate per le partizioni remote contenute nel database di origine.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizzazione di oggetti ROLAP  
 Il **Synchronize** comando non è possibile sincronizzare aggregazioni o dati per gli oggetti che utilizzano l'archiviazione ROLAP poiché tali informazioni vengono archiviate nelle tabelle in un'origine dati relazionale sottostante. È possibile tuttavia sincronizzare i metadati per gli oggetti ROLAP. Per sincronizzare i metadati, il **Synchronize** comando ricrea la struttura della tabella in un'origine dati relazionale.  
  
 È possibile usare la **posizione** elemento in un comando di sincronizzazione per sincronizzare oggetti ROLAP. Per ogni **ubicazione** elemento utilizzato per rilocare un'origine dati, il **DataSourceType** proprietà deve essere impostata in modo esplicito su *locale*. . Inoltre necessario impostare il **ConnectionString** proprietà delle **posizione** elemento alla stringa di connessione della nuova posizione. Durante la sincronizzazione, il **Synchronize** comando sostituirà la stringa di connessione per l'origine dati identificata dalle **DataSourceID** proprietà del **percorso** elemento con il valore della **ConnectionString** proprietà delle **posizione** elemento.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento Backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Backup e ripristino di database di Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
