---
title: Novità in SSMA per Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 50723f7b7161bbed960ce2f94e1b7bbf79d420d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938417"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novità in SSMA per Access (AccessToSQL)

Questo articolo elenca SQL Server Migration Assistant (SSMA) per le modifiche all'accesso in ogni versione.  

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA for Access è stata migliorata con correzioni mirate che sono progettate per migliorare le metriche di qualità e la conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.1 SSMA per v8.2. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

> [!IMPORTANT]
> Con v7.4 SSMA e versioni successive, .net 4.5.2 è un prerequisito di installazione.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA for Access è stata migliorata con correzioni mirate che sono progettate per migliorare le metriche di qualità e la conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico potrebbe essere il guasto di un aggiornamento dalla versione 8.0 SSMA per v8.1. Se si verifica questo errore,. scaricare la nuova versione e installarlo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione 8.0 di SSMA for Access è stata migliorata con correzioni mirate progettate per migliorare la qualità e la conversione delle metriche. Questa versione offre anche le nuove funzionalità seguenti:

* Supporto per **istanza gestita di Azure SQL Database** come destinazione. È ora possibile creare nuovi progetti destinati a istanza gestita di Azure SQL Database:

  ![Progetto di database SQL istanza Gestita](../media/ssma-newproject-sqldbmi.png)

