---
title: Gravità degli errori del motore di database | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0984d0003f6a20c410b91f99dc6fd1b4ae3f545
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "73844333"
---
# <a name="database-engine-error-severities"></a>Gravità degli errori del Motore di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Negli errori generati da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], la gravità dell'errore indica il tipo di problema rilevato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="levels-of-severity"></a>Livelli di gravità  
 Nella tabella seguente sono elencati e descritti i livelli di gravità degli errori generati da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Livello di gravità|Descrizione|  
|--------------------|-----------------|  
|0-9|Messaggi informativi che restituiscono dettagli sullo stato o segnalano errori non gravi. [!INCLUDE[ssDE](../../includes/ssde-md.md)] non genera errori di sistema con livelli di gravità compresi tra 0 e 9.|  
|10|Messaggi informativi che restituiscono dettagli sullo stato o segnalano errori non gravi. Per motivi di compatibilità, [!INCLUDE[ssDE](../../includes/ssde-md.md)] converte il livello di gravità 10 nel livello di gravità 0 prima di restituire informazioni sull'errore all'applicazione chiamante.|  
|11-16|Indicano errori che possono essere corretti dall'utente.|  
|11|Indica che l'entità o l'oggetto specificato non esiste.|  
|12|Livello di gravità distinto per le query che non utilizzano il blocco a causa di hint per query speciali. In alcuni casi, le operazioni di lettura eseguite da queste istruzioni possono generare dati inconsistenti, poiché non vengono acquisiti blocchi per garantire la consistenza.|  
|13|Indica errori di deadlock di transazione.|  
|14|Indica errori relativi alla sicurezza, ad esempio un'autorizzazione negata.|  
|15|Indica errori di sintassi nel comando [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|16|Indica errori generali che possono essere corretti dall'utente.|  
|17-19|Indicano errori software che possono essere corretti dall'utente. È consigliabile informare l'amministratore di sistema del problema.|  
|17|Indica che l'istruzione ha causato l'esaurimento delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio memoria, blocchi o spazio su disco per il database, oppure il superamento di un limite impostato dall'amministratore di sistema.|  
|18|Indica un problema nel software di [!INCLUDE[ssDE](../../includes/ssde-md.md)] , ma viene completata l'esecuzione dell'istruzione e viene mantenuta la connessione all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Ogni volta che viene visualizzato un messaggio con livello di gravità 18, è consigliabile informare l'amministratore di sistema.|  
|19|Indica che è stato superato un limite di [!INCLUDE[ssDE](../../includes/ssde-md.md)] non configurabile e che è stata terminata l'elaborazione batch corrente. I messaggi di errore con livello di gravità 19 o superiore arrestano l'esecuzione del batch corrente. Gli errori con livello di gravità 19 sono rari e devono essere corretti dall'amministratore di sistema o dal supporto tecnico. Se viene generato un messaggio con livello di gravità 19, rivolgersi all'amministratore di sistema. I messaggi di errore con livello di gravità compreso tra 19 e 25 vengono scritti nel log degli errori.|  
|20-24|Indicano problemi di sistema e rappresentano errori irreversibili. Pertanto, l'attività del [!INCLUDE[ssDE](../../includes/ssde-md.md)] tramite cui viene eseguita un'istruzione o un batch non è più in esecuzione. L'attività registra le informazioni sul problema che si è verificato e termina l'esecuzione. Nella maggior parte dei casi è possibile che venga terminata anche la connessione dell'applicazione all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, a seconda del problema, l'applicazione potrebbe non essere in grado di eseguire la riconnessione.<br /><br /> I messaggi di errore compresi in questo intervallo possono riguardare tutti i processi che accedono ai dati dello stesso database e potrebbero indicare che un database o un oggetto è danneggiato. I messaggi di errore con livello di gravità compreso tra 19 e 24 vengono scritti nel log degli errori.|  
|20|Indica che si è verificato un problema relativo a un'istruzione. Poiché il problema riguarda solo l'attività corrente, è probabile che il database non sia stato danneggiato.|  
|21|Indica che si è verificato un problema che riguarda tutte le attività del database corrente, ma è probabile che il database non sia stato danneggiato.|  
|22|Indica che la tabella o l'indice specificato nel messaggio è stato danneggiato a causa di un problema software o hardware.<br /><br /> Gli errori con livello di gravità 22 si verificano raramente. Se viene generato un tale errore, eseguire DBCC CHECKDB per determinare se sono stati danneggiati anche altri oggetti contenuti nel database. Il problema potrebbe essere limitato esclusivamente alla cache buffer e non riguardare il disco. In tal caso, è possibile correggere il problema riavviando l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Per continuare a lavorare, è necessario riconnettersi all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]; in alternativa, risolvere il problema utilizzando DBCC. In alcuni casi, potrebbe essere necessario ripristinare il database.<br /><br /> Se il problema persiste dopo il riavvio dell'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] , il problema è presente sul disco. L'eliminazione dell'oggetto specificato nel messaggio di errore consente talvolta di risolvere il problema. Se ad esempio il messaggio segnala che l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] ha rilevato una riga con lunghezza pari a 0 in un indice non cluster, è sufficiente eliminare l'indice e ricompilarlo.|  
|23|Indica che l'integrità dell'intero database è compromessa a causa di un problema hardware o software.<br /><br /> Gli errori con livello di gravità 23 si verificano raramente. Se viene generato un tale errore, eseguire DBCC CHECKDB per determinare l'entità del danno. Il problema potrebbe essere limitato esclusivamente alla cache e non riguardare il disco. In tal caso, è possibile correggere il problema riavviando l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Per continuare a lavorare, è necessario riconnettersi all'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]; in alternativa, risolvere il problema utilizzando DBCC. In alcuni casi, potrebbe essere necessario ripristinare il database.|  
|24|Indica un errore del supporto. È possibile che l'amministratore di sistema debba ripristinare il database. Potrebbe anche essere necessario rivolgersi al fornitore dell'hardware.|  
  
