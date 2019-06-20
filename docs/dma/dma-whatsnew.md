---
title: Novità in Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
manager: jroth
ms.openlocfilehash: f88562c25982ce8c5d6c8d4b87dd629e4ba57c03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794305"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novità di Data Migration Assistant
Questo articolo elenca le aggiunte in ogni versione di Data Migration Assistant (DMA).

## <a name="dma-v43"></a>DMA v4.3

La versione v4.3 di DMA offre supporto per:

* Le raccomandazioni dello SKU per il Database SQL di Azure gestiti istanze basate sulla valutazione dei carichi di lavoro.
* Servizi Desktop remoto di SQL Server come origine per le valutazioni.
* Istanza gestita di valutazioni di processo dell'agente per il Database SQL di Azure come destinazione.
* La possibilità di ignorare determinate regole di valutazione; l'elenco dei codici di errore specificata nella proprietà 'ignoreErrorCodes' configurata in DMA non verrà visualizzato nei risultati di valutazione DMA.
* Valutazione delle query T-SQL in fasi attività processo e fornendo anche raccomandazioni appropriate
* Valutazioni degli eventi estesi (anteprima pubblica).

Inoltre, questa versione di DMA offre prestazioni migliori per la gestione di un numero elevato di oggetti dello schema nel database, nonché correzioni di bug relativi a:

* Procedure compilate con la compilazione nativa, in alcuni casi.
* Schemi di database complesse.

## <a name="dma-v42"></a>DMA v4.2

La versione v4.2 di DMA offre supporto della riga di comando per la valutazione della conformità di destinazione per uno o più istanze del server quando l'istanza gestita di eseguire la migrazione da un'istanza locale di SQL Server a un Database SQL di Azure. I clienti possono ora usare la riga di comando DMA per raccogliere i metadati relativi ai relativi schemi di database, individuare il blocco popup e informazioni sulle funzionalità parzialmente supportate o non supportata che influiscono sulla migrazione a un'istanza gestita di Database SQL di Azure. I risultati possono quindi essere eseguito il rendering utilizzando il modello di Power BI fornito.

## <a name="dma-v41"></a>DMA v4.1

La versione 4.1 di DMA introduce il supporto per la valutazione globale dei database di SQL Server in locale la migrazione a istanza gestita di Azure SQL Database.

Il flusso di lavoro di valutazione ti aiuta a rilevare i problemi seguenti, che possono influire sulla migrazione a istanza gestita di Azure SQL Database:

* **Non è supportato o funzionalità parzialmente supportate**. DMA valuta i database di SQL Server di origine per le funzionalità in uso che sono parzialmente supportate o non è supportato in istanza gestita di Azure SQL Database di destinazione. Quindi, lo strumento fornisce un set completo di indicazioni, approcci alternativi disponibili in Azure e l'attenuazione dei passaggi in modo che i clienti possono sfruttare queste informazioni in considerazione quando si pianificano i propri progetti di migrazione.

* **Problemi di compatibilità**. DMA inoltre identificati i problemi di compatibilità relativi alle aree seguenti:

  * Modifiche di rilievo:  Gli oggetti dello schema specifiche che potrebbero compromettere la funzionalità migrazione al database di destinazione.  Si consiglia di correggere questi oggetti dello schema dopo la migrazione del database.
  * Modifiche del comportamento: Gli oggetti dello schema segnalati continuino a funzionare, ma che potrebbero presentare un comportamento diverso, ad esempio un calo delle prestazioni.
  * Problemi informativi:  Questi oggetti non influisca sulla migrazione, ma potrebbero sono stati deprecati funzionalità di che versioni di SQL Server.

