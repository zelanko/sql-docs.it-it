---
title: Verificare che l'aumento automatico sia attivato per tutti i file di dati e di log durante il processo di aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log files [SQL Server], size
- data files [SQL Server], size
- tempdb [SQL Server], size
- autogrow [SQL Server]
ms.assetid: a5860904-e2be-4224-8a51-df18a10d3fb9
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8ca12075598bce210a905cbdfba89f2d879cf09b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065193"
---
# <a name="verify-autogrow-is-turned-on-for-all-data-and-log-files-during-the-upgrade-process"></a>Verificare che l'aumento di dimensioni automatico sia attivato per tutti i file di dati e di log durante il processo di aggiornamento
  Sono stati rilevati file di dati o di log per cui non è impostato l'aumento automatico delle dimensioni. Le funzionalità nuove e migliorate richiedono ulteriore spazio su disco per i database utente e il database di sistema **tempdb** . Per garantire che le risorse possano supportare gli aumenti di dimensioni durante l'aggiornamento e le successive operazioni di produzione, è consigliabile impostare l'aumento automatico delle dimensioni su ON per tutti i file di dati e di log dell'utente e i file di log e di dati **tempdb**  
  
 Dopo aver aggiornato i carichi di lavoro e averne eseguito il test, è necessario disabilitare l'aumento automatico delle dimensioni o modificare l'incremento FILEGROWTH in modo appropriato per i file di log e i file di dati degli utenti. È consigliabile che l'aumento automatico delle dimensioni rimanga attivo per il database di sistema **tempdb** . Per ulteriori informazioni, vedere "Pianificazione delle capacità per tempdb" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 **File di dati**  
  
 Nella tabella seguente sono elencate le modifiche apportate alle caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che comportano un aumento dei requisiti di spazio su disco per i file di dati definiti dall'utente.  
  
|Funzionalità|Modifiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Full-text|La mappa ID (DOCID) del documento è archiviata nel file di dati anziché nel catalogo full-text.|  
|Colonne `text`, `ntext` e `image`|Le colonne LOB definite come tipi di dati `text`, `ntext` o `image` necessitano di altri 40 byte di spazio su disco per colonna. Quest'unico aumento di spazio viene richiesto durante il primo aggiornamento di ogni colonna LOB.|  
|metadata|Vengono creati e mantenuti metadati di sistema aggiuntivi nel filegroup PRIMARY di ogni database utente per gli oggetti di database e le autorizzazioni utente. Ad esempio, nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le autorizzazioni associate a un utente che concede le autorizzazioni o a un utente autorizzato vengono archiviate su un'unica riga come bitmap, mentre la bitmap viene estesa su più righe.<br /><br /> Durante il processo di aggiornamento, lo spazio disponibile deve essere sufficiente per archiviare sia i nuovi metadati che quelli precedenti. Questi ultimi vengono eliminati dopo il completamento dell'aggiornamento.|  
  
 **File di log delle transazioni**  
  
 Nella tabella seguente sono elencate le modifiche apportate alle caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che comportano un aumento dei requisiti di spazio su disco per i file di log delle transazioni definiti dall'utente.  
  
|Funzionalità|Modifiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Ripristino e recupero|Durante la fase di rollback di un recupero a seguito dell'arresto anomalo del sistema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente agli utenti di accedere al database. Questo è possibile in quanto le transazioni di cui non è stato eseguito il commit quando si è verificato l'arresto anomalo del sistema riacquisiscono eventuali blocchi applicati prima di tale arresto. Durante il rollback di tali transazioni, i relativi blocchi le proteggono da interferenze da parte degli utenti. Questo blocco aggiuntivo delle informazioni deve essere mantenuto nel log delle transazioni.|  
  
 **file di log e di dati di tempdb**  
  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il database **tempdb** viene utilizzato per archiviare gli oggetti seguenti:  
  
-   Oggetti temporanei creati in modo esplicito, ad esempio tabelle, stored procedure, variabili di tabella o cursori.  
  
