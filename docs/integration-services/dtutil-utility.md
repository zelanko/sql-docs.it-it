---
title: Utilità dtutil | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 396e9b59f41ae31b7ae2a6f091dd540fa41afdcc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725729"
---
# <a name="dtutil-utility"></a>utilità dtutil

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'utilità del prompt dei comandi **dtutil** viene usata per gestire i pacchetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Utilizzare questa utility per copiare, spostare, eliminare un pacchetto oppure per verificarne l'esistenza. È possibile eseguire queste azioni in qualsiasi pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] archiviato in un database [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] e nel file system. Se l'utilità accede a un pacchetto archiviato in **msdb**, al prompt dei comandi può essere necessario specificare nome utente e password. Se l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], al prompt dei comandi sarà necessario specificare nome utente e password. Se non viene specificato il nome utente, **dtutil[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tenta di accedere a**  usando l'autenticazione di Windows. Il tipo di archiviazione del pacchetto è definito dalle opzioni **/SQL**, **/FILE** e **/DTS**.  
  
 L'utilità del prompt dei comandi **dtutil** non supporta l'uso del reindirizzamento o di file di comando.  
  
 L'utilità del prompt dei comandi **dtutil** include le funzionalità seguenti:  
  
-   Inserimento di note nel prompt dei comandi, che consente di ottenere un prompt dei comandi autodocumentato e più semplice da capire.  
  
-   Protezione dalla sovrascrittura, che consente di richiedere conferma prima di sovrascrivere un pacchetto esistente durante la copia o lo spostamento dei pacchetti.  
  
-   Guida della console, che consente di fornire informazioni sulle opzioni dei comandi di **dtutil**.  
  
> [!NOTE]  
>  Numerose operazioni eseguite mediante dtutil possono essere eseguite anche in modo visivo in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] durante la connessione a un'istanza di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](../integration-services/service/package-management-ssis-service.md).  
  
 Le opzioni possono essere specificate in base a un ordine qualsiasi. Il carattere barra verticale ("|") equivale all'operatore **OR** e viene usato per visualizzare i valori possibili. È necessario usare una delle opzioni delimitate dalla barra verticale **OR** .  
  
 Tutte le opzioni devono essere precedute da una barra (/) o un segno meno (-). Non includere uno spazio tra la barra o il segno di sottrazione e il testo dell'opzione. In caso contrario, il comando non verrà eseguito.  
  
 Gli argomenti devono essere stringhe racchiuse tra parentesi oppure che non contengono spazi.  
  
 Le virgolette doppie all'interno di stringhe racchiuse tra virgolette rappresentano virgolette singole di escape.  
  
 Le opzioni e gli argomenti, escluse le password, non fanno distinzione tra maiuscole e minuscole.  
  
 **Considerazioni sull'installazione in computer a 64 bit**  
  
 In un computer a 64 bit con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] viene installata una versione a 64 bit dell'utilità **dtexec** (dtexec.exe) e dell'utilità **dtutil** (dtutil.exe). Per installare le versioni a 32 bit di questi strumenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , è necessario selezionare gli strumenti client o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] durante l'installazione.  
  
 Per impostazione predefinita, un computer a 64 bit contenente le versioni a 64 bit e a 32 bit di un'utilità del prompt dei comandi di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] installata eseguirà la versione a 32 bit al prompt dei comandi. Viene eseguita la versione a 32 bit perché il percorso della directory della versione a 32 bit compare nella variabile di ambiente PATH prima del percorso della directory della versione a 64 bit. In genere, il percorso della directory a 32 bit è *\<unità>* :\Programmi (x86) \Microsoft SQL Server\130\DTS\Binn, mentre il percorso della directory a 64 bit è *\<unità>* :\Programmi\Microsoft SQL Server\130\DTS\Binn.  
  
> [!NOTE]  
>  Se si utilizza SQL Server Agent per eseguire l'utilità, verrà automaticamente utilizzata la versione a 64 bit dell'utilità. Per trovare l'eseguibile corretto per l'utilità, SQL Server Agent utilizza il Registro di sistema, non la variabile di ambiente PATH.  
  
 Per assicurarsi di eseguire la versione a 64 bit dell'utilità al prompt dei comandi, è possibile eseguire una delle azioni seguenti:  
  
