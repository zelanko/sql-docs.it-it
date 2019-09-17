---
title: Novità di SSMA per DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/06/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 118cb0430a7db1afc2a7537fb19c24b22dc6dd1f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745376"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novità di SSMA per DB2 (DB2ToSQL)

Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche DB2 in ogni versione.

## <a name="ssma-v84"></a>SSMA v 8.4

La versione v 8.4 di SSMA per DB2 è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug correlato alle colonne di indice Max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

> [!IMPORTANT]
> Con SSMA v 7.4 e versioni successive, .NET 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v83"></a>SSMA v 8.3

La versione 8.3 di SSMA per DB2 è stata migliorata con correzioni mirate progettate per migliorare le metriche di qualità e conversione. Inoltre, questa versione di SSMA per DB2 fornisce le correzioni seguenti:

* Risolvere i problemi di accessibilità
* Aggiungere il supporto di base per il tipo ' hierarchyid ' in SQL Server
* Sostituire l'utilizzo della funzione TRIM nelle query di individuazione z/OS con RTRIM/LTRIM
* Consenti all'utente di specificare la raccolta di pacchetti durante la connessione in "modalità standard" (il valore predefinito è NULLID)
* Aggiungi conversione per CREATE TABLE come SELECT
* Migliorare le conversioni per le tabelle temporanee globali
* Risolvere un problema relativo alla verifica dell'univocità degli oggetti in ordine di priorità delle tabelle rispetto ai vincoli, se i nomi entrano in conflitto
* Risolvere un problema relativo al caricamento dei valori di colonna predefiniti per la data e il TIMESTAMP per z/OS
* Supporto del carattere di avanzamento riga Unicode (noto come NEL)
* Risolvere un problema relativo alla conversione del cursore con la clausola RETURN TO mancante
* Aggiungere il supporto per le etichette e il GOTO

## <a name="ssma-v82"></a>SSMA v8.2

La versione v 8.2 di SSMA per DB2 è stata migliorata con per risolvere i problemi relativi alle connessioni al database SQL di Azure dallo strumento Console di SSMA e la colonna COUNT_BIG nella dichiarazione delle visualizzazioni durante la conversione. Inoltre, questa versione include un set di correzioni mirato progettato per migliorare la qualità e la metrica di conversione, nonché le correzioni per:

* Un problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento dei .NET Framework durante l'installazione invisibile all'utente.
* Arresti anomali intermittenti che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto relativo all'aggiornamento automatico può provocare l'errore di un aggiornamento da SSMA v 8.1 a v 8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v 8.1 di SSMA per DB2 è stata migliorata per fornire correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto relativo all'aggiornamento automatico può provocare l'errore di un aggiornamento da SSMA v 8.0 a v 8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v 8.0 di SSMA per DB2 è stata migliorata per fornire correzioni mirate progettate per migliorare la qualità e la metrica di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **istanza gestita di database SQL di Azure** come destinazione. È ora possibile creare nuovi progetti destinati a Istanza gestita di database SQL di Azure:

  ![Progetto di database SQL MI](../media/ssma-newproject-sqldbmi.png)