* Post-conversione **correzione advisor**. Come descritto in dettaglio [qui](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selezione database preliminare o nello schema.

    Quando ci si connette all'origine, l'utente può a questo punto selezionare i database/schemi di interesse. Selezionando solo gli schemi che si intende eseguire la migrazione verrà risparmiare tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

   ![Oggetti filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA for Access è stata migliorata con correzioni mirate progettate per offrire maggiore sicurezza e protezione della privacy per soddisfare le modifiche nei requisiti globali.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per Access contiene le seguenti modifiche:

* Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze del progetto.
* Finestra di dialogo di connessione Database SQL di Azure in SSMA è stato modificato anche per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso di Database SQL di Azure doveva essere indicato in modo esplicito all'interno delle impostazioni di progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v 7.8 di SSMA per Access contiene le seguenti modifiche:

* Modificare il mapping dei tipi evidenziate nelle impostazioni del progetto.
* La possibilità per gli utenti disabilitare la telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per Access contiene le seguenti modifiche:

* Correzioni mirate che consentono di migliorare le metriche di qualità e la conversione.
* Basato su richiesta comune, la versione a 32 bit di SSMA per l'accesso è nuovamente. Rispetto all'implementazione precedente (prima v7.4), sono disponibili due pacchetti di installazione, ma non possono essere installati side-by-side. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività che si dispone. È sempre preferibile usare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA per l'accesso è stata migliorata con correzioni mirate che consentono di migliorare le metriche di qualità e la conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Supporto per SQL Server 2017 in Windows e Linux è disponibile in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA for Access è stata migliorata con numerosi miglioramenti per assicurare maggiore accessibilità per persone affette da disabilità.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per Access contiene le seguenti modifiche:

* Il **timeout Query** opzione ora è disponibile durante l'individuazione di oggetti dello schema all'origine e destinazione.

  ![query timeout-opzione](../media/query-timeout_red.png)

* La metrica della qualità e la conversione è stata migliorata con correzioni mirate, ai suggerimenti dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire da v7.4, la versione a 32 bit di SSMA è stata interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per Access contiene le seguenti modifiche:

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

Il rilascio della versione 7.2 di SSMA per Access contiene le seguenti modifiche:

* Metrica qualità e conversione migliorata con correzioni mirate ai suggerimenti dei clienti.
* Miglioramenti della telemetria per fornire una migliore punti dati per risolvere i problemi dei clienti e migliorare il tasso di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione 7.1 di SSMA per Access contiene le seguenti modifiche:

* A questo punto, SQL Server 2017 in Windows e Linux CTP1 è una piattaforma di destinazione supportate per la migrazione. Questa funzionalità è disponibile in anteprima tecnica e supporta lo spostamento dei dati e lo schema per i server SQL di destinazione.
* SSMA supporta ora gli aggiornamenti automatici per scaricare la versione più recente di SSMA, non appena è disponibile.
* I file binari installabili SSMA vengono ora forniti tramite file del pacchetto Windows installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiunta del supporto ufficiale per SQL Server 2016
* Rimosso controllo programma di installazione per .net 2.0.
* Risolto "Salva progetto" e "open project" comandi per la Console SSMA.
* Comando fissa "securepassword" per la Console SSMA.
* Risolto il conteggio degli oggetti per il caricamento iniziale.
* Correzione dei dati delle tabelle durante il caricamento per le schede di interfaccia utente per l'accesso.
* Correzione del bug nelle impostazioni globali. 

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per Access aggiunge il supporto per la migrazione a SQL Server 2016.  

## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2016 di SSMA per Access contiene le seguenti modifiche:  
  
* Funzione fixed non valido per impostazione predefinita di un campo GUID (RFC 3894811).  
* Blocco predefinito sull'importazione di record al Database SQL (Azure) (RFC 4919573).  
* Voce di Menu Visualizza aggiunta Log per SSMA (RFC 5706203).  
* Aggiunti i dati di telemetria.
  
## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per Access contiene le seguenti modifiche:  
  
* Conversione del codice di Azure SQL DB migliorata.  
* Spostare la funzionalità di estensione pack allo schema per supportare database SQL di Azure.  
* Miglioramenti delle prestazioni testate per i database con oggetti di oltre 10 k.  
* Aggiunti miglioramenti dell'interfaccia utente per la gestione con un numero elevato di oggetti.  
* Aggiunta del supporto per l'evidenziazione degli schemi LOB "noti" (in modo che possono essere ignorati nella conversione).  
* Aggiunti miglioramenti di velocità di conversione.
* Aggiunta del supporto per la visualizzazione oggetto conta nell'interfaccia utente.
* Dimensioni del report ridotta da più di 25%.
* Messaggi di errore migliorati per i costrutti non analizzati.  
  
## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiunta del supporto per Microsoft SQL Server 2014.
* Bug risolti riguardanti la conversione in Azure.  
* Bug risolti relative alle pagine del report invisibile in Internet Explorer 10.  
  
## <a name="january-2012"></a>Gennaio 2012

La versione di gennaio 2012 di SSMA per Access contiene le seguenti modifiche:  
  
* È disponibile l'opzione per non rendere persistente il nome utente e password per MS Access collegato tabelle dopo la migrazione.  
* Impostare le azioni cascade per riferimenti circolari No Action.  
* Condizione messaggi appropriati che indicano le operazioni di propagazione per i riferimenti circolari sono stati impostati su No Action.  
  
## <a name="july-2011"></a>Mese di luglio 2011

La versione di luglio 2011 di SSMA per Access aggiunge migliorato di segnalazione errori durante la migrazione dei dati.  
  
## <a name="april-2011"></a>Ad aprile 2011

La versione aprile 2011 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiunto installabile di "SSMA per Access", che supporta un unico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" e SQL di Azure.  
* Aggiunta la possibilità di connettersi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Aggiunta di SSMA per la versione della Console di accesso supporta per garantire la compatibilità con le versioni precedenti. È possibile aprire i progetti creati nelle versioni precedenti a v5.0 SSMA.
* Aggiunta la possibilità di installare SSMA v5.0 prodotto affiancata (SxS) con le versioni precedenti del prodotto SSMA.  
  
## <a name="july-2010"></a>Luglio 2010  
La versione di luglio 2010 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiunta del supporto per la migrazione a SQL Server 2008 R2 e SQL di Azure.
* Aggiungere una connessione protetta a SQL Server e SQL di Azure.  
* Aggiunta del supporto per i database di Access 2010.
* Aggiungere una nuova applicazione Console SSMA per l'esecuzione della riga di comando.
* Aggiunta del supporto per il tipo di dati DateTime2 di SQL Server.
  
## <a name="june-2008"></a>Giugno 2008

La versione di giugno 2008 di SSMA per Access aggiunge il supporto per i database di Access 2007.  
  
## <a name="may-2007"></a>Maggio 2007

La versione di maggio 2007 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiunta del supporto per i database di Access che usano i criteri di gruppo di lavoro.  
* È stato possibile eliminare gli oggetti convertiti dal Visualizzatore metadati SQL Server.  
* Aggiunta del supporto per i commenti immessi dall'utente in SQL Server formattata modalità SQL.  
* Aggiunti miglioramenti nella conversione degli oggetti.  
  
## <a name="november-2006"></a>Novembre 2006

La versione di novembre 2006 di SSMA per Access contiene le seguenti modifiche:  
  
* Aggiungere una nuova migrazione guidata di Database che agevola la migrazione di un singolo database da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
* Aggiunto un nuovo Convert, Load, e il comando Migra che converte i database di Access, carica gli oggetti convertiti nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e viene eseguita la migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tutto in un unico passaggio.  
* Migrazione di query migliorato. Eseguire una query migrazione ora converte selezionare più query da viste. Per altre informazioni, vedere [conversione di oggetti di Database di Access](converting-access-database-objects-accesstosql.md).  
* Aggiunta la possibilità di modificare le proprietà di tabelle e indici sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tabella** scheda.  
* Aggiunte nuove impostazioni globali:
  * È possibile scegliere di visualizzare i numeri di riga nelle finestre dell'editor.  
  * È possibile configurare SSMA per la richiesta di sostituire gli oggetti duplicati o sostituire gli oggetti duplicati durante la conversione dello schema sempre o mai.  
* Aggiungere una nuova opzione di conversione che consente di specificare se SSMA viene visualizzato un avviso quando una query complessa contiene un carattere jolly.  
  
## <a name="july-2006"></a>Luglio 2006

La versione di luglio 2006 di SSMA per Access era la versione iniziale.
