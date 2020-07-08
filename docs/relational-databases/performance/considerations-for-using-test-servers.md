---
title: Considerazioni relative all'uso di server di prova | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ef09bd17effe13d415a30a1175e9279744813eca
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85655625"
---
# <a name="considerations-for-using-test-servers"></a>Considerazioni relative all'utilizzo di server di prova
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'utilizzo di un server di prova per ottimizzare un database su un server di produzione è un importante vantaggio offerto da Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Attraverso questa funzionalità è possibile ripartire su un server di prova il carico dell'overhead generato dall'ottimizzazione senza copiare i dati effettivi dal server di produzione al server di prova.  
  
> [!NOTE]  
>  La funzionalità di ottimizzazione del server di prova non è supportata nell'interfaccia utente grafica (GUI) di Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Per utilizzare correttamente questa funzionalità, valutare le considerazioni riportate nelle sezioni seguenti.  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>Configurazione dell'ambiente del server di prova e del server di produzione  
  
-   L'utente che desidera utilizzare un server di prova per ottimizzare un database su un server di produzione deve essere presente su entrambi i server, altrimenti l'operazione non riuscirà.  
  
-   Per usare lo scenario server di prova/server di produzione è necessario abilitare la stored procedure estesa **xp_msver**. [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata usa questa stored procedure estesa per recuperare le informazioni sul numero di processori e sulla memoria disponibile nel server di produzione da usare per l'ottimizzazione del server di prova. Se la stored procedure **xp_msver** non è abilitata, Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa le caratteristiche hardware del computer in cui viene eseguito Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se le caratteristiche hardware del computer su cui Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in esecuzione non sono disponibili, si suppone che siano disponibili un processore e 1024 MB di memoria. Questa stored procedure estesa è attiva per impostazione predefinita quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Configurazione superficie di attacco](../../relational-databases/security/surface-area-configuration.md) e [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata prevede che le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siano identiche nel server di prova e nel server di produzione. In caso contrario, l'edizione in uso nel server di prova ha la precedenza. Ad esempio, se nel server di prova è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition, Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] non includerà tra le indicazioni le viste indicizzate, il partizionamento e le operazioni online, anche se nel server di produzione è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition.  
  
## <a name="about-test-serverproduction-server-behavior"></a>Informazioni sul comportamento del server di prova e del server di produzione  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Nella generazione delle indicazioni, Ottimizzazione guidata tiene in considerazione le differenze hardware esistenti tra il server di produzione e il server di prova. L'indicazione è identica a quella che verrebbe generata nel caso in cui l'ottimizzazione venisse eseguita sul solo server di produzione.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata può imporre un carico aggiuntivo al server di produzione per la raccolta dei metadati e per la creazione delle statistiche necessarie per eseguire l'ottimizzazione.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata non copia i dati effettivi dal server di produzione sul server di prova, Vengono copiati unicamente i metadati dei database e le necessarie statistiche.  
  
-   Tutte le informazioni sulla sessione vengono archiviate in **msdb** sul server di produzione. In questo modo, per eseguire l'ottimizzazione è possibile utilizzare qualsiasi server di prova disponibile, mentre le informazioni relative a tutte le sessioni si trovano in un'unica posizione, ovvero sul server di produzione.  
  
## <a name="issues-related-to-the-shell-database"></a>Problemi relativi allo scheletro di database  
  