-   Aprire una finestra del prompt dei comandi, passare alla directory che contiene la versione a 64 bit dell'utilità, *\<unità>* :\Programmi\Microsoft SQL Server\130\DTS\Binn, quindi eseguire l'utilità da quel percorso.  
  
-   Al prompt dei comandi eseguire l'utilità immettendo il percorso completo ( *\<unità>* :\Programmi\Microsoft SQL Server\130\DTS\Binn) della versione a 64 bit dell'utilità.  
  
-   Modificare in modo definitivo l'ordine dei percorsi nella variabile di ambiente PATH spostando il percorso della versione a 64 bit ( *\<unità>* :\Programmi\Microsoft SQL Server\130\DTS\Binn) prima del percorso della versione a 32 bit ( *\<unità>* :\Programmi(x86)\Microsoft SQL Server\130\DTS\Binn).  
  
## <a name="syntax"></a>Sintassi  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>Parametri  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|/?|Consente di visualizzare le opzioni del prompt dei comandi.|  
|/C[opy] *location;destinationPathandPackageName*|Specifica un'operazione di copia su un pacchetto [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per usare questo parametro, è prima necessario specificare il percorso del pacchetto tramite l'opzione **/FI**, **/SQ**o **/DT** . e quindi indicare la posizione di destinazione e il nome del pacchetto di destinazione. L'argomento *destinationPathandPackageName* specifica la posizione nella quale il pacchetto [!INCLUDE[ssIS](../includes/ssis-md.md)] viene copiato. Se il *percorso* di destinazione è **SQL**, anche gli argomenti *DestUser*, *DestPassword* e *DestServer* devono essere specificati nel comando.<br /><br /> Se l'azione **Copy** rileva un pacchetto esistente nella destinazione, l'utilità **dtutil** richiede all'utente di confermare l'eliminazione del pacchetto. La risposta **Y** comporta la sovrascrittura del pacchetto, mentre la risposta **N** chiude il programma. Se il comando include l'argomento *Quiet* , non viene visualizzata alcuna richiesta di conferma e il pacchetto esistente viene sovrascritto.|  
|/Dec[rypt] *password*|(Facoltativo) Consente di impostare la password di decrittografia utilizzata per caricare un pacchetto con password crittografata.|  
|/Del[ete]|Elimina il pacchetto specificato dall'opzione *SQL*, *DTS* o *FILE* . Se l'utilità **dtutil** non è in grado di eliminare il pacchetto, il programma viene chiuso.|  
|/DestP[assword] *password*|Specifica la password utilizzata dall'opzione SQL per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] di destinazione tramite l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Viene generato un errore se si specifica *DESTPASSWORD* in una riga di comando che non include l'opzione *DTSUSER* .<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].|  
|/DestS[erver] *server_instance*|Specifica il nome del server usato con qualsiasi azione che determina il salvataggio di una destinazione in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Questa opzione viene usata per identificare un server non locale o non predefinito durante il salvataggio di un pacchetto [!INCLUDE[ssIS](../includes/ssis-md.md)] . Non è corretto specificare *DESTSERVER* in una riga di comando che non include un'azione associata a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Azioni come ad esempio le azioni *SIGN SQL*, *COPY SQL*o *MOVE SQL* sono comandi appropriati che è possibile combinare con questa opzione.<br /><br /> Per specificare il nome di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è sufficiente aggiungere una barra rovesciata e il nome dell'istanza al nome del server.|  
|/DestU[ser] *username*|Specifica il nome utente usato con le opzioni *SIGN SQL*, *COPY SQL*e *MOVE SQL* per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Non è corretto specificare *DESTUSER* in una riga di comando che non include l'opzione *SIGN SQL*, *COPY SQL*o *MOVE SQL* .|  
|/Dump *process ID*|(Facoltativo) Causa la sospensione del processo specificato, ovvero l'utilità **dtexec** o il processo **dtsDebugHost.exe** e la creazione dei file dump di debug, con estensione mdmp e tmp.<br /><br /> Nota: per usare l'opzione **/Dump**, è necessario disporre del diritto utente Debug di programmi (SeDebugPrivilege).<br /><br /> Per trovare l' *ID processo* per il processo da sospendere, usare Gestione attività Windows.<br /><br /> Per impostazione predefinita, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] archivia i file dump di debug nella cartella *\<unità>* :\Programmi\Microsoft SQL Server\130\Shared\ErrorDumps.<br /><br /> Per altre informazioni sull'utilità **dtexec** e il processo **dtsDebugHost.exe** , vedere [Utilità dtexec](../integration-services/packages/dtexec-utility.md) e [Compilazione, distribuzione e debug di oggetti personalizzati](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).<br /><br /> Per ulteriori informazioni sui file di dump del debug, vedere [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).<br /><br /> Nota: I file di dump del debug possono contenere informazioni riservate. Utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato.|  
|/DT[S] *filespec*|Specifica che il pacchetto [!INCLUDE[ssIS](../includes/ssis-md.md)] da utilizzare si trova nell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] . L'argomento *filespec* deve includere il percorso della cartella, a partire dalla radice dell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per impostazione predefinita, i nomi delle cartelle radice nel file di configurazione sono "MSDB" e "File System". I percorsi che contengono uno spazio devono essere delimitati da virgolette doppie.<br /><br /> Se si specifica l'opzione DT[S] nella stessa riga di comando di una delle opzioni seguenti, viene restituito un errore DTEXEC_DTEXECERROR:<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(Facoltativo) Crittografa il pacchetto caricato in base alla password e al livello di protezione specificati, quindi lo salva nel percorso specificato in *Path*. L'argomento *ProtectionLevel* determina se è necessaria una password.<br /><br /> *SQL* : il percorso è rappresentato dal nome del pacchetto di destinazione.<br /><br /> *FILE* : il percorso è rappresentato dal percorso e dal nome file completi del pacchetto.<br /><br /> *DTS* : questa opzione non è attualmente supportata.<br /><br /> Opzioni di*ProtectionLevel* :<br /><br /> Livello 0: le informazioni riservate vengono eliminate.<br /><br /> Livello 1: le informazioni riservate vengono crittografate usando le credenziali utente locali.<br /><br /> Livello 2: le informazioni riservate vengono crittografate usando la password richiesta.<br /><br /> Livello 3: il pacchetto viene crittografato usando la password richiesta.<br /><br /> Livello 4: il pacchetto viene crittografato usando le credenziali utente locali.<br /><br /> Livello 5: il pacchetto usa la crittografia per l'archiviazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|/Ex[ists]|(Facoltativo) Utilizzata per determinare l'eventuale esistenza di un pacchetto. **dtutil** tenta di individuare il pacchetto specificato dalle opzioni *SQL*, *DTS* o *FILE* . Se risulta impossibile individuare il pacchetto specificato, l'utilità **dtutil** restituisce un errore DTEXEC_DTEXECERROR.|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(Facoltativo) Crea una nuova cartella il cui nome è specificato in *NewFolderName*. Il percorso della nuova cartella è indicato dall'opzione *ParentFolderPath*.|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(Facoltativo) Elimina la cartella specificata dal nome in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] FolderName [!INCLUDE[ssIS](../includes/ssis-md.md)] da *o*. Il percorso della cartella da eliminare è indicato dall'opzione *ParentFolderPath*.|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(Facoltativo) Elenca il contenuto, ovvero cartelle e pacchetti in una cartella di [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il parametro facoltativo *FolderPath* specifica la cartella di cui visualizzare il contenuto. Il parametro facoltativo *S* specifica che si intende visualizzare l'elenco del contenuto delle sottocartelle della cartella specificata in *FolderPath*.|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(Facoltativo) Verifica se la cartella specificata esiste in [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il parametro *FolderPath* rappresenta il percorso e il nome della cartella da verificare.|  
|/Fi[le] *filespec*|Questa opzione specifica che il pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] da utilizzare si trova nel file system. Il valore di *filespec* può essere specificato sotto forma di percorso UNC (Universal Naming Convention) o di percorso locale.<br /><br /> Se si specifica l'opzione *File* nella stessa riga di comando di una delle opzioni seguenti, viene restituito un errore DTEXEC_DTEXECERROR:<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(Facoltativo) Rinomina una cartella in [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'opzione *ParentFolderPath* specifica il percorso della cartella da rinominare. L'opzione *OldFolderName* specifica il nome attuale della cartella, mentre *NewFolderName* specifica il nuovo nome da assegnare alla cartella.|  
|/H[elp] *option*|Visualizza il testo della Guida dettagliato relativo alle opzioni di **dtutil** e al loro uso. L'argomento è facoltativo. Se si specifica l'argomento, il testo della Guida include informazioni dettagliate sull'opzione specificata. Nell'esempio seguente vengono visualizzate le informazioni della Guida relative a tutte le opzioni.<br /><br /> `dtutil /H`<br /><br /> I due esempi seguenti illustrano come usare l'opzione */H* per visualizzare informazioni dettagliate della Guida per un'opzione specifica, ovvero l'opzione */Q [uiet]* in questo esempio:<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|Crea un nuovo GUID per il pacchetto e aggiorna la proprietà ID del pacchetto. Quando viene copiato un pacchetto, l'ID del pacchetto rimane invariato. I file di log contengono pertanto lo stesso GUID per entrambi i pacchetti. Questa azione crea un nuovo GUID per la nuova copia del pacchetto per distinguerlo dall'originale.|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|Specifica un'operazione di spostamento su un pacchetto [!INCLUDE[ssIS](../includes/ssis-md.md)]. Per usare questo parametro, è prima necessario specificare il percorso del pacchetto tramite l'opzione **/FI**, **/SQ**o **/DT** . e quindi specificare l'azione **Move** . Questa azione richiede due argomenti separati da un punto e virgola:<br /><br /> L'argomento relativo alla destinazione può specificare *SQL*, *FILE*o *DTS*. Una destinazione *SQL* può includere le opzioni *DESTUSER*, *DESTPASSWORD*e *DESTSERVER* .<br /><br /> L'argomento *pathandname* specifica il percorso del pacchetto: *SQL* usa il percorso e il nome del pacchetto, *FILE* usa un percorso UNC o locale, mentre *DTS* usa un percorso relativo alla radice dell'archivio pacchetti [!INCLUDE[ssIS](../includes/ssis-md.md)]. Se si specifica *FILE* o *DTS*come destinazione, l'argomento relativo al percorso non include il nome file, ma utilizza come nome file il nome del pacchetto nella posizione specificata.<br /><br /> <br /><br /> Quando l'azione **MOVE** rileva un pacchetto esistente nella destinazione, **dtutil** richiede la conferma della sovrascrittura del pacchetto. La risposta **Y** comporta la sovrascrittura del pacchetto, mentre la risposta **N** chiude il programma. Se il comando include l'opzione *QUIET* , non viene visualizzata alcuna richiesta di conferma e il pacchetto esistente viene sovrascritto.|  
|/Q[uiet]|Arresta le richieste di conferma che possono essere visualizzate quando viene eseguito un comando che include l'opzione **COPY**, **MOVE**o **SIGN** . Queste richieste di conferma vengono visualizzate se un pacchetto con lo stesso nome del pacchetto specificato esiste già nel computer di destinazione oppure se il pacchetto specificato è già firmato.|  
|/R[emark] *text*|Aggiunge un commento alla riga di comando. L'argomento è facoltativo. Se il testo del commento include spazi, è necessario racchiudere il testo tra virgolette. È possibile includere più opzioni REM in una riga di comando.|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|Firma un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)]. Questa azione usa tre argomenti obbligatori separati da un punto e virgola, ovvero destinazione, percorso e hash:<br /><br /> L'argomento relativo alla destinazione può specificare *SQL*, *FILE*o *DTS*. Una destinazione SQL può includere le opzioni *DESTUSER*, *DESTPASSWORD* e *DESTSERVER* .<br /><br /> L'argomento relativo al percorso specifica la posizione del pacchetto su cui eseguire l'azione.<br /><br /> L'argomento hash specifica un identificatore di certificato espresso come stringa esadecimale di lunghezza variabile.<br /><br /> Per altre informazioni, vedere [Identificazione dell'origine dei pacchetti con firme digitali](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).<br /><br /> <br /><br /> **\*\* Importante \*\*** Se è configurato per la verifica della firma del pacchetto, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] controlla solo la presenza e la validità della firma digitale nonché l'attendibilità della fonte. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]*Non* controlla se il pacchetto è stato modificato.|  
|/SourceP[assword] *password*|Specifica la password usata con le opzioni *SQL* e *SOURCEUSER* per abilitare il recupero di un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] archiviato in un database in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Non è corretto specificare *SOURCEPASSWORD* in una riga di comando che non include l'opzione **SOURCEUSER** .<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *server_instance*|Specifica il nome del server usato con l'opzione **SQL** per abilitare il recupero di un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] archiviato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Non è corretto specificare *SOURCESERVER* in una riga di comando che non include l'opzione *SIGN SQL*, *COPY* *SQL*o *MOVE* *SQL* .<br /><br /> Per specificare il nome di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , è sufficiente aggiungere una barra rovesciata e il nome dell'istanza al nome del server.|  
|/SourceU[ser] *username*|Specifica il nome utente usato con l'opzione *SOURCESERVER* per abilitare il recupero di un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] archiviato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Non è corretto specificare *SOURCESERVER* in una riga di comando che non include l'opzione *SIGN SQL*, *COPY*o *MOVE SQL* .<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|Specifica la posizione di un pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Questa opzione indica che il pacchetto è archiviato nel database **msdb** . L'argomento *package_path* specifica il percorso e il nome del pacchetto di [!INCLUDE[ssIS](../includes/ssis-md.md)] . I nomi delle cartelle terminano con una barra rovesciata.<br /><br /> Se si specifica l'opzione *SQL* nella stessa riga di comando di una delle opzioni seguenti, viene restituito un errore DTEXEC_DTEXECERROR:<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> L'opzione *SQL* può essere accompagnata da zero o da un'istanza delle opzioni seguenti:<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> Se l'opzione *SOURCEUSERNAME* non è inclusa, per accedere al pacchetto verrà usa l'autenticazione di Windows. *SOURCEPASSWORD* è consentita solo se è presente *SOURCEUSER* . Se si omette l'opzione *SOURCEPASSWORD* , viene usata una password vuota.<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>Codici di uscita di dtutil  
 **dtutil** imposta un codice di uscita di avviso nel caso in cui vengano rilevati errori di sintassi, siano stati usati argomenti non corretti o siano state specificate combinazioni di opzioni non valide. In caso contrario, l'utilità visualizza il messaggio "Operazione completata". Nella tabella seguente sono elencati i valori impostati dall'utilità **dtutil** all'uscita.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|L'esecuzione dell'utilità ha avuto esito positivo.|  
