---
title: Quali sono le novità di SSMA per SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 727ede7a057491eea2ea230d7057aa3228b5fc82
ms.sourcegitcommit: 40e55e55a73e39d447da87d9178f2b6067f39c6f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/12/2019
ms.locfileid: "66841111"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Quali sono le novità di SSMA per SAP ASE (SybaseToSQL)
Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche di SAP ASE (in precedenza SSMA per Sybase) in ogni versione.

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA per ASE SAP è stata migliorata con un set specifico di correzioni progettati per migliorare la qualità e le metriche di conversione, nonché correzioni per:

* Un problema con gli indici non cluster disabilitati dopo la migrazione dei dati.
* Rilevamento di .NET Framework durante l'installazione invisibile all'utente.
* Un blocco intermittente che si verifica quando viene scaricata una nuova versione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.1 SSMA per v8.2. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA per ASE SAP è stata migliorata con correzioni mirate che sono progettate per migliorare le metriche di qualità e la conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.0 SSMA per v8.1. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione 8.0 di SSMA per ASE SAP è stata migliorata con correzioni mirate progettate per migliorare la qualità e la conversione delle metriche. Inoltre, questa versione offre le nuove funzionalità seguenti:

* Supporto per **istanza gestita di Azure SQL Database** come destinazione. È ora possibile creare nuovi progetti destinati a istanza gestita di Azure SQL Database:

  ![Progetto di database SQL istanza Gestita](../media/ssma-newproject-sqldbmi.png)

