---
title: Novità di SSMA per Access (AccessToSQL) Documenti Microsoft
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: 2fd3da31e6a635a65f3d2a2f75320dd0586159d9
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625579"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Novità di SSMA per Access (AccessToSQL)

In questo articolo vengono elencate le modifiche di Accesso in ogni versione di SQL ServerSQL Server Migration Assistant (SSMA) per le modifiche di Access.This article lists SQL Server Migration Assistant (SSMA) for Access changes in each release.

## <a name="ssma-v88"></a>SSMA v8.8

La versione v8.8 di SSMA for Access include:

* Miglioramenti alla stabilità della sincronizzazione degli oggetti di SQL ServerSQL Server objects synchronization stability improvements
* Miglioramenti delle prestazioni dell'interfaccia grafica durante la valutazione e la conversione
* Nuovo parser di sintassi di Access per migliorare ulteriormente le prestazioni di conversione

## <a name="ssma-v87"></a>SSMA v8.7

La versione v8.7 di SSMA per `IIF` l'accesso ha migliorato la conversione per la funzione nelle query, nonché correzioni minori e miglioramenti delle prestazioni nell'interfaccia utente grafica.

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v86"></a>SSMA v8.6

Oltre a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni, la versione v8.6 di SSMA per l'accesso è stata migliorata aggiungendo un'impostazione che consente agli utenti di omettere le proprietà estese SSMA nel codice convertito.

Per utilizzare questa impostazione, in SSMA per Access passare a **Strumenti** > **Impostazioni** > di progetto**Conversione****generale** > , quindi in **Varie**aggiornare il valore dell'impostazione **Omettere proprietà estese** su **Sì**.

