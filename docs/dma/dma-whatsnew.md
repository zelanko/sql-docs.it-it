---
title: Novità di Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
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
ms.openlocfilehash: 2a4780c9be50275959a0f32091b90c518ccea124
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000589"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novità di Data Migration Assistant
Questo articolo elenca le aggiunte in ogni versione di Data Migration Assistant (DMA).

## <a name="dma-v45"></a>DMA v 4.5

La versione 4.5 di DMA fornisce supporto per la valutazione della migrazione dei pacchetti di SQL Server Integration Services (SSIS) ospitati nel file System al database SQL di Azure o istanza gestita di database SQL di Azure.

## <a name="dma-v44"></a>DMA v 4.4

La versione 4.4 di DMA fornisce il supporto per il caricamento delle valutazioni in Azure Migrate.

## <a name="dma-v43"></a>DMA v 4.3

La versione v 4.3 di DMA fornisce supporto per:

* Raccomandazioni dello SKU per le istanze gestite del database SQL di Azure in base alla valutazione del carico di lavoro.
* RDS SQL Server come origine per le valutazioni.
* Valutazioni dei processi di Agent per istanza gestita di database SQL di Azure come destinazione.
* Possibilità di ignorare determinate regole di valutazione; l'elenco dei codici di errore specificati nella proprietà' ignoreErrorCodes ' configurata in DMA non verrà visualizzato nei risultati della valutazione DMA.
* Valutazione delle query T-SQL nei passaggi delle attività dei processi e fornire consigli appropriati
* Valutazioni degli eventi estesi (anteprima pubblica).

Inoltre, questa versione di DMA fornisce prestazioni migliorate per la gestione di un numero elevato di oggetti dello schema nei database, oltre a correzioni di bug relative a:

* Procedure compilate con la compilazione nativa, in alcuni casi.
* Schemi di database complicati.

## <a name="dma-v42"></a>DMA v 4.2

La versione v 4.2 di DMA fornisce supporto della riga di comando per la valutazione della conformità della destinazione per una o più istanze del server quando si esegue la migrazione da SQL Server locali a un'istanza gestita di database SQL di Azure. I clienti possono ora usare la riga di comando DMA per raccogliere i metadati relativi allo schema del database, rilevare i blocchi e ottenere informazioni sulle funzionalità parzialmente supportate o non supportate che influiscono sulla migrazione a un'istanza gestita di database SQL di Azure. I risultati possono quindi essere sottoposti a rendering usando il modello di Power BI fornito.

## <a name="dma-v41"></a>DMA v 4.1

La versione 4.1 di DMA introduce il supporto per la valutazione completa dei database SQL Server locali che eseguono la migrazione a Istanza gestita di database SQL di Azure.

Il flusso di lavoro di valutazione consente di rilevare i seguenti problemi che possono influire sulla migrazione a Istanza gestita di database SQL di Azure:

* **Funzionalità non supportate o parzialmente supportate**. DMA valuta il database di origine SQL Server per le funzionalità in uso che sono parzialmente supportate o non supportate nel Istanza gestita di database SQL di Azure di destinazione. Lo strumento offre quindi un set completo di indicazioni, approcci alternativi disponibili in Azure e procedure di mitigazione in modo che i clienti possano prendere in considerazione queste informazioni durante la pianificazione dei progetti di migrazione.

* **Problemi di compatibilità**. DMA consente inoltre di identificare i problemi di compatibilità correlati alle aree seguenti:

  * Modifiche di rilievo:  Oggetti dello schema specifici che potrebbero interrompere la migrazione della funzionalità al database di destinazione.  Si consiglia di correggere questi oggetti dello schema dopo la migrazione del database.
  * Modifiche comportamentali: Gli oggetti dello schema segnalati possono continuare a funzionare, ma possono presentare un comportamento diverso, ad esempio una riduzione delle prestazioni.
  * Problemi informativi:  Questi oggetti non avranno alcun effetto sulla migrazione, ma potrebbero essere stati deprecati dalla funzionalità SQL Server versioni.