Dopo aver completata la valutazione, utilizzare nostri [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) (DMS) per eseguire la migrazione dei tuoi database di SQL Server a istanza gestita di Azure SQL Database.  Servizio migrazione del database supporta entrambe [offline](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (una tantum) e [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) le migrazioni del database (tempo di inattività minimo) per istanza gestita di Azure SQL Database.

## <a name="dma-v40"></a>DMA v4.0

La versione v4.0 di DMA introduce la funzionalità di raccomandazioni dello SKU del Database SQL di Azure, che consente agli utenti di identificare il valore minimo consigliato di SKU di Database SQL di Azure basati sui contatori delle prestazioni raccolti dai computer che ospita i database. Questa funzionalità offre consigli relativi ai prezzi di livello, a livello di calcolo e le dimensioni massime dei dati, nonché il costo stimato al mese. Offre inoltre la possibilità di eseguire il provisioning in blocco tutti i database in Azure.

> [!NOTE]
> Attualmente questa funzionalità sarà disponibile solo tramite l'interfaccia della riga di comando (CLI).

Per ulteriori informazioni, vedere l'articolo [identificare lo SKU del Database SQL di Azure corretto per il database locale](dma-sku-recommend-sql-db.md).

## <a name="dma-v36"></a>DMA v3.6

La versione v3.6 di DMA introduce "Correggi" per gli oggetti dello schema che sono interessati da blocchi di migrazione più comuni.

Questa versione fornisce autofix per il seguente blocco di migrazione e problemi di modifica del comportamento:

* Gli oggetti dello schema che utilizzano la sintassi di Join non qualificato.
* Gli oggetti dello schema che usano l'istruzione RAISEERROR legacy.
* Istruzioni SQL che usano ordine dall'intero valore letterale.

DMA esegue la conversione automatica dello schema per gli oggetti interessati dai problemi elencati e chiede all'utente una conferma prima di procedere con la conversione dello schema. Gli utenti possono esaminare le modifiche al codice suggerito e quindi accettare o rifiutare tutte le conversioni per qualsiasi oggetto di database specificato.

DMA utilizza la tecnologia Microsoft programma sintesi (PROSE) per suggerire che correzioni di codice. Altre informazioni sulle [PROSE](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>DMA v3.5

La versione v3.5 di DMA include le aggiunte seguenti:

* Miglioramenti significativi delle prestazioni per la migrazione al Database SQL di Azure (i test di benchmark indicano che il processo è quattro volte più veloce rispetto alle versioni precedenti di DMA).
* Il footprint di memoria è ulteriormente ottimizzato per migliorare la stabilità del flusso di lavoro della migrazione.
* La possibilità di ignorare le valutazioni durante le migrazioni di schema e i dati (se già stata eseguita la valutazione e risolti tutti gli oggetti dello schema di rilievo prima della migrazione).
* Una correzione per risolvere un problema con lo strumento in modo anomalo quando viene specificato un percorso di condivisione di rete non è valida per i file di backup, quando si esegue un aggiornamento di una versione legacy di SQL Server locale a una versione successiva o a SQL Server in macchine virtuali di Azure.

## <a name="dma-v34"></a>DMA v3.4

La versione di versione 3.4 di DMA include le aggiunte seguenti:

* Supporto per SQL Server 2017 come origine per le migrazioni di Database SQL di Azure.
* Miglioramenti alla stabilità, prestazioni e valutazione della correttezza di regola.

## <a name="dma-v33"></a>DMA v3.3

Il rilascio della versione 3.3 di DMA consente la migrazione di un'istanza di SQL Server locale alla nuova versione di SQL Server 2017 in Windows e Linux. Anche se il flusso di lavoro complessivo della migrazione per Windows e Linux è la stessa, il passaggio a SQL Server 2017 per Linux richiede un paio di considerazioni aggiuntive.

### <a name="specifying-the-back-up-path"></a>Che specifica il percorso di backup

Linux e Windows usano formati di percorso diversi. Di conseguenza, la migrazione a SQL Server 2017 in Linux richiede che l'utente fornisca le versioni di Windows sia Linux del percorso per il percorso del file fisico. È possibile specificare entrambe le versioni del percorso in modi diversi a seconda della posizione del file fisico.
Se il file di backup fisico è in un computer che esegue:

* Linux, usare un 'samba' condivide per condividere il file con altri computer nella rete.
* Windows, usare il comando '/mnt' per montare la condivisione nel computer che esegue Linux.

> [!NOTE]
> Dettagli dell'utilizzo di una condivisione 'samba' o il comando '/mnt' rientrano nell'ambito di questo articolo.

### <a name="migrating-windows-logins"></a>La migrazione gli account di accesso di Windows

Benché la migrazione degli account di accesso di Active Directory (AD) è ufficialmente supportata da SQL Server 2017 in Linux, richiede configurazione aggiuntiva per funzionare correttamente. Vedere l'articolo [autenticazione di Active Directory con SQL Server in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) per informazioni dettagliate sull'impostazione degli account di accesso di Active Directory in SQL Server 2017 in Linux. Dopo aver eseguito la configurazione richiesta, il programma di installazione è stata completata ed è possibile migrare gli account di accesso di Active Directory come di consueto. Autenticazione standard di SQL funziona come previsto senza alcuna configurazione aggiuntiva.

## <a name="dma-v32"></a>DMA v3.2

La versione v 3.2 di DMA include le aggiunte seguenti:

* Migrazione di schemi e dati sono abilitati dai database di SQL Server in locale per Database SQL di Azure con un nuovo flusso di lavoro di migrazione.
* Durante la migrazione dello schema al Database SQL di Azure, DMA generare script per oggetti di database di origine, vengono fornite indicazioni su come risolvere eventuali problemi di compatibilità e quindi distribuisce lo schema in Azure.

## <a name="dma-v31"></a>DMA v3.1

La versione v3.1 di DMA include le aggiunte seguenti:

* Le raccomandazioni di assessment migliorata per i database SQL di Azure in termini di regole di confronto del database, l'uso di non supportate stored procedure di sistema e gli oggetti CLR.
* Linee guida di valutazione per i livelli di compatibilità 130, 120, 110 e 100 durante la migrazione al database SQL di Azure.

## <a name="dma-v30"></a>DMA v3.0

La versione 3.0 di DMA estende la valutazione del database SQL di Azure per fornire raccomandazioni complete per aiutare a risolvere i problemi correlati a:

* Problemi di blocco della migrazione.
* Parzialmente o funzionalità non supportate e le funzioni.

## <a name="dma-v21"></a>DMA v2.1

La versione v2.1 di DMA include le aggiunte seguenti:

* Supporto della riga di comando per l'esecuzione delle valutazioni in modalità automatica, che consente di eseguire valutazioni su larga scala. Per ulteriori informazioni, vedere l'articolo [eseguito Data Migration Assistant da riga di comando](dma-commandline.md).
* Miglioramenti delle prestazioni quando gli utenti di avviano e chiudere DMA.
* La possibilità di configurare il timeout della connessione SQL. Per ulteriori informazioni, vedere l'articolo [impostazioni di configurazione per Data Migration Assistant](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v2.0

La versione 2.0 di DMA include migliorate raccomandazioni funzionalità per Stretch database per fornire tabelle in ordine di priorità appropriate che massimizzano i risparmi di archiviazione.

## <a name="dma-v10"></a>DMA v1.0

La versione v1.0 di DMA è la versione iniziale, e consente di:

* Individuazione dei problemi che possono influire sull'aggiornamento a una versione locale di SQL Server. Vengono descritti eventuali risultati come problemi di compatibilità e organizzati in categorie nelle aree seguenti:
  * Modifiche di rilievo
  * Modifiche del comportamento
  * Funzionalità deprecate
* Individuazione di nuove funzionalità alla piattaforma di SQL Server di destinazione che il database può trarre vantaggio dalla dopo un aggiornamento. Vengono descritti eventuali risultati come funzionalità consigliate e organizzati in categorie nelle aree seguenti:
  * Prestazioni
  * Sicurezza
  * Archiviazione
* Esperienze utente moderne per eseguire valutazioni.

## <a name="see-also"></a>Vedere anche

[Panoramica di Data Migration Assistant](../dma/dma-overview.md)
