---
description: Opzione SORT_IN_TEMPDB per gli indici
title: Opzione SORT_IN_TEMPDB per gli indici | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- SORT_IN_TEMPDB option
- disk space [SQL Server], indexes
- space [SQL Server], indexes
- tempdb database [SQL Server], indexes
- indexes [SQL Server], tempdb database
- index creation [SQL Server], tempdb database
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f8f1ab5eb19e5590c5a4e3604469f93c2d524aac
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478182"
---
# <a name="sort_in_tempdb-option-for-indexes"></a>Opzione SORT_IN_TEMPDB per gli indici
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Quando si crea o si ricompila un indice, l'impostazione dell'opzione SORT_IN_TEMPDB su ON consente a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di usare **tempdb** per l'archiviazione dei risultati intermedi dell'ordinamento usati per la compilazione dell'indice. Questa opzione aumenta lo spazio su disco temporaneo necessario per creare un indice, ma può consentire di creare o ricompilare un indice in tempi più brevi se **tempdb** si trova in un set di dischi diverso rispetto al database utente. Per altre informazioni su **tempdb**, vedere [Configurare l'opzione di configurazione del server index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md).  
  
## <a name="phases-of-index-building"></a>Fasi della compilazione di un indice  
 La compilazione di un indice in [!INCLUDE[ssDE](../../includes/ssde-md.md)] include le fasi seguenti:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] esegue innanzitutto l'analisi delle pagine di dati della tabella di base per recuperare i valori di chiave e quindi compila una riga foglia dell'indice per ogni riga di dati. Quando i buffer di ordinamento interni vengono riempiti completamente con le voci dell'indice di livello foglia, le voci vengono ordinate e scritte su disco come operazione di ordinamento intermedia. A questo punto [!INCLUDE[ssDE](../../includes/ssde-md.md)] riprende l'analisi delle pagine di dati fino a quando i buffer di ordinamento non vengono di nuovo riempiti completamente. Questo processo, che prevede l'analisi di più pagine di dati seguita dall'ordinamento e dalla registrazione di un'operazione di ordinamento, continua finché non vengono elaborate tutte le righe della tabella di base.  
  
     Poiché in un indice cluster le righe foglia sono le righe dei dati della tabella, le operazioni di ordinamento intermedie includono tutte le righe di dati. In un indice non cluster, le righe foglia possono contenere colonne non chiave, ma sono in genere di dimensioni inferiori rispetto a quelle di un indice cluster. Se le chiavi dell'indice sono di grandi dimensioni o se l'indice contiene numerose colonne non chiave, un'operazione di ordinamento di un indice non cluster può essere estesa. Per altre informazioni sull'inclusione di colonne non chiave, vedere [Creare indici con colonne incluse](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] unisce i vari ordinamenti delle righe foglia dell'indice in un unico flusso ordinato. Il componente di [!INCLUDE[ssDE](../../includes/ssde-md.md)] che presiede all'unione delle operazioni di ordinamento inizia dalla prima pagina di ogni operazione, trova la chiave minore in tutte le pagine e quindi passa la riga foglia corrispondente al componente per la creazione dell'indice. Vengono quindi elaborate tutte le altre chiavi, dalla minore alla maggiore. Dopo aver estratto l'ultima riga foglia dell'indice da una pagina di un'operazione di ordinamento, il processo passa alla pagina successiva della stessa operazione di ordinamento. Quando sono state elaborate tutte le pagine di un extent di un'operazione di ordinamento, l'extent viene liberato. Ogni riga foglia passata al componente per la creazione dell'indice viene inserita in una pagina foglia dell'indice all'interno del buffer. Ogni pagina foglia viene scritta non appena viene riempita completamente. Man mano che vengono scritte le pagine foglia, [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila inoltre i livelli superiori dell'indice. Ogni pagina dell'indice di livello superiore viene scritta non appena viene riempita completamente.  
  