Al termine della valutazione, usare il [servizio migrazione del database di Azure](https://azure.microsoft.com/services/database-migration/) (DMS) per eseguire la migrazione dei database di SQL Server al istanza gestita di database SQL di Azure.  DMS supporta le migrazioni di database sia [offline](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (monouso) che [online](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) (minimo tempo di inattività) per istanza gestita di database SQL di Azure.

## <a name="dma-v40"></a>DMA v 4.0

La versione 4.0 di DMA introduce la funzionalità di consigli per lo SKU del database SQL di Azure, che consente agli utenti di identificare la SKU minima consigliata del database SQL di Azure in base ai contatori delle prestazioni raccolti dai computer che ospitano i database. Questa funzionalità fornisce consigli relativi al piano tariffario, al livello di calcolo e alle dimensioni massime dei dati, oltre ai costi stimati al mese. Offre inoltre la possibilità di eseguire il provisioning di tutti i database in Azure in blocco.

> [!NOTE]
> Questa funzionalità è attualmente disponibile solo tramite l'interfaccia della riga di comando (CLI).

Per altri dettagli, vedere l'articolo [identificare lo SKU del database SQL di Azure appropriato per il database locale](dma-sku-recommend-sql-db.md).

## <a name="dma-v36"></a>DMA v 3.6

La versione 3.6 di DMA introduce la correzione automatica per gli oggetti dello schema interessati dai blocchi di migrazione più comuni.

Questa versione fornisce Autofix per il blocco di migrazione e i problemi di modifica del comportamento seguenti:

* Oggetti dello schema che usano la sintassi di join non qualificata.
* Oggetti dello schema che usano l'istruzione RAISEERROR legacy.
* Istruzioni SQL che usano order by Integer Literal.

DMA esegue la conversione automatica dello schema per gli oggetti interessati dai problemi elencati e chiede conferma all'utente prima di procedere con la conversione dello schema. Gli utenti possono esaminare le modifiche del codice suggerite e quindi accettare o rifiutare tutte le conversioni per un determinato oggetto di database.

DMA usa la tecnologia Microsoft Program Synthesis (prosa) per suggerire le correzioni del codice. Scopri di più su [prosa](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>DMA v 3.5

La versione 3.5 di DMA include le aggiunte seguenti:

* Miglioramenti significativi delle prestazioni per la migrazione al database SQL di Azure (i test di benchmark indicano che il processo è quattro volte più veloce rispetto alle versioni precedenti di DMA).
* Il footprint di memoria è ulteriormente ottimizzato per migliorare la stabilità del flusso di lavoro di migrazione.
* Possibilità di ignorare le valutazioni durante le migrazioni dello schema e dei dati (se la valutazione è già stata eseguita e sono stati risolti tutti gli oggetti dello schema di rilievo prima della migrazione).
* Correzione per risolvere un problema con lo strumento che si arresta in modo anomalo quando viene fornito un percorso di condivisione di rete non valido per i file di backup, quando si esegue un aggiornamento di una versione legacy di SQL Server locale a una versione successiva o di SQL Server in macchine virtuali di Azure.

## <a name="dma-v34"></a>DMA v 3.4

La versione 3.4 del DMA include le aggiunte seguenti:

* Supporto per SQL Server 2017 come origine per le migrazioni nel database SQL di Azure.
* Miglioramenti alla correttezza delle regole di stabilità, prestazioni e valutazione.

## <a name="dma-v33"></a>DMA v 3.3

La versione 3.3 di DMA consente la migrazione di un'istanza di SQL Server locale alla nuova versione di SQL Server 2017, sia in Windows che in Linux. Anche se il flusso di lavoro di migrazione complessivo per Windows e Linux è lo stesso, il passaggio a SQL Server 2017 per Linux richiede alcune considerazioni aggiuntive.

### <a name="specifying-the-back-up-path"></a>Specifica del percorso di backup

Linux e Windows usano formati di percorso diversi. Di conseguenza, per eseguire la migrazione a SQL Server 2017 in Linux è necessario che l'utente fornisca le versioni Windows e Linux del percorso al percorso del file fisico. È possibile specificare entrambe le versioni del percorso in modi diversi a seconda della posizione del file fisico.
Se il file di backup fisico si trova in un computer che esegue:

* Linux, usare una condivisione "Samba" per condividere il file con altri computer della rete.
* Usare il comando "mnt" per montare la condivisione nel computer che esegue Linux.

> [!NOTE]
> I dettagli dell'uso di una condivisione ' Samba ' o del comando ' mnt ' esulano dall'ambito di questo articolo.

### <a name="migrating-windows-logins"></a>Migrazione degli account di accesso di Windows

Sebbene la migrazione degli account di accesso di Active Directory (AD) sia ufficialmente supportata da SQL Server 2017 in Linux, è necessario che la configurazione aggiuntiva funzioni correttamente. Per informazioni dettagliate sulla configurazione degli account di accesso Active Directory in SQL Server 2017 in Linux, vedere l'articolo [Active Directory autenticazione con SQL Server in Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) . Dopo aver eseguito la configurazione richiesta, l'installazione è stata completata ed è possibile eseguire la migrazione di Active Directory accessi come di consueto. L'autenticazione SQL standard funziona come previsto senza alcuna configurazione aggiuntiva.

## <a name="dma-v32"></a>DMA v 3.2

La versione 3.2 di DMA include le aggiunte seguenti:

* La migrazione dello schema e dei dati è abilitata dai database SQL Server locali al database SQL di Azure con un nuovo flusso di lavoro di migrazione.
* Durante la migrazione dello schema al database SQL di Azure, DMA esegue lo script degli oggetti di database di origine, fornisce informazioni aggiuntive su come risolvere i potenziali problemi di compatibilità e quindi distribuisce lo schema in Azure.

## <a name="dma-v31"></a>DMA v 3.1

La versione v 3.1 di DMA include le aggiunte seguenti:

* Suggerimenti per la valutazione migliorati per i database SQL di Azure in termini di regole di confronto del database, uso di stored procedure di sistema non supportate e di oggetti CLR.
* Guida alla valutazione per i livelli di compatibilità 130, 120, 110 e 100 durante la migrazione a database SQL di Azure.

## <a name="dma-v30"></a>DMA v3.0

La versione 3.0 di DMA estende la valutazione del database SQL di Azure per fornire consigli completi per la risoluzione dei problemi relativi a:

* Problemi di blocco della migrazione.
* Funzionalità e funzioni parzialmente o non supportate.

## <a name="dma-v21"></a>DMA v 2.1

La versione 2.1 di DMA include le aggiunte seguenti:

* Supporto della riga di comando per l'esecuzione di valutazioni in modalità automatica, che consente di eseguire valutazioni su larga scala. Per altri dettagli, vedere l'articolo [eseguire Data Migration Assistant dalla riga di comando](dma-commandline.md).
* Miglioramenti delle prestazioni quando gli utenti avviano e chiudono DMA.
* Possibilità di configurare il timeout della connessione SQL. Per ulteriori dettagli, vedere l'articolo [relativo alle impostazioni di configurazione per Data Migration Assistant](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v 2.0

La versione 2.0 di DMA include consigli sulle funzionalità di stretch database migliorati per fornire tabelle con priorità appropriate per ottimizzare il risparmio di spazio di archiviazione.

## <a name="dma-v10"></a>DMA v1.0

La versione 1.0 di DMA è la versione iniziale e fornisce:

* Individuazione di problemi che possono influire sull'aggiornamento a una versione locale di SQL Server. I risultati vengono descritti come problemi di compatibilità e sono suddivisi in categorie nelle aree seguenti:
  * Modifiche di rilievo
  * Modifiche del comportamento
  * Funzionalità deprecate
* Individuazione di nuove funzionalità nella piattaforma SQL Server di destinazione di cui il database può trarre vantaggio dopo un aggiornamento. I risultati sono descritti come raccomandazioni sulle funzionalità e sono suddivisi in categorie nelle aree seguenti:
  * Prestazioni
  * Security
  * Archiviazione
* Esperienza utente moderna per eseguire valutazioni.

## <a name="see-also"></a>Vedere anche

[Panoramica di Data Migration Assistant](../dma/dma-overview.md)
