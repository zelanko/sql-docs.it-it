---
title: Stored procedure (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e64a097fb4d2eed917155fb3881d233231c413bc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70148293"
---
# <a name="stored-procedures-database-engine"></a>Stored procedure (Motore di database)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Una stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un gruppo di una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure un riferimento a un metodo CLR (Common Runtime Language) di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Le stored procedure assomigliano ai costrutti di altri linguaggi di programmazione perché possono essere utilizzate per:  
  
-   Accettare parametri di input e restituire più valori sotto forma di parametri di output al programma che esegue la chiamata.  
  
-   Includere istruzioni di programmazione che eseguono operazioni nel database, tra cui la chiamata di altre stored procedure.  
  
-   Restituire un valore di stato a un programma che esegue la chiamata per indicare l'esito positivo o negativo (e il motivo dell'esito negativo).  
  
## <a name="benefits-of-using-stored-procedures"></a>Vantaggi dell'utilizzo delle stored procedure  
 Nell'elenco seguente vengono descritti alcuni vantaggi dell'utilizzo di stored procedure.  
  
 Riduzione del traffico di rete server/client  
 I comandi in una stored procedure vengono eseguiti come un solo batch di codice. In questo modo è possibile ridurre significativamente il traffico di rete tra il server e il client perché solo la chiamata per eseguire la stored procedure viene inviata attraverso la rete. Senza l'incapsulamento del codice consentito dalla stored procedure, la rete viene attraversata da ogni singola riga di codice.  
  
 Miglioramento della sicurezza  
 Tramite una stored procedure, più utenti e programmi client sono in grado di eseguire operazioni su oggetti di database sottostanti, anche se gli utenti e i programmi non dispongono di autorizzazioni dirette su tali oggetti sottostanti. La stored procedure consente di controllare quali processi e attività vengono eseguiti e di proteggere gli oggetti di database sottostanti. In questo modo si elimina la necessità di concedere autorizzazioni a livello di singolo oggetto, semplificando i livelli di sicurezza.  
  
 È possibile specificare la clausola [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) nell'istruzione CREATE PROCEDURE per consentire la rappresentazione di un altro utente o consentire a utenti e applicazioni di eseguire alcune attività nel database senza avere bisogno di autorizzazioni dirette per gli oggetti e i comandi sottostanti. Ad esempio per alcune azioni, come TRUNCATE TABLE non sono disponibili autorizzazioni. Per eseguire TRUNCATE TABLE è necessario che l'utente disponga dell'autorizzazione ALTER per la tabella specificata. Concedere a un utente l'autorizzazione ALTER su una tabella non è consigliabile, perché l'utente disporrebbe di autorizzazioni ben superiori alla semplice possibilità di troncare la tabella. Incorporando l'istruzione TRUNCATE TABLE in un modulo e specificando che tale modulo venga eseguito come un utente che dispone di autorizzazioni per la modifica della tabella è possibile estendere le autorizzazioni per il troncamento della tabella all'utente al quale si concede l'autorizzazione EXECUTE sul modulo.  
  
 In caso di chiamata a una stored procedure attraverso la rete, solo la chiamata per eseguire la stored procedure è visibile. Pertanto, gli utenti malintenzionati non possono visualizzare i nomi di oggetti di database e tabelle, incorporare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzate o cercare dati critici.  
  
 L'utilizzo dei parametri della stored procedure aiuta a proteggersi da attacchi SQL injection. Dal momento che l'input del parametro viene trattato come un valore letterale e non come codice eseguibile, è più difficile che un pirata informatico riesca a inserire un comando nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] all'interno della stored procedure compromettendo la sicurezza.  
  
 È possibile crittografare le stored procedure, nascondendo il codice sorgente. Per altre informazioni, vedere [Crittografia di SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Riutilizzo del codice  
 Il codice di operazioni ripetitive sul database risulta assolutamente appropriato ai fini dell'incapsulamento nelle stored procedure. In questo modo si elimina la necessità di riscrivere più volte lo stesso codice, si riducono le incoerenze al suo interno e se ne consentono l'accesso e l'esecuzione da parte di qualsiasi utente o applicazione che disponga delle autorizzazioni necessarie.  
  
 Semplificazione della manutenzione  
 Quando si effettua la chiamata delle stored procedure tramite le applicazioni client e si mantengono le operazioni nel database solo nel livello dati, in caso di modifiche nel database sottostante è necessario aggiornare unicamente le stored procedure. Si mantiene separato il livello applicazione senza che venga interessato dalle modifiche a layout del database, relazioni o processi.  
  
 prestazioni migliorate  
 Per impostazione predefinita, una stored procedure viene compilata solo alla prima esecuzione e si crea un piano di esecuzione da riutilizzare nelle esecuzioni successive. Dal momento che non è necessaria la creazione di un nuovo piano da parte del sistema di elaborazione delle query, l'elaborazione della stored procedure richiede generalmente un tempo minore.  
  
 Se c'è stata modifica significativa alle tabelle o ai dati a cui fa riferimento la stored procedure, è possibile che il piano precompilato comporti in realtà un'esecuzione più lenta della stored procedure. In questo caso, la ricompilazione della stored procedure e la forzatura di un nuovo piano di esecuzione possono migliorare le prestazioni.  
  
## <a name="types-of-stored-procedures"></a>Tipi di stored procedure  

 **Definita dall'utente**  
 È possibile creare una stored procedure definita dall'utente in un database definito dall'utente o in tutti i database del sistema a eccezione del **database delle risorse** . La stored procedure può essere sviluppata in [!INCLUDE[tsql](../../includes/tsql-md.md)] o come un riferimento a un metodo CLR (Common Runtime Language) di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 **Temporanea**  
 Le stored procedure temporanee sono un tipo di stored procedure definite dall'utente. Sono simili alle stored procedure permanenti, ma vengono archiviate in **tempdb**. Esistono due tipi di stored procedure temporanee:locali e globali. I due tipi differiscono per i nomi, la visibilità e la disponibilità. Le stored procedure temporanee locali contengono un solo simbolo di cancelletto (#) come primo carattere del nome, sono visibili solo durante la connessione utente corrente e vengono eliminate alla chiusura della connessione. Le stored procedure temporanee globali contengono due simboli di cancelletto (##) come primi caratteri del nome, sono visibili per tutti gli utenti in seguito alla creazione e vengono eliminate al termine dell'ultima sessione che utilizza la stored procedure.  
  
 **Sistema**  
 Le stored procedure di sistema sono incluse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sono archiviate fisicamente nel **database delle risorse** , interno e nascosto e livello logico compaiono nello schema **sys** di tutti i database di sistema e di quelli definiti dall'utente. Inoltre, il database **msdb** contiene anche stored procedure di sistema nello schema **dbo** che vengono utilizzate per la pianificazione di avvisi e processi. Dal momento che le stored procedure di sistema iniziano con il prefisso **sp_** , si consiglia di non utilizzare questo prefisso per l'assegnazione di un nome alle procedure definite dall'utente. Per un elenco completo delle stored procedure di sistema, vedere [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta le stored procedure di sistema che forniscono ai programmi esterni un'interfaccia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per varie attività di manutenzione. Tali stored procedure estese utilizzano il prefisso xp_. Per un elenco completo delle stored procedure estese, vedere [Stored procedure estese generali &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md).  
  
 **Estese definite dall'utente**  
 Le stored procedure estese permettono di creare routine esterne in un linguaggio di programmazione come C e sono DLL che possono essere caricate ed eseguite in modo dinamico da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Le stored procedure estese verranno eliminate nelle future versioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non usare questa funzionalità in un nuovo progetto di sviluppo e modificare non appena possibile le applicazioni in cui è attualmente implementata. In alternativa, creare stored procedure CLR. Questo metodo offre un'alternativa più efficiente rispetto alla scrittura di stored procedure estese.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione dell'attività**|**Argomento**|  
|Viene descritto il processo di creazione di una stored procedure.|[Creare una stored procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|Viene descritto il processo di modifica di una stored procedure.|[Modificare una stored procedure](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|Viene descritto il processo di eliminazione di una stored procedure.|[Eliminare una stored procedure](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|Viene descritto come eseguire una stored procedure.|[Eseguire una stored procedure](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|Viene descritto come concedere autorizzazioni per una stored procedure.|[Concedere autorizzazioni per una stored procedure](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|Viene descritto come restituire dati da una stored procedure a un'applicazione.|[Restituire dati da una stored procedure](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|Viene descritto come ricompilare una stored procedure.|[Ricompilare una stored procedure](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|Viene descritto come ridenominare una stored procedure.|[Rinominare una stored procedure](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|Viene descritto come visualizzare la definizione di una stored procedure.|[Visualizzare la definizione di una stored procedure](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|Viene descritto come visualizzare ciò che dipende da una stored procedure.|[Visualizzare le dipendenze di una stored procedure](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|Viene descritta la modalità d'uso dei parametri in una stored procedure.|[Parameters](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Stored procedure CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/clr-stored-procedures)  
 [Risoluzione dei nomi posticipata](../../t-sql/statements/create-trigger-transact-sql.md#deferred-name-resolution)
  
