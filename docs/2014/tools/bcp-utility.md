---
title: Utilità bcp | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0ddc4c4e7023a83bfde9295a1410e7db5cb90b84
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008738"
---
# <a name="bcp-utility"></a>Utilità bcp
  L'utilità **bcp** esegue operazioni di copia bulk di dati tra un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e un file di dati in un formato specificato dall'utente. L'utilità **bcp** può essere usata per importare un numero elevato di nuove righe nelle tabelle di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o per esportare dati dalle tabelle in file di dati. Ad eccezione del caso in cui venga usata con l'opzione **queryout** , l'utilità non richiede alcuna conoscenza di [!INCLUDE[tsql](../includes/tsql-md.md)]. Per importare dati in una tabella, è necessario utilizzare un file di formato creato per la tabella specifica oppure conoscere approfonditamente la struttura della tabella e i tipi di dati validi per le relative colonne.  
  
 ![Icona di collegamento all'argomento](../../2014/database-engine/media/topic-link.gif "Icona di collegamento a un argomento") Per informazioni sulle convenzioni adottate per la sintassi di **bcp**, vedere [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
> [!NOTE]  
>  Se si esegue il backup dei dati con **bcp** , creare un file di formato per registrare il formato dei dati. I file di dati di**bcp** non includono alcuna informazione sullo schema o sul formato. Di conseguenza, se si elimina una tabella o una vista e non è disponibile un file di formato, può non essere possibile importare i dati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
   bcp [database_name.] schema.{table_name | view_name | "query" {indata_file | outdata_file | queryoutdata_file | format nul}  
  
[-apacket_size]  
[-bbatch_size]  
[-c]  
[-C { ACP | OEM | RAW | code_page } ]  
[-ddatabase_name]  
[-eerr_file]  
[-E]  
[-fformat_file]  
[-Ffirst_row]  
[-h"hint [,...n]"]   
[-iinput_file]  
[-k]  
[-Kapplication_intent]  
[-Llast_row]  
[-mmax_errors]  
[-n]  
[-N]  
[-ooutput_file]  
[-Ppassword]  
[-q]  
[-rrow_term]  
[-R]  
[-S [server_name[\instance_name]]  
[-tfield_term]  
[-T]  
[-Ulogin_id]  
[-v]  
[-V (80 | 90 | 100 | 110)]  
[-w]  
[-x]  
/?  
```  
  
## <a name="arguments"></a>Argomenti  
 *data_file*  
 Percorso completo del file di dati. Quando si esegue un'importazione bulk dei dati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il file di dati include i dati da copiare nella tabella o nella vista specificata. Quando si esegue un'esportazione bulk dei dati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il file di dati include i dati copiati dalla tabella o dalla vista. Il percorso può essere costituito da un numero di caratteri compreso tra 1 e 255. Il file di dati può contenere un massimo di 2<sup>63</sup> -1 righe.  
  
 *database_name*  
 Nome del database in cui si trova la tabella o la vista specificata. Se tale valore non è specificato, il database è quello predefinito dell'utente.  
  
 È inoltre possibile specificare in modo esplicito il nome del database tramite `d-`.  
  
 **in** _data_file_  |  **out**_data_file_  |  **queryout**_data_file_  |  **formato NUL**  
 Specifica la direzione della copia bulk nel modo seguente:  
  
-   **in** esegue la copia da un file nella tabella o nella vista del database.  
  
-   **out** esegue la copia dalla tabella o dalla vista del database in un file. Se si specifica un file esistente, il file viene sovrascritto. Durante l'estrazione dei dati, si noti che l'utilità **bcp** rappresenta una stringa vuota come Null e una stringa Null come stringa vuota.  
  
-   **queryout** esegue la copia da una query e deve essere specificata solo in caso di copia bulk di dati da una query.  
  
-   **Format** crea un file di formato basato sull'opzione specificata (**-n**, `-c` , `-w` o **-n**) e sui delimitatori della tabella o della vista. Quando si esegue la copia bulk dei dati, il comando **bcp** può fare riferimento a un file di formato, evitando di immettere nuovamente le informazioni sul formato in modo interattivo. L'opzione **format** richiede l'opzione **-f** . Se si crea un file di formato XML, è necessaria anche l'opzione **-x** . Per altre informazioni, vedere [Creazione di un file di formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md). È necessario specificare **nul** come valore (**format nul**).  
  
 *owner*  
 Nome del proprietario della tabella o della vista. *owner* è facoltativo se l'utente che esegue l'operazione è il proprietario della tabella o della vista specificata. Se *owner* non viene specificato e l'utente che esegue l'operazione non è il proprietario della tabella o della vista specificata, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] restituisce un messaggio di errore e l'operazione viene annullata.  
  
 **"** _query_ **"**  
 Query [!INCLUDE[tsql](../includes/tsql-md.md)] che restituisce un set di risultati. Se la query restituisce più set di risultati, nel file di dati viene copiato solo il primo set, mentre quelli successivi vengono ignorati. Racchiudere la query tra virgolette doppie e utilizzare le virgolette singole per altri elementi inclusi nella query. L'opzione**queryout** deve essere specificata solo in caso di copia bulk di dati da una query.  
  
 La query può fare riferimento a una stored procedure a condizione che tutte le tabelle cui viene fatto riferimento nella stored procedure siano disponibili prima dell'esecuzione dell'istruzione bcp. Se, ad esempio, la stored procedure genera una tabella temporanea, l'istruzione **bcp** ha esito negativo poiché la tabella è disponibile solo in fase di esecuzione e non nel momento in cui viene eseguita l'istruzione. In questo caso, è opportuno inserire i risultati della stored procedure in una tabella e usare **bcp** per copiare i dati dalla tabella in un file di dati.  
  
 *table_name*  
 Nome della tabella di destinazione per l'importazione di dati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e della tabella di origine per l'esportazione di dati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**).  
  
 *view_name*  
 Nome della vista di destinazione per la copia di dati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e della vista di origine per la copia di dati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**). È possibile utilizzare come viste di destinazione solo quelle in cui tutte le colonne fanno riferimento alla stessa tabella. Per altre informazioni sulle restrizioni per la copia di dati nelle viste, vedere [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
 **-a** _packet_size_  
 Specifica il numero di byte inviati al e dal server per ogni pacchetto di rete. È possibile impostare un'opzione di configurazione del server usando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o la stored procedure di sistema **sp_configure** . Questa opzione, tuttavia, ha la precedenza sull'opzione di configurazione del server. Il valore di*packet_size* può essere compreso tra 4096 e 65535 byte. Il valore predefinito è 4096.  
  
 Le prestazioni delle operazioni di copia bulk migliorano con l'aumentare delle dimensioni del pacchetto. Se è richiesta una dimensione del pacchetto maggiore di quella consentita, viene utilizzato il valore predefinito. Le statistiche sulle prestazioni generate dall'utilità **bcp** indicano le dimensioni del pacchetto in uso.  
  
 **-b** _batch_size_  
 Specifica il numero di righe per ogni batch di dati importati. Ogni batch viene importato e registrato come transazione distinta che importa l'intero batch prima del commit. Per impostazione predefinita, tutte le righe incluse nel file di dati vengono importate come un unico batch. Per distribuire le righe tra più batch, specificare un valore di *batch_size* inferiore al numero di righe presenti nel file di dati. Se la transazione per un batch non viene completata correttamente, viene eseguito il rollback solo degli inserimenti dal batch corrente. I batch già importati dalle transazioni di cui è stato eseguito il commit non sono influenzati in caso di esito negativo.  
  
 Non usare questa opzione in combinazione con l'opzione **-h "** ROWS_PER_BATCH ** = *`bb`* "** .  
  
 `-c`  
 Esegue l'operazione utilizzando un tipo di dati carattere. Questa opzione non visualizza una richiesta per ogni campo. USA `char` come tipo di archiviazione, senza prefissi e con **\t** (carattere di tabulazione) come separatore di campo e **\r\n** (carattere di nuova riga) come carattere di terminazione della riga. `-c` non è compatibile con `-w`.  
  
 Per altre informazioni, vedere [Usare il formato carattere per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }  
 Specifica la tabella codici dei dati contenuti nel file di dati. *code_page* è pertinente solo se i dati `char` contengono `varchar` colonne di tipo, o `text` con valori di carattere maggiori di 127 o minori di 32.  
  
> [!NOTE]  
>  È consigliabile specificare un nome per le regole di confronto per ogni colonna in un file di formato.  
  
|Valore tabella codici|Descrizione|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252).|  
|OEM|Tabella codici predefinita utilizzata dal client. Si tratta della tabella codici predefinita usata se non si specifica **-C** .|  
|RAW|Non vengono eseguite conversioni tra tabelle codici. Per questo motivo, si tratta dell'opzione più rapida.|  
|*code_page*|Numero di tabella codici specifico, ad esempio 850.<br /><br /> **&#42;&#42; importanti &#42;&#42;** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta la tabella codici 65001 (codifica UTF-8).|  
  
 `-d`*database_name*  
 Specifica il database al quale connettersi. Per impostazione predefinita, bcp.exe si connette al database predefinito dell'utente. Se `-d` si specifica *database_name* e un nome in tre parti (*database_name. Schema. Table*, passato come primo parametro per bcp.exe), si verificherà un errore perché non è possibile specificare il nome del database due volte. Se *database_name* inizia con un segno meno (-) o una barra (/), non aggiungere uno spazio tra `-d` e il nome del database.  
  
 **-e** _err_file_  
 Specifica il percorso completo di un file di errori usato per archiviare le eventuali righe che l'utilità **bcp** non è in grado di trasferire dal file al database. I messaggi di errore generati dal comando **bcp** vengono inviati alla workstation dell'utente. Se questa opzione non viene utilizzata, non viene creato alcun file degli errori.  
  
 Se *err_file* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra **-e** e il valore *err_file* .  
  
 **-E**  
 Specifica che il valore o i valori Identity presenti nel file di dati importato devono essere usati per la colonna Identity. Se si omette l'opzione **-E** , i valori Identity della colonna nel file di dati da importare vengono ignorati e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] assegna automaticamente valori univoci in base ai valori di inizializzazione e incremento specificati durante la creazione della tabella.  
  
 Se il file di dati non contiene valori per la colonna Identity della tabella o della vista, utilizzare un file di formato per specificare che durante l'importazione di dati la colonna Identity della tabella o della vista deve essere ignorata. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] assegna automaticamente valori univoci alla colonna. Per altre informazioni, vedere [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql).  
  
 L'opzione **-E** è caratterizzata da requisiti di autorizzazione speciali. Per ulteriori informazioni, vedere la sezione "Osservazioni" di seguito in questo argomento.  
  
 **-f** _format_file_  
 Specifica il percorso completo di un file di formato. Il significato di questa opzione dipende dall'ambiente in cui viene utilizzata, come descritto di seguito:  
  
-   Se l'opzione **-f** viene usata con l'opzione **format** , per la tabella o per la vista indicata verrà creato il file *format_file* specificato. Per creare un file di formato XML, è necessario specificare anche l'opzione **-x** . Per altre informazioni, vedere [Creazione di un file di formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
-   Se si usa con l'opzione **in** o **out** , **-f** richiede un file di formato esistente.  
  
    > [!NOTE]  
    >  L'uso di un file di formato con l'opzione **in** o **out** è facoltativo. Se l'opzione **-f** non è specificata, se non si specifica **-n**, `-c` , `-w` o **-n** , il comando richiede informazioni sul formato e consente di salvare le risposte in un file di formato (il cui nome predefinito è bcp. fmt).  
  
 Se *format_file* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra **-f** e il valore *format_file* .  
  
 **-F** _first_row_  
 Specifica il numero della prima riga da esportare da una tabella o da importare da un file di dati. Per questo parametro è necessario un valore maggiore di (>) 0 ma minore di ( \< ) o uguale a (=) il numero totale di righe. Se il parametro viene omesso, l'impostazione predefinita è la prima riga del file.  
  
 *first_row* può essere un numero intero positivo con valore massimo pari a 2^63-1. **-F**_first_row_ è in base 1.  
  
 **-h"** _hint_[ **,**... *n*] **"**  
 Specifica gli hint da utilizzare per l'importazione bulk di dati in una tabella o in una vista.  
  
 Order **(**_colonna_[ASC | DESC] [**,**... *n*] **)**  
 Tipo di ordinamento dei dati nel file di dati. Le prestazioni dell'importazione bulk sono migliori se i dati da importare vengono ordinati in base all'indice cluster della tabella, se disponibile. Se il file di dati viene ordinato in modo diverso rispetto all'ordine di una chiave di indice cluster o se la tabella non include un indice cluster, la clausola ORDER viene ignorata. I nomi di colonna specificati devono corrispondere a nomi di colonna validi nella tabella di destinazione. Per impostazione predefinita, **bcp** presuppone che il file di dati non sia ordinato. Per garantire l'ottimizzazione dell'importazione bulk, in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene inoltre verificato che i dati importati siano ordinati.  
  
 ROWS_PER_BATCH **=** _BB_  
 Numero di righe di dati per batch (come *bb*). Viene usato quando non si specifica **-b** e quindi l'intero file di dati viene inviato al server come singola transazione. Il server ottimizza il caricamento bulk in base al valore *bb*. Per impostazione predefinita, il valore ROWS_PER_BATCH è sconosciuto.  
  
 KILOBYTES_PER_BATCH **=** _CC_  
 Numero approssimativo di kilobyte di dati per batch (come *cc*). Per impostazione predefinita, il valore KILOBYTES_PER_BATCH è sconosciuto.  
  
 TABLOCK  
 Specifica che viene acquisito un blocco a livello di tabella per l'aggiornamento bulk per la durata dell'operazione di caricamento bulk. In caso contrario, viene acquisito un blocco di riga. Questo hint migliora significativamente le prestazioni, in quanto il mantenimento di un blocco per la durata dell'operazione di copia bulk riduce la contesa dei blocchi per la tabella. Una tabella può essere caricata simultaneamente da più client se non include indici e si specifica **TABLOCK** . Per impostazione predefinita, la modalità di blocco è determinata dall'opzione **table lock on bulk load**della tabella.  
  
 CHECK_CONSTRAINTS  
 Specifica che tutti i vincoli sulla tabella o sulla vista di destinazione devono essere controllati durante l'operazione di importazione bulk. Se non si specifica l'hint CHECK_CONSTRAINTS, i vincoli CHECK e FOREIGN KEY vengono ignorati e al termine dell'operazione il vincolo sulla tabella viene contrassegnato come non trusted.  
  
> [!NOTE]  
>  I vincoli UNIQUE, PRIMARY KEY e NOT NULL vengono sempre applicati.  
  
 In un determinato momento sarà necessario controllare i vincoli sull'intera tabella. Se prima dell'operazione di importazione bulk la tabella non è vuota, il costo per la riconvalida del vincolo potrebbe essere superiore a quello correlato all'applicazione dei vincoli CHECK ai dati incrementali. È pertanto consigliabile abilitare in genere il controllo dei vincoli durante un'importazione bulk incrementale.  
  
 Una situazione in cui può essere necessario disabilitare i vincoli (comportamento predefinito) è rappresentata dal caso in cui i dati di input contengono righe che violano i vincoli. Se i vincoli CHECK sono disabilitati, è possibile importare i dati e quindi utilizzare le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] per rimuovere i dati non validi.  
  
> [!NOTE]  
>  **bcp** ora esegue la convalida e i controlli dei dati che potrebbero causare la mancata esecuzione degli script quando questi vengono eseguiti su dati non validi inclusi in un file di dati.  
  
> [!NOTE]  
>  L'opzione **-m** _max_errors_ non è valida per il controllo dei vincoli.  
  
 FIRE_TRIGGERS  
 Se specificato con l'argomento **in** , determina l'esecuzione dei trigger di inserimento definiti nella tabella di destinazione durante l'operazione di copia bulk. Se non si specifica FIRE_TRIGGERS, non viene eseguito alcun trigger di inserimento. FIRE_TRIGGERS viene ignorato per gli argomenti **out**, **queryout**e **format** .  
  
 **-i** _input_file_  
 Specifica il nome di un file di risposta contenente le risposte alle domande del prompt dei comandi per ogni campo dati quando viene eseguita una copia bulk con la modalità interattiva (**-n**,, `-c` `-w` o **-n** non è specificato).  
  
 Se *input_file* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra **-i** e il valore *input_file* .  
  
 **-k**  
 Specifica che durante l'operazione il valore delle colonne vuote deve essere Null, ovvero che non verranno inseriti valori predefiniti in tali colonne. Per altre informazioni, vedere [Mantenere i valori Null o usare i valori predefiniti durante l'importazione in blocco &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 **-K** _application_intent_  
 Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. L'unico valore consentito è **ReadOnly**. Se l'opzione **-K** non è specificata, l'utilità bcp non supporterà la connettività a una replica secondaria in un gruppo di disponibilità AlwaysOn. Per ulteriori informazioni, vedere [repliche secondarie attive: repliche secondarie leggibili (gruppi di disponibilità AlwaysOn)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **-L** _last_row_  
 Specifica il numero dell'ultima riga da esportare da una tabella o da importare da un file di dati. Per questo parametro è necessario un valore maggiore di (>) 0 ma minore di ( \< ) o uguale a (=) il numero dell'ultima riga. Se il parametro viene omesso, l'impostazione predefinita è l'ultima riga del file.  
  
 *last_row* può essere un numero intero positivo con valore massimo pari a 2^63-1.  
  
 **-m** _max_errors_  
 Specifica il numero massimo di errori di sintassi che possono verificarsi prima dell'annullamento dell'operazione **bcp** . Un errore di sintassi implica un errore di conversione dei dati nel tipo di dati di destinazione. Nel valore totale restituito da *max_errors* sono esclusi tutti gli errori che possono essere rilevati solo a livello del server, ad esempio le violazioni dei vincoli.  
  
 Una riga che non può essere copiata dall'utilità **bcp** viene ignorata e conteggiata come errore. Se l'opzione viene omessa, il valore predefinito è 10.  
  
> [!NOTE]  
>  L'opzione **-m** non è valida anche per la conversione `money` dei `bigint` tipi di dati o.  
  
 **-n**  
 Esegue l'operazione di copia bulk utilizzando i tipi di dati nativi del database. Con questa opzione non viene visualizzata una richiesta per ogni campo, ma vengono utilizzati i valori nativi.  
  
 Per altre informazioni, vedere [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
 **-N**  
 Esegue l'operazione di copia bulk utilizzando i tipi di dati nativi del database per i dati non di tipo carattere e i caratteri Unicode per i dati di tipo carattere. Questa opzione rappresenta un'alternativa, con migliori prestazioni, all'opzione `-w` ed è destinata al trasferimento di dati tra istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite un file di dati. Non viene visualizzata una richiesta per ogni campo. Utilizzare questa opzione per trasferire dati contenenti caratteri ANSI estesi se si desidera sfruttare le prestazioni della modalità nativa.  
  
 Per altre informazioni, vedere [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Se si esportano e quindi si importano dati nello stesso schema di tabella utilizzando bcp.exe con **-N**, è possibile che venga visualizzato un avviso di troncamento se è presente una colonna di tipo carattere non Unicode a lunghezza fissa, ad esempio `char(10)` .  
  
 L'avviso può essere ignorato. Per evitare la visualizzazione dell'avviso, usare **-n** invece di **-N**.  
  
 **-o** _output_file_  
 Specifica il nome di un file in cui viene reindirizzato l'output dal prompt dei comandi.  
  
 Se *output_file* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra **-o** e il valore *output_file* .  
  
 **-P** _password_  
 Specifica la password per l'ID di accesso. Se si omette questa opzione, il comando **bcp** richiede una password. Se l'opzione viene specificata alla fine del prompt dei comandi senza indicare una password, **bcp** userà la password predefinita (NULL).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]  
  
 Per nascondere la password, non specificare l'opzione **-P** in combinazione con l'opzione **-U** . Dopo aver specificato il comando **bcp** con **-U** e altre opzioni (non specificare **-P**) premere INVIO. Il comando richiederà l'immissione di una password. Questo metodo garantisce che la password venga nascosta durante l'immissione.  
  
 Se *password* inizia con un segno meno (-) o una barra (/), non aggiungere uno spazio tra **-P** e il valore *password* .  
  
 `-q`  
 Esegue l'istruzione SET QUOTED_IDENTIFIERS ON durante la connessione tra l'utilità **bcp** e un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Questa opzione consente di specificare il nome di un database, di un proprietario, di una tabella o di una vista che include uno spazio o una virgoletta singola. Racchiudere tra virgolette doppie (" ") l'intero nome in tre parti della tabella o della vista.  
  
 Per specificare un nome di database contenente uno spazio o una virgoletta singola, è necessario usare l'opzione **-q**.  
  
 `-q` non è applicabile ai valori passati a `-d`.  
  
 Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 **-r** _row_term_  
 Specifica il carattere di terminazione della riga. Il valore predefinito è **\n** (carattere di nuova riga). Utilizzare questo parametro per specificare un carattere di terminazione della riga diverso da quello predefinito. Per altre informazioni, vedere [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se si specifica il carattere di terminazione della riga in notazione esadecimale nel comando bcp.exe, il valore verrà troncato in corrispondenza di 0x00. Se ad esempio si specifica 0x410041, verrà utilizzato 0x41.  
  
 Se *row_term* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra **-r** e il valore *row_term* .  
  
 **-R**  
 Specifica che la copia bulk dei dati relativi a valuta, data e ora verrà eseguita in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzando il formato definito per le impostazioni locali del computer client. Per impostazione predefinita, le impostazioni internazionali vengono ignorate.  
  
 **-S** _server_name_[ **\\** _instance_name_]  
 Specifica l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a cui connettersi. Se non si specifica alcun server, l'utilità **bcp** si connette all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] del computer locale. È necessario specificare questa opzione se un comando **bcp** viene eseguito da un computer remoto in rete o in un'istanza denominata locale. Per connettersi all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un server, specificare solo *server_name*. Per connettersi a un'istanza denominata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare *server_name **_\\_** instance_name*.  
  
 `-t`*field_term*  
 Specifica il carattere di terminazione del campo. Il valore predefinito è **\t** (carattere di tabulazione). Utilizzare questo parametro per specificare un carattere di terminazione del campo diverso da quello predefinito. Per altre informazioni, vedere [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se si specifica il carattere di terminazione del campo in notazione esadecimale nel comando bcp.exe, il valore verrà troncato in corrispondenza di 0x00. Se ad esempio si specifica 0x410041, verrà utilizzato 0x41.  
  
 Se *field_term* inizia con un segno meno (-) o una barra (/), non includere uno spazio tra `-t` e il valore di *field_term* .  
  
 **-T**  
 Specifica che l'utilità **bcp** si connette a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con una connessione trusted che usa la sicurezza integrata. Non è necessario specificare le credenziali di sicurezza dell'utente di rete, ovvero *login_id*e *password* . Se non si specifica **-T** , è necessario specificare **-U** e **-P** per eseguire correttamente l'accesso.  
  
 **-U** _login_id_  
 Specifica l'ID di accesso utilizzato per connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Quando l'utilità **bcp** si connette a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite una connessione trusted con sicurezza integrata, usare l'opzione **-T** (connessione trusted) invece della combinazione di *user name* e *password* .  
  
 **-v**  
 Visualizza il numero di versione e le informazioni sul copyright per l'utilità **bcp** .  
  
 **-V** (**80** | **90** | **100**| **110**)  
 Esegue l'operazione di copia bulk utilizzando i tipi di dati di una versione precedente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Con questa opzione non viene visualizzata una richiesta per ogni campo, ma vengono utilizzati i valori predefiniti.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110 =[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]**  
  
 Per generare ad esempio dati per tipi non supportati in [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], ma introdotti in versioni successive di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], utilizzare l'opzione -V80.  
  
 Per altre informazioni, vedere [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 `-w`  
 Esegue l'operazione di copia bulk utilizzando caratteri Unicode. Questa opzione non visualizza una richiesta per ogni campo. USA `nchar` come tipo di archiviazione, nessun prefisso, **\t** (carattere di tabulazione) come separatore di campo e **\n** (carattere di nuova riga) come carattere di terminazione della riga. `-w` non è compatibile con `-c`.  
  
 Per altre informazioni, vedere [Usare il formato carattere Unicode per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 **-x**  
 Se usato con le opzioni **format** e **-f**_format_file_, genera un file di formato basato su XML anziché un file di formato predefinito non XML. L'opzione **-x** non può essere usata per l'importazione o l'esportazione dei dati. Genera un errore se viene usata senza **format** e **-f**_format_file_.  
  
## <a name="remarks"></a>Osservazioni  
 Il client **bcp** 12,0 viene installato quando si installano [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] gli strumenti di. Se gli strumenti vengono installati sia per [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] che per una versione precedente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a seconda del valore della variabile di ambiente PATH è possibile che venga utilizzato il client **bcp** precedente anziché il client **bcp** 12.0. La variabile di ambiente definisce il set di directory utilizzato in Windows per la ricerca di file eseguibili. Per determinare la versione in uso, eseguire il comando **bcp /v** al prompt dei comandi di Windows. Per informazioni su come impostare il percorso di comando nella variabile di ambiente PATH, vedere la Guida di Windows.  
  
 I file di formato XML sono supportati solo quando gli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono installati insieme a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
 Per informazioni sulla posizione e sulle modalità di esecuzione dell'utilità **bcp** e sulle convenzioni di sintassi per le utilità della riga di comando, vedere [Guida di riferimento alle utilità del prompt dei comandi &#40;Motore di database&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
 Per informazioni sulla preparazione dei dati per le operazioni di importazione o esportazione in blocco, vedere [Preparare i dati per l'importazione o l'esportazione in blocco &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Per informazioni sui casi in cui le operazioni di inserimento di righe eseguite durante l'importazione in blocco vengono registrate nel log delle transazioni, vedere [Prerequisiti per la registrazione minima nell'importazione in blocco](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="native-data-file-support"></a>Supporto per file di dati nativi  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], l'utilità **bcp** supporta i file di dati nativi compatibili con [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
## <a name="computed-columns-and-timestamp-columns"></a>Colonne calcolate e colonne timestamp  
 I valori per le colonne calcolate o `timestamp` nel file di dati importato vengono ignorati e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] assegna automaticamente nuovi valori. Se il file di dati non contiene valori per le colonne calcolate o `timestamp` della tabella, utilizzare un file di formato per specificare che le colonne calcolate o `timestamp` della tabella dovranno essere ignorate durante l'importazione dei dati. I valori per la colonna verranno assegnati automaticamente da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Le copie bulk di colonne calcolate e `timestamp` da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un file di dati vengono eseguite con le modalità consuete.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>Definizione di identificatori contenenti spazi o virgolette  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] possono includere caratteri quali spazi incorporati e virgolette. Tali identificatori possono essere utilizzati nei modi seguenti:  
  
-   Quando al prompt dei comandi si specifica un identificatore o un nome di file che include uno spazio o una virgoletta singola, racchiuderlo tra virgolette doppie ("").  
  
     Il comando `bcp out` seguente, ad esempio, consente di creare un file di dati denominato `Currency Types.dat`:  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   Per specificare un nome di database contenente uno spazio o una virgoletta singola, utilizzare l'opzione `-q`.  
  
-   Per i nomi di proprietario, di tabella o di vista contenenti spazi incorporati o virgolette singole, è possibile effettuare le operazioni seguenti:  
  
    -   Specificare l'opzione `-q` oppure  
  
    -   Racchiudere il nome del proprietario, della tabella o della vista tra parentesi quadre ([]) all'interno di virgolette.  
  
## <a name="data-validation"></a>Convalida dei dati  
 **bcp** ora esegue la convalida e i controlli dei dati che potrebbero causare la mancata esecuzione degli script quando questi vengono eseguiti su dati non validi inclusi in un file di dati. L'utilità **bcp** , ad esempio, verifica quanto segue:  
  
-   Validità della rappresentazione nativa dei tipi di dati `float` o `real`.  
  
-   Lunghezza in byte pari dei dati Unicode.  
  
 Il caricamento di alcuni tipi di dati non validi di cui può essere eseguita l'importazione bulk nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] potrebbe avere esito negativo in questa versione. Nelle versioni precedenti l'errore si verifica solo quando un client tenta di accedere ai dati non validi. La convalida aggiuntiva riduce il rischio di errori durante l'esecuzione di query sui dati in seguito al caricamento bulk.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Esportazione o importazione bulk di documenti SQLXML  
 Per l'esportazione o l'importazione bulk di dati SQLXML, utilizzare uno dei tipi di dati seguenti nel file di formato.  
  
|Tipo di dati|Effetto|  
|---------------|------------|  
|SQLCHAR o SQLVARYCHAR|I dati vengono inviati nella tabella codici del client o nella tabella codici implicita delle regole di confronto. L'effetto equivale a quello ottenuto specificando l'opzione `-c` senza definire un file di formato.|  
|SQLNCHAR o SQLNVARCHAR|I dati vengono inviati in formato Unicode. L'effetto equivale a quello ottenuto specificando l'opzione `-w` senza definire un file di formato.|  
|SQLBINARY o SQLVARYBIN|I dati vengono inviati senza conversione.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Un'operazione**bcpout** richiede l'autorizzazione SELECT per la tabella di origine.  
  
 Un'operazione **bcpin** richiede almeno l'autorizzazione SELECT/INSERT per la tabella di destinazione. È inoltre richiesta l'autorizzazione ALTER TABLE se si verifica uno dei casi seguenti:  
  
-   Sono presenti alcuni vincoli e l'hint CHECK_CONSTRAINTS non è specificato.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, i vincoli sono disabilitati. Per abilitarli in modo esplicito, usare l'opzione **-h** con l'hint CHECK_CONSTRAINTS.  
  
-   Sono presenti alcuni trigger e l'hint FIRE_TRIGGER non è specificato.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, i trigger non sono attivati. Per attivarli in modo esplicito, usare l'opzione **-h** con l'hint FIRE_TRIGGERS.  
  
-   Usare l'opzione **-E** per importare valori Identity da un file di dati.  
  
> [!NOTE]  
>  Il requisito relativo all'autorizzazione ALTER TABLE per la tabella di destinazione è una caratteristica introdotta in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Questo nuovo requisito può causare l'esito negativo degli script di **bcp** che non consentono l'applicazione di trigger e controlli dei vincoli se l'account utente non dispone delle autorizzazioni ALTER TABLE per la tabella di destinazione.  
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>Procedure consigliate relative alla modalità carattere (-c) e alla modalità nativa (-n)  
 In questa sezione sono presenti indicazioni relative alla modalità carattere (-c) e alla modalità nativa (-n).  
  
-   (Amministratore/utente) Quando possibile, utilizzare il formato nativo (-n) per evitare i problemi relativi al separatore. Utilizzare il formato nativo per esportare e importare tramite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se i dati saranno importati in un database non [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esportarli da[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzando l'opzione -c o -w.  
  
-   (Amministratore) Verificare i dati in caso di utilizzo di BCP OUT. Ad esempio, quando si utilizza BCP OUT, BCP IN, quindi BCP OUT, verificare che i dati vengano esportati correttamente e che i valori del carattere di terminazione non siano utilizzati in alcuni valori di dati. Considerare di eseguire l'override dei caratteri di terminazione predefiniti (utilizzando le opzioni -t e -r) con valori esadecimali casuali per evitare conflitti tra i valori del carattere di terminazione e i valori dei dati.  
  
-   (Utente) Utilizzare un carattere di terminazione lungo e univoco (qualsiasi sequenza di byte o caratteri) per ridurre la possibilità di un conflitto con il valore stringa effettivo. Questa operazione può essere effettuata utilizzando le opzioni -t e -r.  
  
## <a name="examples"></a>Esempi  
 Questa sezione contiene gli esempi seguenti:  
  
-   R. Copia delle righe di tabella in un file di dati (con connessione trusted)  
  
-   B. Copia delle righe di tabella in un file di dati (con autenticazione in modalità mista)  
  
-   C. Copia di dati da un file a una tabella  
  
-   D. Copia di una colonna specifica in un file di dati  
  
-   E. Copia di una riga specifica in un file di dati  
  
-   F. Copia di dati da una query a un file di dati  
  
-   G. Creazione di un file di formato non XML  
  
-   H. Creazione di un file di formato XML  
  
-   I. Uso di un file di formato per l'importazione bulk con **bcp**  
  
### <a name="a-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>R. Copia delle righe di tabella in un file di dati (con connessione trusted)  
 L'esempio seguente illustra l'uso dell'opzione **out** nella tabella `AdventureWorks2012.Sales.Currency` e viene creato un file di dati denominato `Currency.dat` in cui vengono copiati i dati della tabella utilizzando il formato carattere. Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi immettere il comando seguente:  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -T -c  
```  
  
### <a name="b-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>B. Copia delle righe di tabella in un file di dati (con autenticazione in modalità mista)  
 L'esempio seguente illustra l'uso dell'opzione **out** nella tabella `AdventureWorks2012.Sales.Currency` e viene creato un file di dati denominato `Currency.dat` in cui vengono copiati i dati della tabella utilizzando il formato carattere.  
  
 Si presuppone che l'utente usi l'autenticazione in modalità mista, quindi l'opzione **-U** è necessaria per specificare l'ID di accesso. A meno che non venga eseguita la connessione all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sul computer locale, usare l'opzione **-S** per specificare il nome di sistema e, facoltativamente, il nome di un'istanza.  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -c -U<login_id> -S<server_name\instance_name>  
```  
  
 Verrà richiesto di inserire la password.  
  
### <a name="c-copying-data-from-a-file-to-a-table"></a>C. Copia di dati da un file a una tabella  
 L'esempio seguente illustra l'uso dell'opzione **in** con il file creato nell'esempio precedente (`Currency.dat`). Viene innanzitutto creata una copia vuota della tabella `AdventureWorks2012 Sales.Currency`, `Sales.Currency2`, in cui vengono copiati i dati. Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Per creare la tabella vuota, nell'editor di query immettere il comando seguente:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO AdventureWorks2012.Sales.Currency2   
FROM AdventureWorks2012.Sales.Currency WHERE 1=2;  
```  
  
 Per eseguire la copia bulk di dati di tipo carattere nella nuova tabella, ovvero per importare i dati, al prompt dei comandi immettere il comando seguente:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -c  
```  
  
 Per verificare la corretta esecuzione del comando, visualizzare il contenuto della tabella nell'editor di query e digitare:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM Sales.Currency2  
```  
  
### <a name="d-copying-a-specific-column-into-a-data-file"></a>D. Copia di una colonna specifica in un file di dati  
 Per copiare una colonna specifica, è possibile usare l'opzione **queryout** . Nell'esempio seguente viene copiata in un file di dati solo la colonna `Name` della tabella `Sales.Currency` . Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp "SELECT Name FROM AdventureWorks.Sales.Currency" queryout Currency.Name.dat -T -c  
```  
  
### <a name="e-copying-a-specific-row-into-a-data-file"></a>E. Copia di una riga specifica in un file di dati  
 Per copiare una riga specifica, è possibile usare l'opzione **queryout** . Nell'esempio seguente viene copiata solo la riga per il contatto denominato `Jarrod Rana` dalla tabella `AdventureWorks2012.Person.Person` in un file di dati (`Jarrod Rana.dat`). Nell'esempio si presuppone che l'uso l'autenticazione di Windows e l'esistenza di una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp**.  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp "SELECT * FROM AdventureWorks2012.Person.Person WHERE FirstName='Jarrod' AND LastName='Rana' "  queryout "Jarrod Rana.dat" -T -c  
```  
  
### <a name="f-copying-data-from-a-query-to-a-data-file"></a>F. Copia di dati da una query a un file di dati  
 Per copiare il set di risultati da un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] a un file di dati, usare l'opzione **queryout** . Nell'esempio seguente vengono copiati i nomi dalla tabella `AdventureWorks2012.Person.Person` nel file di dati `Contacts.txt` , ordinandoli in base al cognome e quindi al nome. Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp "SELECT FirstName, LastName FROM AdventureWorks2012.Person.Person ORDER BY LastName, Firstname" queryout Contacts.txt -c -T  
```  
  
### <a name="g-creating-a-non-xml-format-file"></a>G. Creazione di un file di formato non XML  
 Nell'esempio seguente viene creato un file di formato non XML denominato `Currency.fmt` per la tabella `Sales.Currency` nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c  -f Currency.fmt  
```  
  
 Per altre informazioni, vedere [File in formato non XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="h-creating-an-xml-format-file"></a>H. Creazione di un file di formato XML  
 Nell'esempio seguente viene creato un file di formato XML denominato `Currency.xml` per la tabella `Sales.Currency` nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c -x -f Currency.xml  
```  
  
> [!NOTE]  
>  Per usare l'opzione **-x** , è necessario avere un client **bcp** 9.0. Per informazioni sull'utilizzo del client **bcp** 9,0, vedere la sezione "osservazioni".  
  
 Per altre informazioni, vedere [File in formato XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. Utilizzo di un file di formato per l'importazione bulk con bcp  
 Per usare un file di formato creato in precedenza durante l'importazione di dati in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], specificare **-f** con l'opzione **in** . Il comando seguente, ad esempio, consente di eseguire la copia bulk del contenuto di un file di dati denominato `Currency.dat` in una copia della tabella `Sales.Currency` (`Sales.Currency2`) utilizzando il file di formato creato in precedenza (`Currency.xml`). Si presuppone che l'utente usi l'autenticazione di Windows e una connessione trusted all'istanza del server in cui viene eseguito il comando **bcp** .  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -f Currency.xml  
```  
  
> [!NOTE]  
>  I file di formato risultano particolarmente utili quando i campi dei file di dati sono diversi dalle colonne della tabella, ad esempio per numero, ordine o tipi di dati. Per altre informazioni, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
 Negli argomenti seguenti sono contenuti esempi di utilizzo di **bcp**:  
  
-   [Creazione di un file di formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Preparare i dati per l'importazione o l'esportazione bulk &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [IMPOSTA QUOTED_IDENTIFIER &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_tableoption &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)   
 [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