![Omettere l'impostazione delle proprietà estese](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 e versioni successive, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v85"></a>SSMA v8.5

La versione v8.5 di SSMA for Access è stata migliorata con il supporto per l'autenticazione di Azure Active Directory e il supporto di base per le funzionalità JSON nel server SQL, insieme a un set mirato di correzioni progettate per migliorare l'usabilità e le prestazioni.

Inoltre, SSMA per Access ora supporta la`ISNULL`conversione di più funzioni standard ( , `IIF`, e così via).

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 è un prerequisito per l'installazione. Se è necessario installare questa versione, è possibile scaricare il file di runtime da [qui](https://dotnet.microsoft.com/download/dotnet-framework/net472).

## <a name="ssma-v84"></a>SSMA v8.4

La versione v8.4 di SSMA per l'accesso è stata migliorata con correzioni mirate progettate per risolvere i problemi di accessibilità e correggere un bug relativo alle colonne di indice max (per consentire 32 anziché 16) per SQL Server 2016 e versioni successive.

> [!IMPORTANT]
> Con SSMA versioni 7.4 anche 8.4, .NET 4.5.2 è un prerequisito per l'installazione.

## <a name="ssma-v83"></a>SSMA v8.3

La versione v8.3 di SSMA for Access è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Inoltre, questa versione di SSMA per l'accesso fornisce correzioni che:In addition, this release of SSMA for Access provides fixes that:

* Risolvere i problemi di accessibilità.
* Aggiungere il `hierarchyid` supporto di base per il tipo in SQL Server.Add basic support for type in SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

La versione v8.2 di SSMA for Access è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.1 a v8.2. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versione v8.1 di SSMA for Access è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione.

> [!NOTE]
> Un problema noto con l'aggiornamento automatico può causare l'errore di un aggiornamento da SSMA v8.0 a v8.1. Se si verifica questo errore, scaricare la nuova versione e installarla manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versione v8.0 di SSMA for Access è stata migliorata con correzioni mirate progettate per migliorare la qualità e le metriche di conversione. Questa versione offre anche le seguenti nuove funzionalità:

* Supporto per **l'istanza gestita del database SQL** di Azure come destinazione. È ora possibile creare nuovi progetti destinati all'istanza gestita del database SQL di Azure:You can now create new projects targeting Azure SQL Database Managed Instance:

  ![Progetto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Avviso **fix**post-conversione . Scopri di più [qui](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733).

* Selezione preliminare di database/schema.

    Quando ci si connette all'origine, l'utente può ora selezionare database/schemi di interesse. Selezionando solo gli schemi che si prevede di eseguire la migrazione si risparmia tempo durante la connessione iniziale e migliorare le prestazioni complessive SSMA.

   ![Oggetti filtro SSMASSMA filter objects](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versione v7.10 di SSMA for Access è stata migliorata con correzioni mirate progettate per fornire ulteriori protezioni di sicurezza e privacy per soddisfare le modifiche dei requisiti globali.

## <a name="ssma-v79"></a>SSMA v7.9

La versione v7.9 di SSMA per l'accesso contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* Supporto nella riga di comando SSMA per modificare il mapping dei tipi di dati e le preferenze di progetto.
* Anche la finestra di dialogo di connessione al database SQL di Azure in SSMA è stata modificata per specificare il nome completo del server. Nelle versioni precedenti di SSMA, il prefisso del database SQL di Azure doveva essere menzionato in modo esplicito all'interno delle impostazioni dei progetti.

## <a name="ssma-v78"></a>SSMA v7.8

La versione v7.8 di SSMA per l'accesso contiene le seguenti modifiche:

* Modificare il mapping dei tipi evidenziato in Impostazioni progetto.
* Possibilità per gli utenti di disabilitare i dati di telemetria.

## <a name="ssma-v77"></a>SSMA v7.7

La versione v7.7 di SSMA per l'accesso contiene le seguenti modifiche:

* Correzioni mirate che migliorano la qualità e le metriche di conversione.
* In base alla richiesta popolare, la versione a 32 bit di SSMA per l'accesso è tornato. Rispetto all'implementazione precedente (prima della v7.4), esistono due pacchetti di installazione, ma non possono essere installati affiancati. Di conseguenza, è necessario scegliere la versione più appropriata in base ai componenti di connettività disponibili. È sempre preferibile utilizzare la versione a 64 bit, se possibile.

## <a name="ssma-v76"></a>SSMA v7.6

La versione v7.6 di SSMA for Access è stata migliorata con correzioni mirate che migliorano la qualità e le metriche di conversione e con il supporto per SQL Server 2017 (anteprima pubblica). Il supporto per SQL Server 2017 in Windows e Linux è in anteprima pubblica e non deve essere usato per le migrazioni di produzione.

## <a name="ssma-v75"></a>SSMA v7.5

La versione v7.5 di SSMA for Access è stata migliorata con diversi miglioramenti per garantire una maggiore accessibilità per gli utenti disabili.

## <a name="ssma-v74"></a>SSMA v7.4

La versione v7.4 di SSMA per l'accesso contiene le seguenti modifiche:

* L'opzione **Timeout query** è ora disponibile durante l'individuazione degli oggetti dello schema nell'origine e nella destinazione.

  ![opzione di timeout della query](../media/query-timeout_red.png)

* La metrica di qualità e conversione è stata migliorata con correzioni mirate, in base al feedback dei clienti.

  > [!IMPORTANT]
  > .NET 4.5.2 è un prerequisito per l'installazione di SSMA v7.4. Inoltre, a partire dalla v7.4, la versione a 32 bit di SSMA è stata interrotta.

## <a name="ssma-v73"></a>SSMA v7.3

La versione v7.3 di SSMA per l'accesso contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Framework di estendibilità SSMA esposto tramite gli elementi seguenti:SSMA extensibility framework exposed via the following items:
  * Funzionalità di esportazione in un progetto SQL Server Data Tools (SSDT).
    * È ora possibile esportare gli script dello schema da SSMA a un progetto SSDT. È possibile utilizzare gli script dello schema per apportare ulteriori modifiche allo schema e distribuire il database.

        ![Comando salva come progetto SSDT](../media/export-schema-scripts_red.png)
  * Librerie che possono essere utilizzate da SSMA per l'esecuzione di conversioni personalizzate.
    * È ora possibile costruire codice in grado di gestire le conversioni di sintassi personalizzate e le conversioni che non sono state gestite in precedenza da SSMA.
      * Le istruzioni su come costruire un convertitore personalizzato, insieme a un progetto di esempio per la conversione, sono disponibili nel post di blog Estensione delle funzionalità di [conversione di Assistente migrazione SQL Server.](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)

## <a name="ssma-v72"></a>SSMA v7.2

La versione v7.2 di SSMA per l'accesso contiene le seguenti modifiche:

* Metriche di qualità e conversione migliorate con correzioni mirate in base al feedback dei clienti.
* Miglioramenti della telemetria per fornire punti dati migliori per risolvere i problemi dei clienti e migliorare i tassi di conversione di SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versione v7.1 di SSMA per l'accesso contiene le seguenti modifiche:

* SQL Server 2017 SQL su CTP1 di Windows e Linux è ora una piattaforma di destinazione supportata per la migrazione. Questa funzionalità è in anteprima tecnica e supporta lo spostamento di schema e dati ai server SQL di destinazione.
* SSMA ora supporta gli aggiornamenti automatici per scaricare la versione più recente di SSMA non appena è disponibile.
* I file binari installabili SSMA vengono ora recapitati tramite i file del pacchetto di Windows Installer (MSI).

## <a name="may-2016"></a>Maggio 2016

La versione di maggio 2016 di SSMA per l'accesso contiene le seguenti modifiche:

* Aggiunto il supporto ufficiale per SQL Server 2016.
* È stato rimosso il controllo del programma di installazione per .NET 2.0.Removed installer check for .NET 2.0.
* Risolto `save-project` `open-project` e comandi per la console SSMA.
* Comando `securepassword` fisso per la console SSMA.
* Corretto il conteggio degli oggetti per il caricamento iniziale.
* Correzione del caricamento dei dati delle tabelle per le schede dell'interfaccia utente per Access.Fixed tables data loading for UI tabs for Access.
* Corretto bug nelle impostazioni globali.

## <a name="march-2016"></a>marzo 2016

La versione di anteprima di marzo 2016 di SSMA per l'accesso aggiunge il supporto per la migrazione a SQL Server 2016.The March 2016 preview release of SSMA for Access adds support for migration to SQL Server 2016.

## <a name="january-2016"></a>Gennaio 2016

La versione di manutenzione di gennaio 2016 di SSMA per l'accesso contiene le seguenti modifiche:

* Correzione della funzione non valida per l'impostazione predefinita di un campo GUID (RFC 3894811).
* Correzione del blocco durante l'importazione di record nel database SQL (Azure) (RFC 4919573).
* Aggiunta voce di menu Visualizza registro a SSMA (RFC 5706203).
* Aggiunto Telemetria.

## <a name="july-2014"></a>Luglio 2014

La versione di luglio 2014 di SSMA per l'accesso contiene le seguenti modifiche:

* Conversione del codice del database SQL di Azure migliorata.
* È stata spostata la funzionalità del pacchetto di estensione allo schema per supportare il database SQL di Azure.Moved extension pack functionality to schema to support Azure SQL DB.
* Miglioramenti delle prestazioni testati per i database con oltre 10k oggetti.
* Aggiunti miglioramenti dell'interfaccia utente per la gestione di un numero elevato di oggetti.
* Aggiunto il supporto per l'evidenziazione degli schemi LOB "noti" (in modo che possano essere ignorati nella conversione).
* Aggiunti miglioramenti alla velocità di conversione.
* Aggiunto il supporto per la visualizzazione dei conteggi degli oggetti nell'interfaccia utente.
* Dimensioni del report ridotte di oltre il 25%.
* Messaggi di errore migliorati per i costrutti non analizzati.

## <a name="april-2014"></a>Aprile 2014

La versione di aprile 2014 di SSMA per l'accesso contiene le seguenti modifiche:

* Aggiunto il supporto per MS SQL Server 2014.
* Corretti i bug relativi alla conversione in Azure.Fixed bugs related to conversion to Azure.
* Corretti i bug relativi alle pagine di report invisibili in IE 10.

## <a name="january-2012"></a>gennaio 2012

La versione di gennaio 2012 di SSMA per l'accesso contiene le seguenti modifiche:

* Hai fornito l'opzione per non rendere persistenti nome utente e password per le tabelle collegate di MS Access dopo la migrazione.
* Impostare le azioni a catena per i riferimenti circolari su Nessuna azione.
* Sono stati forniti messaggi appropriati che indicano azioni a catena per i riferimenti circolari impostati su Nessuna azione.

## <a name="july-2011"></a>luglio 2011

La versione di luglio 2011 di SSMA per Access aggiunge una migliore segnalazione degli errori durante la migrazione dei dati.

## <a name="april-2011"></a>Aprile 2011

La versione di aprile 2011 di SSMA per l'accesso contiene le seguenti modifiche:

* È stato aggiunto un singolo oggetto installabile di [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]"SSMA for Access", che supporta , [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]e [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] SQL di Azure.
* Aggiunta la possibilità [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]di connettersi a .
* Aggiunto SSMA per il supporto della versione di Access Console per la compatibilità con le versioni precedenti. È possibile aprire i progetti creati da versioni precedenti a SSMA v5.0.You can open the projects created by versions earlier to SSMA v5.0.
* Aggiunta la possibilità di installare SSMA v5.0 prodotto side-by-side (SxS) con le versioni precedenti del prodotto SSMA.

## <a name="july-2010"></a>Luglio 2010

La versione di luglio 2010 di SSMA per l'accesso contiene le seguenti modifiche:

* Aggiunto il supporto per la migrazione a SQL Server 2008 R2 e SQL di Azure.Added support for migrating to SQL Server 2008 R2 and Azure SQL.
* Aggiunta di una connessione sicura a SQL Server e SQL di Azure.Added a secure connection to both SQL Server and Azure SQL.
* Aggiunto il supporto per i database di Access 2010.
* Aggiunta una nuova applicazione Console SSMA per l'esecuzione della riga di comando.
* Aggiunto il supporto `DateTime2` per il tipo di dati di SQL Server.Added support for the SQL Server data type.

## <a name="june-2008"></a>Giugno 2008

La versione di giugno 2008 di SSMA for Access aggiunge il supporto per i database di Access 2007.

## <a name="may-2007"></a>Maggio 2007

La versione di maggio 2007 di SSMA per l'accesso contiene le seguenti modifiche:

* Aggiunto il supporto per i database di Access che utilizzano criteri del gruppo di lavoro.
* Offerta la possibilità di eliminare gli oggetti convertiti da Esplora metadati di SQL ServerSQL Server .
* Aggiunto il supporto per i commenti immessi dall'utente in modalità SQL in formato SQL ServerSQL Server.
* Aggiunti miglioramenti nella conversione degli oggetti.

## <a name="november-2006"></a>Novembre 2006

La versione di novembre 2006 di SSMA per l'accesso contiene le seguenti modifiche:

* Aggiunta una nuova Migrazione guidata database che guida l'utente [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]attraverso la migrazione di un singolo database da Access a .
* È stato aggiunto un nuovo comando Converti, Carica e Migra che converte i database di Access, carica gli oggetti convertiti in [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]e migra tutti in [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] un unico passaggio.
* Migrazione delle query migliorata. La migrazione delle query consente ora di convertire più query SELECT in viste. Per ulteriori informazioni, vedere [Conversione di oggetti di database di Access](converting-access-database-objects-accesstosql.md).
* Aggiunta la possibilità di modificare le [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] proprietà di tabelle e indici nella scheda **Tabella.**
* Aggiunte nuove impostazioni globali:
  * È possibile scegliere di visualizzare i numeri di riga nelle finestre dell'editor.
  * È possibile configurare SSMA per richiedere di sostituire gli oggetti duplicati o sempre o mai sostituire gli oggetti duplicati durante la conversione dello schema.
* Aggiunta una nuova opzione di conversione che consente di specificare se SSMA visualizza un avviso quando una query complessa contiene un carattere jolly.

## <a name="july-2006"></a>Luglio 2006

La versione di luglio 2006 di SSMA for Access è stata la versione iniziale.