## <a name="user-defined-error-message-severity"></a>Gravità dei messaggi di errore definiti dall'utente  
 **sp_addmessage** consente di aggiungere messaggi di errore definiti dall'utente con livelli di gravità compresi tra 1 e 25 alla vista del catalogo **sys.messages** . Tali messaggi di errore definiti dall'utente possono essere utilizzati da RAISERROR. Per altre informazioni, vedere [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
 RAISERROR può essere utilizzato per generare messaggi di errore definiti dall'utente con livelli di gravità compresi tra 1 e 25. RAISERROR può fare riferimento a un messaggio di errore definito dall'utente archiviato nella vista del catalogo **sys.messages** oppure compilare un messaggio in modo dinamico. Quando si usa il messaggio di errore definito dall'utente nella vista del catalogo **sys.messages** durante la generazione di un errore, la gravità specificata da RAISERROR sostituisce quella specificata in **sys.messages**. Per altre informazioni, vedere [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
## <a name="error-severity-and-trycatch"></a>Gravità dell'errore e TRY...CATCH  
 Un costrutto TRY...CATCH rileva tutti gli errori di esecuzione con gravità superiore a 10 che non terminano la connessione al database.  
  
 Gli errori con gravità compresa tra 0 e 10 sono messaggi informativi e non causano l'esecuzione del blocco CATCH di un costrutto TRY...CATCH.  
  
 Gli errori che terminano la connessione al database, in genere con gravità compresa tra 20 e 25, non vengono gestiti dal blocco CATCH in quanto l'esecuzione viene interrotta al termine della connessione.  
  
 Per altre informazioni, vedere [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md).  
  
## <a name="retrieving-error-severity"></a>recupero di gravità errore  
 La funzione di sistema ERROR_SEVERITY consente di recuperare la gravità dell'errore che ha causato l'esecuzione del blocco CATCH di un costrutto TRY...CATCH. ERROR_SEVERITY restituisce NULL se chiamata al di fuori dell'ambito di un blocco CATCH. Per altre informazioni, vedere [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sugli errori del Motore di database](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