-   Tabelle di lavoro interne create dal [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Risultati degli ordinamenti temporanei quando vengono creati o ricompilati indici, se SORT_IN_TEMPDB è specificato.  
  
 Gli oggetti aggiuntivi utilizzano anche il database **tempdb** . Nella tabella seguente sono elencate le modifiche o le aggiunte alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzionalità che hanno come risultato requisiti di spazio su disco aggiuntivi per i file di dati e di log di **tempdb** .  
  
|Funzionalità|Modifiche introdotte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|-------------|-----------------------------------------------------|  
|Controllo delle versioni delle righe|Il controllo delle versioni delle righe è un framework generale in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per:<br /><br /> Trigger di supporto: compilare le tabelle inserite ed eliminate nei trigger. Le righe modificate dal trigger vengono sottoposte al controllo delle versioni. Questo include le righe modificate dall'istruzione che ha avviato il trigger, nonché qualsiasi modifica ai dati eseguita dal trigger. I trigger AFTER utilizzano l'archivio delle versioni di **tempdb** per contenere le immagini precedenti delle righe modificate dal trigger. Quando si esegue il caricamento bulk con i trigger abilitati, all'archivio delle versioni viene aggiunta una copia di ogni riga.<br /><br /> Supportare più set di risultati attivi (MARS). Se una sessione MARS genera un'istruzione di modifica dei dati (ad esempio INSERT, UPDATE oppure DELETE) nel momento in cui è attivo un set di risultati, le righe influenzate dall'istruzione di modifica sono sottoposte al controllo delle versioni.<br /><br /> Supportare operazioni di indice che specificano l'opzione ONLINE. Nelle operazioni sugli indici online viene utilizzato il controllo delle versioni delle righe per isolare le operazioni dagli effetti delle modifiche apportate da altre transazioni. In questo modo, non è necessario richiedere blocchi di condivisione sulle righe lette. Inoltre, le operazioni di aggiornamento ed eliminazione simultanee degli utenti durante le operazioni sugli indici online richiedono spazio per i record di versione in **tempdb**.<br /><br /> Supportare i livelli di isolamento delle transazioni basati sul controllo delle versioni delle righe: una nuova implementazione del livello di isolamento Read committed che utilizza il controllo delle versioni delle righe per fornire la coerenza di lettura a livello di istruzione. Un nuovo livello di isolamento, snapshot, per offrire consistenza di lettura a livello di transazione.<br /><br /> <br /><br /> Le versioni di riga vengono mantenute nell'archivio delle versioni di **tempdb** abbastanza per soddisfare i requisiti delle transazioni in esecuzione con i livelli di isolamento basati sul controllo delle versioni delle righe.<br /><br /> Per ulteriori informazioni sul controllo delle versioni delle righe e sull'archivio delle versioni, vedere "Informazioni sui livelli di isolamento basati sul controllo delle versioni delle righe" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Memorizzazione nella cache dei metadati di tabella temporanea e variabile temporanea|Per ogni metadati della tabella temporanea e della variabile temporanea memorizzati nella cache dei metadati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vengono allocate due pagine aggiuntive per **tempdb**.<br /><br /> Se una stored procedure o un trigger crea una tabella temporanea o una variabile temporanea, l'oggetto temporaneo non viene eliminato al completamento della stored procedure o del trigger, ma viene invece troncato in un'unica pagina e riutilizzato alla successiva esecuzione della stored procedure o del trigger.|  
|Indici in tabelle partizionate|Quando [!INCLUDE[ssDE](../../includes/ssde-md.md)] esegue l'ordinamento per compilare indici partizionati, è necessario spazio sufficiente per l'esecuzione delle operazioni di ordinamento intermedie di ogni partizione in **tempdb** se viene specificata l'opzione SORT_IN_TEMPDB index.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|[!INCLUDE[ssSB](../../includes/sssb-md.md)]USA in modo esplicito **tempdb** quando si conserva il contesto della finestra di dialogo esistente che non può rimanere in memoria (approssimativamente 1 KB per dialogo).<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)]utilizza in modo implicito **tempdb** tramite la memorizzazione nella cache di oggetti nel contesto dell'esecuzione della query. ad esempio le tabelle di lavoro utilizzate per gli eventi del timer e le conversazioni recapitate in background.<br /><br /> Le caratteristiche DBMail, le notifiche degli eventi e le notifiche delle query utilizzano in modo implicito [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|Tipi di dati LOB<br /><br /> Variabili e parametri LOB|I tipi di dati `varchar(max)` , `nvarchar(max)` , **varbinary (max) Text**, `ntext` `image,` e `xml` sono tipi LOB.<br /><br /> Quando nel database è abilitato un livello di isolamento delle transazioni basato sul controllo delle versioni delle righe e vengono apportate modifiche a oggetti di grandi dimensioni, il frammento modificato del LOB viene copiato nell'archivio delle versioni in **tempdb**.<br /><br /> I parametri definiti come tipo di dati LOB vengono archiviati in **tempdb**.|  
|Espressioni di tabella comuni|Le tabelle di lavoro temporanee per le operazioni di spooling vengono create in **tempdb** quando vengono eseguite query di espressioni di tabella comuni.|  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per impostare un file di dati o di log per l'aumento automatico di dimensioni, modificare le istruzioni seguenti per specificare i dati e il log per il database. È necessario regolare l'incremento FILEGROWTH su un valore appropriato per l'ambiente.  
  
```  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = tempdev,  
    FILEGROWTH = 20MB);  
GO  
ALTER DATABASE tempdb  
MODIFY FILE  
    (NAME = templog,  
    FILEGROWTH = 10MB);  
```  
  
 L'incremento predefinito per l'aumento delle dimensioni dei file di dati è di 1 MB. L'impostazione predefinita del file di log è 10%. Per l'impostazione dell'incremento FILEGROWTH, è consigliabile applicare le linee guida generali seguenti:  
  
|Dimensione del file|Incremento FILEGROWTH|  
|---------------|--------------------------|  
|0-50 MB|10 MB|  
|100-200 MB|20MB|  
|500MB o più|10%|  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