* **Avviso di correzione**post-conversione. Altre informazioni sono disponibili [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione dello schema o del database preliminare.

  Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Se si selezionano solo gli schemi di cui si intende eseguire la migrazione, si risparmia tempo durante la connessione iniziale e si migliorano le prestazioni complessive del SSMA.

  ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v 7.10 di SSMA per DB2 contiene le modifiche seguenti:

* Correzioni mirate progettate per fornire protezione aggiuntiva per la sicurezza e la privacy per soddisfare le modifiche nei requisiti globali.
* Correzione per la conversione dei blocchi BEGIN-END.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v 7.9 di SSMA per DB2 contiene le modifiche seguenti:

* Correzioni mirate che migliorano le metriche di qualità e conversione.
* Supporto nella riga di comando di SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Supporto per la migrazione dei dati tramite SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS utilizzando l'opzione del menu di scelta rapida.
* La finestra di dialogo di connessione del database SQL di Azure in SSMA è stata anche modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v 7.8 di SSMA per DB2 contiene le modifiche seguenti:

* Modificare il mapping dei tipi evidenziato nelle impostazioni del progetto.
* Possibilità per gli utenti di disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v 7.7 di SSMA per DB2 contiene le modifiche seguenti:

* Correzioni mirate che migliorano le metriche di qualità e conversione.
* In base alla richiesta più diffusa, la versione a 32 bit di SSMA per DB2 è di nuovo. Rispetto all'implementazione precedente (precedente alla versione 7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile usare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione 7.6 di SSMA per DB2 è stata migliorata con correzioni mirate che migliorano le metriche di qualità e conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in versione di anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v 7.5 di SSMA per DB2 è stata migliorata con diversi miglioramenti per garantire una maggiore accessibilità per le persone affette da disabilità.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v 7.4 di SSMA per DB2 contiene le modifiche seguenti:

* L'opzione **query timeout** è ora disponibile durante l'individuazione di oggetti dello schema all'origine e alla destinazione.

  ![query timeout-opzione](../media/query-timeout_red.png)

* La metrica relativa alla qualità e alla conversione è stata migliorata con correzioni mirate, basate sui suggerimenti dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v 7.4. Inoltre, a partire da v 7.4, la versione a 32 bit di SSMA è stata sospesa.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v 7.3 di SSMA per DB2 contiene le modifiche seguenti:

* Miglioramento della qualità e della metrica di conversione con correzioni mirate basate sui suggerimenti dei clienti.
* SSMA Extensibility Framework esposto tramite gli elementi seguenti:
  * Esporta la funzionalità in un progetto di SQL Server Data Tools (SSDT).
    * È ora possibile esportare gli script dello schema da SSMA a un progetto SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche allo schema e distribuire il database.

      ![Comando Salva come progetto SSDT](../media/export-schema-scripts_red.png)
  * Librerie che possono essere utilizzate da SSMA per l'esecuzione di conversioni personalizzate.
    * È ora possibile costruire codice in grado di gestire le conversioni e le conversioni di sintassi personalizzate che non sono state precedentemente gestite da SSMA.
      * In questo post di Blog sono disponibili istruzioni per la creazione di un convertitore personalizzato, che [estende le funzionalità di conversione di SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Scaricare un progetto di esempio per la conversione da questo [post di Blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versione 7.2 di SSMA per DB2 contiene le modifiche seguenti:

* Miglioramento della qualità e della metrica di conversione con correzioni mirate basate sui suggerimenti dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per la risoluzione dei problemi dei clienti e per migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v 7.1 di SSMA per DB2 contiene le modifiche seguenti:

* SQL Server 2017 in Windows e Linux CTP1 è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e consente lo spostamento dello schema e dei dati per i server SQL di destinazione.
* Supporto per aggiornamenti automatici per scaricare la versione più recente di SSMA non appena disponibile.
* I file binari installabili di SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione 2016 di SSMA per DB2 contiene le seguenti modifiche:  

* Aggiunta del supporto per SQL Server 2016.
* Aggiunta della conversione di tabelle regolari e in memoria di DB2 a SQL Server funzionalità in memoria e Hekaton.
* Aggiunta della conversione dei controlli di accesso DB2 a oggetti Criteri di SQL Server (Sicurezza a livello di riga per DB2).
* Aggiunta della conversione di tabelle DB2 con controllo delle versioni di sistema in SQL Server tabelle temporali.
* Migliorato parser e resolver DB2.
* Controllo del programma di installazione rimosso per .NET 2,0.
* Rimosso *. dll superfluo dal programma di installazione di DB2.
* Corretti i comandi "Salva progetto" e "Apri progetto" per la console SSMA.
* Correzione del comando "SecurePassword" per la console di SSMA.
* Correzione del conteggio degli oggetti per il caricamento iniziale.
* Correzione del bug nelle impostazioni globali.
  
## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per DB2 aggiunge il supporto per la migrazione a SQL Server 2016.

## <a name="january-2016"></a>2016 gennaio

La versione di manutenzione di SSMA per DB2 di gennaio 2016 contiene le modifiche seguenti:  
  
* Aggiunta del supporto per numerose funzioni standard.  
* Correzione degli errori del parser DB2.  
* Correzione del supporto per DB2 V9 zOS (RFC 5690920).  
* Correzione degli errori di identificazione non risolta DB2 durante la conversione.  
* Aggiunta voce di menu Visualizza log a SSMA (RFC 5706203).  
* Aggiunta di dati di telemetria.
  
## <a name="november-2014"></a>2014 novembre

La versione di novembre 2014 di SSMA per DB2 era la versione iniziale.