|1|L'esecuzione dell'utilità ha avuto esito negativo.|  
|4|L'utilità non è in grado di individuare il pacchetto richiesto.|  
|5|L'utilità non è in grado di caricare il pacchetto richiesto.|  
|6|L'utilità non è in grado di risolvere la riga di comando perché contiene errori sintattici o semantici.|  
  
## <a name="remarks"></a>Remarks  
 Non è possibile usare file di comando o reindirizzamenti con **dtutil**.  
  
 L'ordine delle opzioni all'interno della riga di comando non è significativo.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti vengono illustrati in dettaglio alcuni scenari tipici di utilizzo della riga di comando.  
  
### <a name="copy-examples"></a>Esempi di copia  
 Per copiare nell'archivio pacchetti SSIS un pacchetto archiviato nel database **msdb** in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite l'autenticazione di Windows, usare la sintassi seguente:  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 Per copiare in una posizione diversa un pacchetto da una posizione qualsiasi del file system e assegnare alla copia un nome diverso, utilizzare la sintassi seguente:  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 Per copiare un pacchetto nel file system locale in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ospitata in un altro computer, usare la sintassi seguente:  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 Poiché non sono state usate le opzioni */DestU[ser]* e */DestP[assword]* , verrà usata l'autenticazione di Windows.  
  
 Per creare un nuovo ID per un pacchetto dopo averlo copiato, utilizzare la sintassi seguente:  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 Per creare un nuovo ID per tutti i pacchetti presenti in una cartella specifica, utilizzare la sintassi seguente:  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 Utilizzare un simbolo di percentuale singolo (%) quando si digita il comando al prompt dei comandi. Utilizzare un simbolo di percentuale doppio (%%) se si utilizza il comando in un file batch.  
  