* Post-conversione **correzione advisor**. Come descritto in dettaglio [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione database preliminare o nello schema.

  Quando ci si connette all'origine, l'utente può a questo punto selezionare i database/schemi di interesse. Selezionando solo gli schemi che si intende eseguire la migrazione verrà risparmiare tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

  ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA per ASE SAP è stata migliorata con correzioni mirate progettate per offrire maggiore sicurezza e protezione della privacy per soddisfare le modifiche nei requisiti globali.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per ASE SAP contiene le seguenti modifiche:

* Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze del progetto.
* Supporto per la migrazione dei dati usando SQL Server Integration Services (SSIS). Dopo la conversione dello schema, è possibile creare un pacchetto SSIS usando un'opzione di menu di scelta rapida.
* Finestra di dialogo di connessione Database SQL di Azure in SSMA è stato modificato anche per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso di Database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni di progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione di v 7.8 di SSMA per ASE SAP contiene le seguenti modifiche:

* Modificare il mapping dei tipi evidenziate nelle impostazioni del progetto.
* La possibilità per gli utenti disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per ASE SAP contiene le seguenti modifiche:

* SSMA per ASE SAP è stato migliorato con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
* La versione a 32 bit di SSMA per ASE SAP basato su richiesta comune, è nuovamente. Rispetto all'implementazione precedente (prima a v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività che si dispone. È sempre preferibile usare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per ASE SAP contiene le seguenti modifiche:

* Correzioni che consentono di migliorare le metriche di qualità e la conversione di destinazione e con il supporto per SQL Server 2017 (anteprima pubblica). Supporto per SQL Server 2017 in Windows e Linux è disponibile in anteprima pubblica e non deve essere usato per le migrazioni di produzione.
* Supporto per la conversione di funzioni di Sybase.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA per ASE SAP (in precedenza SSMA per Sybase) contiene le seguenti modifiche:

* Numerosi miglioramenti per assicurare maggiore accessibilità per persone affette da disabilità.
* Supporto per la sintassi CREATE o REPLACE.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per Sybase contiene le seguenti modifiche:

* Il **timeout Query** opzione ora è disponibile durante l'individuazione di oggetti dello schema all'origine e destinazione.

  ![query timeout-opzione](../media/query-timeout_red.png)
* La metrica della qualità e la conversione è stata migliorata con correzioni mirate, ai suggerimenti dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA verrà terminato a breve.  

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per Sybase contiene le seguenti modifiche:

* Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
* Framework di estendibilità SSMA esposta tramite gli elementi seguenti:
  * La funzionalità di esportazione in un progetto di SQL Server Data Tools (SSDT).
    * È ora possibile esportare gli script dello schema da SSMA per un progetto di SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche dello schema e distribuire il database.

        ![Salva come comando di progetto SSDT](../media/export-schema-scripts_red.png)
  * Librerie che possono essere usate da SSMA per l'esecuzione di conversioni personalizzate.
    * È ora possibile creare codice in grado di gestire le conversioni di sintassi personalizzata e che non sono stati precedentemente gestiti da SSMA.
      * Le istruzioni su come costruire un convertitore personalizzato sono disponibili in questo post di blog [funzionalità di conversione di estensione di SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Scaricare un progetto di esempio per la conversione da questo [post di blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versione di versione 7.2 di SSMA per Sybase contiene le seguenti modifiche:

* Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
* Miglioramenti della telemetria per fornire una migliore punti dati per risolvere i problemi dei clienti e migliorare il tasso di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione 7.1 di SSMA per Sybase contiene le seguenti modifiche:

* A questo punto, SQL Server 2017 in Windows e Linux CTP1 è una piattaforma di destinazione supportate per la migrazione. Questa funzionalità è disponibile in anteprima tecnica e supporta lo spostamento dei dati e lo schema per i server SQL di destinazione.
* Supporto per gli aggiornamenti automatici scaricare la versione più recente di SSMA, non appena è disponibile.
* I file binari installabili SSMA vengono ora forniti tramite file del pacchetto Windows installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per Sybase contiene le seguenti modifiche:  

* Aggiunta del supporto per SQL Server 2016.
* Rimosso controllo programma di installazione per .net 2.0.
* Pacchetto di estensioni delle dipendenze aggiornato da .net 3.5 a .net 4.0.
* Risolto "Salva progetto" e "open project" comandi per la Console SSMA.
* Comando fissa "securepassword" per la Console SSMA.
* Risolto il conteggio degli oggetti per il caricamento iniziale.
* Correzione del bug nelle impostazioni globali.

## <a name="march-2016"></a>Marzo 2016

La versione di anteprima di marzo 2016 di SSMA per Sybase aggiunge il supporto per la migrazione a SQL Server 2016.  
  
## <a name="january-2016"></a>Gennaio 2016

La versione di gennaio 2016 la manutenzione di SSMA per Sybase contiene le seguenti modifiche:  
  
* Voce di Menu Visualizza aggiunta Log per SSMA (RFC 5706203).  
* Aggiunti i dati di telemetria.

## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Conversione del codice di Azure SQL DB migliorata.  
* Spostare la funzionalità di estensione pack allo schema per supportare database SQL di Azure.  
* Miglioramenti delle prestazioni aggiunti testato per i database con oltre 10k oggetti.  
* Aggiunti miglioramenti dell'interfaccia utente per la gestione con un numero elevato di oggetti.  
* Aggiunta la possibilità di evidenziare gli schemi LOB "noti" (in modo che possono essere ignorati nella conversione).  
* Aggiunti miglioramenti di velocità di conversione.  
* Aggiunta la possibilità di visualizzare il numero di oggetti nell'interfaccia utente.
* Dimensioni del report ridotta da più di 25%.  
* Messaggi di errore migliorati per i costrutti non analizzati.  
  
## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Aggiunta del supporto di Microsoft SQL Server 2014.  
* Bug risolti riguardanti la conversione in Azure.  
* Bug risolti relative alle pagine del report invisibile in Internet Explorer 10.  
  
## <a name="january-2012"></a>Gennaio 2012

La versione di gennaio 2012 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Aggiunta del supporto per la conversione di trigger di rollback.
* Fornito correzione per la conversione di@ROWCOUNT e @@ERROR nella stessa istruzione SET.  
  
## <a name="july-2011"></a>Mese di luglio 2011

La versione di luglio 2011 di SSMA per Sybase fornisce migliorato di segnalazione errori durante la migrazione dei dati.  
  
## <a name="april-2011"></a>Ad aprile 2011

La versione di aprile 2011 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Prodotto "SSMA per Sybase" consolidato, che supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e SQL di Azure.  
* Aggiunta del supporto per la connessione e la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Aggiungere una nuova funzionalità per convertire ed eseguire la migrazione dei database Sybase a SQL di Azure.  
* Modulo di migrazione avanzata dei dati lato client, supporto per la migrazione parallela dei dati.  
* Alle prestazioni della migrazione dei dati migliorate con semplici e operazioni Bulk registrate di modelli di recupero.
* Aggiunta la possibilità di convertire correttamente e la migrazione dei database di Sybase distinzione maiuscole/minuscole in maiuscole/minuscole SQL Server.  
* Aggiunta del supporto per la conversione di istruzioni join di Sybase ASE Non ANSI per istruzioni di join ANSI SQL Server è stato esteso per eliminare e aggiornare le istruzioni.  
* Fornite opzioni di connettività aggiuntivo per la connessione al server di Sybase ASE mediante il provider ODBC di ASE Sybase e provider Sybase ASE ADO.Net.
* Rimuovere la dipendenza da un database separato denominato **SysDB**, che contiene le funzioni di emulazione di Sybase (installate come parte del pacchetto di estensione).
* Aggiunta la possibilità di installare SSMA per Sybase Extension Pack in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cluster.
* Aggiunta la compatibilità con le versioni precedenti dei progetti creati nelle versioni precedenti di SSMA (v4.0 e v4.2).  
* Aggiunta la possibilità di installare SSMA per Sybase v5.0 prodotti side-by-side (SxS) con le versioni precedenti di SSMA (v4.0 e v4.2).  
  
## <a name="july-2010"></a>Luglio 2010

La versione di luglio 2010 di SSMA per Sybase aggiunto:

* Supporto per la migrazione a SQL Server 2008 R2.  
* Una nuova applicazione Console SSMA per l'esecuzione della riga di comando.  
* Supporto per la migrazione dei dati tramite motori di migrazione dei dati lato Client e lato Server.  
* Supporto per l'istruzione "SELECT Custom" nella migrazione dei dati.  
* Supporto per la migrazione da Sybase ASE 15.0.3 e 15.5.  
  
## <a name="june-2008"></a>Giugno 2008

La versione di giugno 2008 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Aggiunta SSMA Tester, che consente di testare automaticamente la conversione di oggetti di database e la migrazione dei dati apportate da SSMA. Al termine di tutti i passaggi di migrazione di SSMA, utilizzare il Tester di SSMA per verificare che gli oggetti convertiti funzionano allo stesso modo e che tutti i dati è stato trasferito correttamente.
* Aggiunta la conversione di versioni precedenti a SQL. Utente può ora specificare tabella temporanea (e altri oggetti) dichiarazioni per ogni procedura di origine da utilizzare nella conversione.
* Aggiunti miglioramenti nella conversione degli oggetti:  
  * Crea un join conversione rivista.  
  * Funzioni di aggregazione e non aggregati senza avere/Raggruppa clausole.  
  * La funzione IDENTITY con un'istruzione SELECT INTO.  
  * Cluster i vincoli e indici su dati solo bloccati.  
  * Tabelle temporanee create da SELECT INTO.  
  * I vincoli o indici per le tabelle temporanee.  
  * Nuovo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 i tipi data/ora sono supportati.  
  * Supporto di connettività e tipi di dati Sybase 15.0.  
  
## <a name="may-2007"></a>Maggio 2007

La versione di maggio 2007 di SSMA per Sybase aggiunto:  
  
* La possibilità di caricare più rapidamente il contenuto di database durante il salvataggio di un progetto.  
* Supporto per i commenti immessi dall'utente in SQL Server formattata modalità SQL.  
* Miglioramenti nella conversione degli oggetti.  

## <a name="november-2006"></a>Novembre 2006

La versione di novembre 2006 di SSMA per Sybase contiene le seguenti modifiche:  
  
* Aggiunte nuove impostazioni globali:  
  * È possibile scegliere di visualizzare i numeri di riga nelle finestre dell'editor.  
  * È possibile configurare SSMA per la richiesta di sostituire gli oggetti duplicati o sostituire gli oggetti duplicati durante la conversione dello schema sempre o mai.  
* Aggiungere una nuova opzione di conversione che consente di configurare il modo in SSMA gestisce situazioni seguenti:  
  * Un'istruzione CAST o CONVERT che contiene una stringa binaria.  
  * Verifica dei valori null nelle espressioni di uguaglianza.  
  * Tabelle di proxy.  
  * Numeri di errore messaggio utente per RAISERROR.  
  * AGGIORNARE le istruzioni che contengono gli identificatori non risolti.  
* Aggiungere una nuova opzione di migrazione che consente di specificare come SSMA deve gestire date che si trovano all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervallo di date.  
* Aggiunto un **SQL formattati** impostazione nelle **SQL** scheda, che formatta il codice per una migliore leggibilità.  
* Correzioni di bug, tra cui:
  * SSMA è ora possibile convertita la tabella di blocco *tabella* IN {SHARED | Istruzioni in modalità esclusiva} mediante l'aggiunta di un hint TABLOCK o TABLOCKX alla successiva query SELECT sulla tabella.  
  * I cast necessari vengono aggiunti a questo punto quando vengono usati tipi binari nelle espressioni di caratteri.  
  * Miglioramenti delle prestazioni e memoria.  
  
## <a name="july-2006"></a>Luglio 2006

La versione di SSMA per Sybase di luglio 2006 costituisce la versione iniziale.  
  
## <a name="see-also"></a>Vedere anche

[Introduzione a SSMA per Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