-   Dopo aver eseguito l'ottimizzazione, Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] rimuove tutti i metadati creati sul server di prova durante il processo di ottimizzazione. Viene rimosso anche lo scheletro di database. Se si stanno eseguendo più sessioni di ottimizzazione utilizzando gli stessi server di produzione e di prova, è possibile conservare lo scheletro di database per risparmiare tempo. Nel file di input XML specificare il sottoelemento **RetainShellDB** insieme agli altri sottoelementi all'interno dell'elemento padre **TuningOptions** . L'utilizzo di queste opzioni specifica a Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] di conservare lo scheletro di database. Per altre informazioni, vedere [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
-   Dopo una sessione di ottimizzazione riuscita che prevede l'utilizzo combinato di un server di prova e un server di produzione, è possibile che gli scheletri di database rimangano nel server di prova, anche se non è stato usato il sottoelemento **RetainShellDB** . Tali scheletri di database indesiderati possono interferire con le sessioni di ottimizzazione successive e devono essere eliminati prima di eseguire una nuova sessione di ottimizzazione che prevede l'utilizzo combinato di un server di prova e un server di produzione. Inoltre, se una sessione di ottimizzazione si interrompe in modo imprevisto, è possibile che gli scheletri di database nei server di prova e gli oggetti presenti in tali database rimangano nei server di prova. Prima di avviare una nuova sessione di ottimizzazione che prevede l'utilizzo combinato di un server di prova e un server di produzione è necessario eliminare anche tali database e oggetti.  
  
## <a name="issues-related-to-the-tuning-process"></a>Problemi relativi al processo di ottimizzazione  
  
-   L'utente deve controllare il contenuto del log di ottimizzazione per individuare eventuali errori di ottimizzazione causati dalle differenze esistenti tra il server di produzione e quello di prova ed errori risultanti dalla copia dei metadati dal server di produzione a quello di prova. Potrebbe ad esempio accadere che l'account di accesso di un utente non esista sul server di prova. Se l'account di accesso di un utente non è presente sul server di prova, gli eventi nel carico di lavoro generati da quell'utente potrebbero non essere ottimizzabili. Utilizzare la GUI di Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] per visualizzare il log di ottimizzazione. Per altre informazioni, vedere [Visualizzare e utilizzare l'output di Ottimizzazione guidata motore di database](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)  
  
-   Se Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] non riesce a ottimizzare molti eventi perché alcuni oggetti risultano mancanti nello scheletro di database creato da Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] nel server di prova, l'utente deve controllare il log di ottimizzazione. In questo log sono elencati gli eventi che non è possibile ottimizzare. Per ottimizzare correttamente il database sul server di prova, è necessario che l'utente crei gli oggetti mancanti nello scheletro di database e che quindi avvii una nuova sessione di ottimizzazione  
  
-   Se sul server di prova esiste già un database con lo stesso nome, Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] non copia i metadati, continua l'ottimizzazione e procede con la raccolta delle statistiche necessarie. Questa funzionalità è utile nel caso in cui l'utente abbia già creato un database sul server di prova e abbia copiato i metadati appropriati prima di eseguire Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Se sul server di produzione è stata attivata l'opzione DATE_CORRELATION_OPTIMIZATION per un database, i metadati e i dati associati a questa opzione non vengono inseriti completamente in uno script durante l'ottimizzazione del server di prova. Quando l'ottimizzazione viene eseguita in uno scenario con server di prova/server di produzione, possono verificarsi i problemi seguenti:  
  
    -   Possono essere presenti utenti con piani di query differenti sui server per query che utilizzano l'opzione DATE_CORRELATION_OPTIMIZATION.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata potrebbe consigliare di eliminare le viste indicizzate che impongono l'opzione DATE_CORRELATION_OPTIMIZATION nello script di indicazioni.  
  
     È pertanto possibile ignorare le indicazioni generate da Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] per le viste indicizzate relative alle statistiche di correlazione, dato che Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] ne conosce i costi ma non i vantaggi. [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ottimizzazione guidata potrebbe consigliare di non selezionare determinati indici, ad esempio gli indici cluster in colonne **datetime** , che potrebbero risultare utili quando l'opzione DATE_CORRELATION_OPTIMIZATION è abilitata.  
  
     Per determinare se una vista è basata su statistiche di correlazione, selezionare la colonna **is_date_correlation_view** della vista del catalogo [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md) .  
  
  