## <a name="sort_in_tempdb-option"></a>SORT_IN_TEMPDB - opzione  
 Se l'opzione SORT_IN_TEMPDB è impostata su OFF (impostazione predefinita), le operazioni di ordinamento vengono archiviate nel filegroup di destinazione. Durante la prima fase della creazione dell'indice, l'alternarsi delle operazioni di lettura delle pagine della tabella di base e delle operazioni di scrittura delle operazioni di ordinamento comporta lo spostamento delle testine di lettura/scrittura tra le diverse aree del disco. Le testine si trovano nell'area delle pagine di dati delle quali viene eseguita l'analisi, passano a un'area di spazio libero quando vengono riempiti completamente i buffer di ordinamento ed è necessario scrivere su disco l'operazione di ordinamento corrente, quindi tornano all'area delle pagine di dati non appena riprende l'analisi delle pagine della tabella. Il movimento delle testine di lettura/scrittura è più intenso nella seconda fase, durante la quale il processo di ordinamento in genere legge alternativamente le varie aree relative alle operazioni di ordinamento. Sia le operazioni di ordinamento che le pagine del nuovo indice vengono compilate nel filegroup di destinazione, a indicare che mentre [!INCLUDE[ssDE](../../includes/ssde-md.md)] distribuisce le letture tra le operazioni di ordinamento, deve passare periodicamente agli extent dell'indice per scrivere le nuove pagine dell'indice non appena vengono riempite completamente.  
  
 Se l'opzione SORT_IN_TEMPDB è impostata su ON e **tempdb** si trova in un set di dischi diverso rispetto al filegroup di destinazione, durante la prima fase le operazioni di lettura delle pagine di dati vengono eseguite in un disco diverso da quello in cui vengono eseguite le operazioni di scrittura nell'area delle operazioni di ordinamento in **tempdb**. Di conseguenza, le letture da disco delle chiavi di dati tendono a procedere in modo più seriale nel disco e anche le operazioni di scrittura nel disco di **tempdb** e quelle necessarie per compilare l'indice finale sono seriali. Anche se altri utenti utilizzano il database e accedono a diverse aree dei dischi, lo schema generale di lettura e scrittura risulta più efficiente se viene specificata l'opzione SORT_IN_TEMPDB.  
  
 L'opzione SORT_IN_TEMPDB può determinare una maggiore contiguità degli extent degli indici, in particolare se l'operazione CREATE INDEX non viene elaborata in parallelo. Gli extent dell'area delle operazioni di ordinamento vengono liberati in modo relativamente casuale rispetto alla relativa posizione nel database. Se le aree delle operazioni di ordinamento sono incluse nel filegroup di destinazione, man mano che vengono liberati gli extent di ordinamento possono essere acquisite dalle richieste di inclusione della struttura dell'indice negli extent mentre la struttura viene compilata. In una certa misura, ciò può comportare la distribuzione casuale degli extent dell'indice. Se gli extent di ordinamento sono separati in **tempdb**, la sequenza con cui vengono liberati non influisce sulla posizione degli extent dell'indice. Se le operazioni di ordinamento intermedie vengono archiviate in **tempdb** anziché nel filegroup di destinazione, inoltre, in quest'ultimo sarà disponibile una maggiore quantità di spazio e pertanto aumenteranno le probabilità che gli extent degli indici siano contigui.  
  
 L'opzione SORT_IN_TEMPDB ha effetto solo sull'istruzione corrente. Non sono presenti metadati che indicano se l'indice è stato ordinato o meno in **tempdb**. Ad esempio, se si crea un indice non cluster utilizzando l'opzione SORT_IN_TEMPDB e successivamente si crea un indice cluster senza specificare tale opzione, [!INCLUDE[ssDE](../../includes/ssde-md.md)] non la utilizza per ricreare l'indice non cluster.  
  
> [!NOTE]  
>  Se un'operazione di ordinamento non è necessaria o può essere eseguita in memoria, l'opzione SORT_IN_TEMPDB viene ignorata.  
  