### <a name="delete-examples"></a>Esempi di eliminazione  
 Per eliminare un pacchetto archiviato nel database **msdb** in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di Windows, usare la sintassi seguente:  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 Per eliminare un pacchetto archiviato nel database **msdb** in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usare la sintassi seguente:  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  Per eliminare un pacchetto da un server specificato, includere l'opzione **SOURCESERVER** e il relativo argomento. Un server può essere specificato solo usando l'opzione *SQL* .  
  
 Per eliminare un pacchetto archiviato nell'archivio pacchetti SSIS, utilizzare la sintassi seguente:  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 Per eliminare un pacchetto archiviato nel file system, utilizzare la sintassi seguente:  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>Esempi di verifica dell'esistenza  
 Per determinare se un pacchetto esiste nel database **msdb** in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di Windows, usare la sintassi seguente:  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 Per determinare se un pacchetto esiste nel database **msdb** in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usare la sintassi seguente:  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  Per determinare se un pacchetto esiste in un server specificato, includere l'opzione **SOURCESERVER** e il relativo argomento. Un server può essere specificato solo utilizzando l'opzione SQL.  
  
 Per determinare se un pacchetto esiste nell'archivio pacchetti locale, utilizzare la sintassi seguente:  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 Per determinare se un pacchetto esiste nel file system locale, utilizzare la sintassi seguente:  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>Esempi di spostamento  
 Per spostare un pacchetto archiviato nell'archivio pacchetti SSIS nel database **msdb** in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di Windows, usare la sintassi seguente:  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 Per spostare un pacchetto archiviato nel database **msdb** in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel database **msdb** in un'istanza locale diversa di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che usa l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usare la sintassi seguente:  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  Per spostare un pacchetto da un server specificato a un altro, includere le opzioni **SOURCES** e **DESTS** insieme ai relativi argomenti. Un server può essere specificato solo usando l'opzione *SQL* .  
  
 Per spostare un pacchetto archiviato nell'archivio pacchetti SSIS, utilizzare la sintassi seguente:  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 Per spostare un pacchetto archiviato nel file system, utilizzare la sintassi seguente:  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>Esempi di firma  
 Per firmare un pacchetto archiviato in un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che utilizza l'autenticazione di Windows, utilizzare la sintassi seguente:  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 Per individuare le informazioni sul certificato, usare **CertMgr**. Per visualizzare il codice hash nell'utilità **CertMgr** , selezionare il certificato e fare clic su **Visualizza** per visualizzare le proprietà. Nella scheda **Dettagli** sono disponibili altre informazioni sul certificato. La proprietà **Thumbprint** viene usata come valore hash, rimuovendo gli spazi.  
  
> [!NOTE]  
>  L'hash utilizzato in questo esempio non è un hash reale.  
  
 Per altre informazioni, vedere la sezione relativa a CertMgr in [Firma e controllo del codice con Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100).  
  
### <a name="encrypt-examples"></a>Esempi di crittografia  
 Nell'esempio seguente viene eseguita la crittografia del pacchetto PackageToEncrypt.dtsx basato su file nel pacchetto EncryptedPackage.dts basato su file utilizzando la crittografia completa dei pacchetti e una password. La password usata per la crittografia è *EncPswd*.  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>Vedere anche  
[Eseguire pacchetti di Integration Services (SSIS)](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
  