## <a name="disk-space-requirements"></a>Requisiti relativi allo spazio su disco  
 Se si imposta l'opzione SORT_IN_TEMPDB su ON, è necessario che lo spazio disponibile su disco di **tempdb** sia sufficiente per contenere le operazioni di ordinamento intermedie e che lo spazio disponibile su disco del filegroup di destinazione sia sufficiente per contenere il nuovo indice. L'istruzione CREATE INDEX non viene eseguita correttamente se lo spazio libero non è sufficiente e se per qualche motivo non è possibile aumentare automaticamente le dimensioni del database in modo da acquisire lo spazio necessario. Ciò si verifica, ad esempio, se lo spazio su disco è insufficiente oppure se la funzione di aumento automatico delle dimensioni è disattivata.  
  
 Se l'opzione SORT_IN_TEMPDB è impostata su OFF, lo spazio libero nel filegroup di destinazione deve corrispondere approssimativamente alle dimensioni dell'indice finale. Durante la prima fase vengono compilate le operazioni di ordinamento, che richiedono uno spazio quasi equivalente a quello necessario per l'indice finale. Durante la seconda fase vengono elaborati e quindi liberati gli extent delle operazioni di ordinamento. Poiché tali extent vengono liberati a una velocità analoga a quella con cui vengono acquisiti altri extent destinati alle pagine dell'indice finale, i requisiti di spazio complessivi non superano di molto le dimensioni dell'indice finale. Uno degli effetti collaterali è rappresentato dal fatto che se la quantità di spazio libero equivale approssimativamente alle dimensioni dell'indice finale, [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenderà a riutilizzare gli extent delle operazioni di ordinamento non appena vengono liberati. Il fatto che gli extent delle operazioni di ordinamento vengano liberati in modo relativamente casuale rende meno continui gli extent dell'indice. Se l'opzione SORT_IN_TEMPDB è impostata su OFF, la continuità degli extent dell'indice è maggiore se lo spazio libero nel filegroup di destinazione è sufficiente per consentire di allocare gli extent dell'indice da un pool contiguo anziché dagli extent delle operazioni di ordinamento appena deallocati.  
  
Quando si crea un indice non cluster, deve essere disponibile una quantità di spazio libero corrispondete alle indicazioni seguenti:  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su ON, in **tempdb** deve essere disponibile spazio sufficiente per archiviare le operazioni di ordinamento e nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare la struttura finale dell'indice. Le operazioni di ordinamento includono le righe foglia dell'indice.  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su OFF, nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare la struttura finale dell'indice. È possibile che gli extent dell'indice abbiano una maggiore continuità se è disponibile una maggiore quantità di spazio libero.  
  
Quando si crea un indice cluster in una tabella che non contiene indici non cluster, deve essere disponibile una quantità di spazio libero corrispondente alle indicazioni seguenti:  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su ON, in **tempdb** deve essere disponibile spazio sufficiente per archiviare le operazioni di ordinamento, incluse le righe di dati della tabella. Nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare la struttura finale dell'indice, incluse le righe di dati della tabella e l'albero B dell'indice. Può essere necessario adeguare tale stima tenendo conto di fattori quali chiavi di grandi dimensioni oppure un fattore di riempimento con un valore basso.  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su OFF, nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare la tabella finale, inclusa la struttura dell'indice. È possibile che gli extent della tabella e dell'indice abbiano una maggiore continuità se è disponibile una maggiore quantità di spazio libero.  
  
Quando si crea un indice cluster in una tabella che contiene indici non cluster, deve essere disponibile una quantità di spazio libero corrispondente alle indicazioni seguenti:  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su ON, in **tempdb** deve essere disponibile spazio sufficiente per archiviare la raccolta delle operazioni di ordinamento relative all'indice di dimensioni maggiori (in genere l'indice cluster) e nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare le strutture finali di tutti gli indici, incluso l'indice cluster che contiene le righe di dati della tabella.  
  
-   Se l'opzione SORT_IN_TEMPDB è impostata su OFF, nel filegroup di destinazione deve essere disponibile spazio sufficiente per archiviare la tabella finale, incluse le strutture di tutti gli indici. È possibile che gli extent della tabella e dell'indice abbiano una maggiore continuità se è disponibile una maggiore quantità di spazio libero.  
  
## <a name="related-tasks"></a>Attività correlate  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [Riorganizzare e ricompilare gli indici](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [Configurare l'opzione di configurazione del server index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [Requisiti di spazio su disco per operazioni DDL sugli indici](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  
