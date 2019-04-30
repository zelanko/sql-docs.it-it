---
title: Note sulla versione
titleSuffix: Azure Data Studio
description: Note sulla versione di Azure Data Studio
ms.custom: seodec18
ms.date: 04/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f142602efa4e2c0d7c12b4f5f7634f2a9b668cb3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63143710"
---
# <a name="release-notes-for-azure-data-studio"></a>Note sulla versione per Azure Data Studio

**[Scaricare e installare la versione più recente.](download.md)**

## <a name="april-2019"></a>Aprile 2019

18 aprile 2019 &nbsp;  /  &nbsp; versione: 1.6.0 

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Rinominati **i server** premere TAB per passare **connessioni** | |
| Spostare Esplora risorse di Azure come un Azure viewlet in connessioni | Gli utenti possono ora visualizzare le istanze di SQL di Azure tramite Azure viewlet nella visualizzazione di connessioni e si espandono per visualizzare gli oggetti in ogni server o database.|
| Miglioramenti di Notebook SQL | &bull; &nbsp; Aggiunto il pulsante sulla barra degli strumenti per cancellare l'output per tutte le celle <br/>&bull; &nbsp; Aggiunto il pulsante sulla barra degli strumenti per eseguire tutte le celle <br/>&bull; &nbsp; Nome di connessione fisso anziché il nome server (se impostata) nella finestra Connetti a elenco a discesa <br/>&bull; &nbsp; Correzione per le immagini in markdown non per il rendering quando si usano i percorsi delle immagini relativo <br/>&bull; &nbsp; Funzionalità migliorate nelle griglie notebook aggiungendo fare doppio clic sulla dimensione della colonna-ridimensionamento automatico e un migliore supporto rotellina del mouse <br/>&bull; &nbsp; Miglioramenti alla gestione degli errori e python installare resilienza durante l'installazione di python tramite i notebook <br/>&bull; &nbsp; Miglioramenti alla funzionalità "Seleziona tutto" quando si selezionano celle del blocco appunti <br/>&bull; &nbsp; Miglioramenti alle connessioni di notebook per impedire la chiusura di un notebook e conseguenze per una connessione di Esplora oggetti <br/>&bull; &nbsp; Esperienza notebook migliorata per visualizzare un messaggio all'utente quando notebook disconnesso e richiede una connessione per l'esecuzione di celle<br/>&bull; &nbsp; Supporto migliorato per i notebook non salvati reidratare in annunci quando viene avviato nuovamente gli annunci |
| Bug risolti e problemi. | Visualizzare [bug e problemi, in GitHub](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1). |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>Marzo 2019 (Hotfix)

22 marzo 2019 &nbsp;  /  &nbsp; versione: 1.5.2 &nbsp;  /  &nbsp; versione dell'Hotfix

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Risolti alcuni problemi riscontrati in 1.5.1. | Visualizzare [marzo versione dell'Hotfix, su GitHub](https://github.com/Microsoft/azuredatastudio/milestone/28).<br/> <br/>&bull; &nbsp; Risolto un problema in cui utente Impossibile chiudere il notebook aperto dall'attività "Apri blocco appunti" nel Dashboard <br/>&bull; &nbsp; Problema risolto dove Notebook JSON ha molto} dopo il salvataggio <br/>&bull; &nbsp; Risolto un problema in cui le griglie notebook non sono stati risponde alle modifiche al tema <br/>&bull; &nbsp; Risolto un problema in cui è stato illustrato percorso del notebook completa nell'intestazione della scheda. A questo punto viene visualizzato solo il nome del file. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>Marzo 2019

18 marzo 2019 &nbsp;  /  &nbsp; versione: 1.5.1

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Aggiunto [estensioni di PostgreSQL per Data Studio di Azure](postgres-extension.md) | Funzionalità supportate: <br/>&bull; &nbsp; Finestra di dialogo connessione <br/>&bull; &nbsp; Esplora oggetti <br/>&bull; &nbsp; Editor di query <br/>&bull; &nbsp; Creazione di grafici <br/>&bull; &nbsp; Dashboard <br/>&bull; &nbsp; Frammenti di codice <br/>&bull; &nbsp; Modificare i dati <br/>&bull; &nbsp; Notebook |
| Notebook SQL aggiunto | Aggiunta del supporto SQL Kernel al Visualizzatore di Notebook predefinito: <br/>&bull; &nbsp; Supporta T-SQL <br/>&bull; &nbsp; Supporto PGSQL |
| Estensione PowerShell aggiunta  | Porta il [estensione PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) esperienza da Visual Studio Code.  |
| Estensione di file dacpac di SQL Server aggiunta  | Rimuove la creazione guidata applicazione livello dati dall'estensione di SQL Server Import in una nuova estensione.  |
| Estensione della Community aggiunta QueryPlan.show | Aggiunge il supporto di integrazione per visualizzare i piani di query  |
| Estensione di anteprima di SQL Server 2019 aggiornato | &bull; &nbsp; Supporto per Notebook di Jupyter, in particolare le kernel Spark e Python3, sono stati spostati nello strumento Azure Data Studio core. <br/>&bull; &nbsp; Correzioni di bug per creazione guidata dati esterni  |
| Bug risolti e problemi. | Visualizzare [bug e problemi, in GitHub](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemi noti
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): Facendo clic su Esegui nella cella prima del Kernel è pronto per i risultati di Spark in errore irreversibile **soluzione alternativa:** Attendere finché l'esecuzione di tutte le celle vengono caricati i kernel
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): ANNUNCI avviati da SSMS con autenticazione SQL - richieste di immissione di password **soluzione alternativa:** Usare l'autenticazione di Windows per il momento. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): Non è possibile installare la funzionalità di notebook SQL <br/>
**Soluzione alternativa:** Attenersi alle procedure alternative [qui](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832). 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): Azure Data Studio non può essere aperto direttamente dalla cartella di download (Mac) <br />
**Soluzione alternativa:** Riavviare i computer dopo la decompressione dell'app. Verranno esaminati. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  Salva con nome notebook perde il contesto di connessione <br />
**Soluzione alternativa:** Verrà risolto nella prossima versione. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): Estrarre dacpac arresti anomali SqlToolsService se viene utilizzata la versione non valida <br/>
**Soluzione alternativa:** Riavviare Data Studio di Azure e garantire che venga usata la versione corretta.
- Nuove icone di Notebook e aprire Notebook vengono perse <br/> 
**Soluzione alternativa:** Il tipo di connessione legacy è deprecato. È consigliabile connettersi all'endpoint di SQL Server e si riceverà tutte le azioni (nuovo Notebook, processo Spark) come previsto. 

## <a name="february-2019"></a>Febbraio 2019

13 febbraio 2019 &nbsp;  /  &nbsp; versione: 1.4.5

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Aggiunti **Admin pack per SQL Server** pacchetto di estensioni. | Questo rende più semplice installare le estensioni correlate all'amministrazione di SQL Server. ad esempio:<br/>&bull; &nbsp; [SQL Server Agent](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Import](sql-server-import-extension.md?view=sql-server-2017) |
| Il filtro aggiunto esteso supporto per gli eventi nell'estensione di Profiler. | &nbsp; |
| Sono state aggiunte salvare come funzionalità XML in grado di salvare i risultati di T-SQL in formato XML. | &nbsp; |
| Aggiunti miglioramenti di creazione guidata applicazione livello dati. | &bull; &nbsp; Pulsante Genera script<br/>&bull; &nbsp; Visualizzazione aggiunta per fornire gli avvisi della possibile perdita di dati durante la distribuzione. |
| Aggiornamenti all'estensione di anteprima di SQL Server 2019. | Visualizzare [estensione di anteprima di SQL Server 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Risultati di streaming abilitati per impostazione predefinita per molto tempo esecuzione di query. | &nbsp; |
| Bug risolti e problemi. | Visualizzare [bug e problemi, in GitHub](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1). |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>Gennaio 2019 (Hotfix)

16 gennaio 2019 &nbsp;  /  &nbsp; versione: 1.3.9 &nbsp;  /  &nbsp; versione dell'Hotfix

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Risolti alcuni problemi riscontrati in 1.3.8. | Visualizzare [versione dell'Hotfix di gennaio, su GitHub](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).<br/><br/>Per informazioni dettagliate, vedere:<br/>&bull; &nbsp; [Modifica Log, in GitHub](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).<br/>&bull; &nbsp; [Le versioni, su GitHub](https://github.com/Microsoft/azuredatastudio/releases). |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>Gennaio 2019

09 gennaio 2019 &nbsp;  /  &nbsp; versione: 1.3.8

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Aggiungere un nuovo programma di installazione di utente per Windows. | A differenza di installazione del sistema esistente, il nuovo programma di installazione di utente non richiede privilegi di amministratore. In questo modo un'esperienza di aggiornamento più semplice per utenti non amministratori. |
| Aggiunta del supporto autenticazione Azure Active Directory. | &nbsp; |
| Announcing SQL Idera DM prestazioni Insights (anteprima). | &nbsp; |
| Supporto per la creazione guidata applicazione livello dati nell'estensione di SQL Server Import. | &nbsp; |
| Aggiornare l'estensione di anteprima di SQL Server 2019. | Visualizzare [estensione di anteprima di SQL Server 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Miglioramenti di SQL Server Profiler. | &nbsp; |
| Risultati della query di grandi dimensioni (anteprima) di Streaming. | &nbsp; |
| Le estensioni della community: sp_executesql, sql e al nuovo Database. | &nbsp; |
| Bug risolti e problemi. | Visualizzare [bug e problemi, in GitHub](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1). |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>Novembre 2018

6 novembre 2018 &nbsp;  /  &nbsp; versione: 1.2.4

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Aggiornare l'estensione di anteprima di SQL Server 2019. | Visualizzare [estensione di anteprima di SQL Server 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Introduzione a incollare l'estensione del piano. | &nbsp; |
| Introduzione a estensione query High Color, incluso il tema dell'editor SSMS. | &nbsp; |
| Consente di correggere le estensioni di importazione, Profiler e SQL Server Agent. | &nbsp; |
| Correggere.NET Core che causa problema Socket KeepAlive eliminate le connessioni inattive in macOS. | &nbsp; |
| Aggiornamento servizio di strumenti di SQL per.NET Core versione 2.2 Preview 3 (per un eventuale supporto AAD). | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Correzioni di bug, novembre 2018

- Correggere [problema #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Connessione perdita a database SQL di Azure
- Correggere [problema #2914](https://github.com/Microsoft/azuredatastudio/issues/2914): "Argomento non valido" eccezione espansione OE nodo del database
- Correggere [problema #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Visualizzare i messaggi a più righe in modo corretto nei risultati della query
- Correggere [problema #2906](https://github.com/Microsoft/azuredatastudio/pull/2906): Correzione nome documento la modifica dei dati quando il nome di tabella contiene caratteri speciali
- Correggere [problema #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): Compilato nell'estensione changelog afferma controllare le note sulla versione di Visual Studio code per le modifiche
- Correggere [problema #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): Tema a contrasto elevato. valori Double/Triple icone
- Correggere [problema #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Aggiungere un'interfaccia della riga di comando per la connessione a SQL Server
- Correggere [problema #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Aggiungere il supporto di tema piano di query

## <a name="october-2018"></a>Ottobre 2018

29 ottobre 2018 &nbsp;  /  &nbsp; versione: 1.1.4

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Introduzione a Esplora risorse di Azure per esplorare database SQL di Azure. | &nbsp; |
| Migliorare l'affidabilità di connettività di Esplora oggetti ed Editor di Query. | &nbsp; |
| Miglioramenti di estensioni SQL Agent. | &nbsp; |
| Aggiornare l'estensione di anteprima di SQL Server 2019. | Visualizzare [estensione di anteprima di SQL Server 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Correzioni di bug, ottobre 2018

- Correggere [problema #2717](https://github.com/Microsoft/azuredatastudio/issues/2717): Il risultato di colonne XML su formattazione
- Correggere [problema #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Finestre dei risultati della larghezza è incompleta
- Correggere [problema #2999](https://github.com/Microsoft/azuredatastudio/issues/2999): Impossibile caricare il file Tracing in computer Mac quando ci si connette al database
- Correggere [problema #2851](https://github.com/Microsoft/azuredatastudio/issues/2851): Grafico delle serie temporali non esegue il rendering correttamente
- Correggere [problema #2996](https://github.com/Microsoft/azuredatastudio/issues/2996): Perdita di tabella temporanea a causa di modifiche improvvise sessione

Per informazioni dettagliate, vedere la [Log delle modifiche](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versioni](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-ga-release"></a>Settembre 2018 (versione di disponibilità generale)

Il 24 settembre 2018 &nbsp;  /  &nbsp; versione: 1.0 &nbsp;  /  &nbsp; versione GA

Versione di disponibilità generale di Studio dei dati di Azure (precedentemente SQL Operations Studio).

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Miglioramenti dell'esperienza utente per un numero elevato di set di risultati e le prestazioni di griglia di risultati di query. | &nbsp; |
| Codice sorgente di Visual Studio Code Aggiorna da 1,23 per 1.26.1 con griglia di Layout e migliorato impostazioni Editor (anteprima). | &nbsp; |
| Miglioramenti all'accessibilità per la lettura dello schermo, la navigazione da tastiera e a contrasto elevato. | &nbsp; |
| Aggiunto `Connection name` opzione per specificare un nome alternativo visualizzato nel consentono di visualizzare i server. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>Annuncio dell'estensione di anteprima di SQL Server 2019

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Supporto per le funzionalità di anteprima di SQL Server 2019 compresi [cluster di big data](../big-data-cluster/big-data-cluster-overview.md) supportano. | Connettersi al Gateway HDFS/Spark forniti con l'anteprima di SQL Server 2019.<br/><br/>Sfoglia HDFS, caricare i file, salvare i file e avviare azioni utili, ad esempio analizza in blocco note per i file CSV.<br/><br/>Inviare processi Spark nel dashboard o fare clic su una connessione di Spark o HDFS in Esplora oggetti. |
| Notebook di Studio dei dati di Azure. | Creare o aprire notebook utilizzando un Visualizzatore integrato Notebook. In questa versione il Notebook viewer supporta la connessione a kernel locale e solo il cluster di big data di SQL Server 2019.<br/><br/>Per informazioni su tipi di dati e formato di file per la preparazione dei dati veloce, usare le librerie di tasti di scelta rapida codice PROSE nel Notebook. |
| Esplora risorse di Azure. | La visualizzazione di Esplora risorse di Azure consente di esplorare gli endpoint relativi ai dati per gli account Azure e creare connessioni a essi in Esplora oggetti. In questa versione sono supportati server e database SQL di Azure. |
| PolyBase di SQL Server Creazione guidata tabella esterna. | Creare una tabella esterna e le relative strutture di metadati di supporto con una procedura guidata di facile utilizzo. In questa versione, i server remoti di SQL Server e Oracle sono supportati. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Correzioni di bug, settembre 2018

- Correggere [problema #2647](https://github.com/Microsoft/azuredatastudio/issues/143): I grafici ha richiesto un grosso passo con le versioni precedenti.
- Correggere [problema #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT che restituisce l'intera colonna collegamenti ipertestuali JSON.

Per informazioni dettagliate, vedere la [Log delle modifiche](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versioni](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="august-2018"></a>Agosto 2018

30 agosto 2018 &nbsp;  /  &nbsp; versione: 0.32.8 &nbsp;  /  &nbsp; anteprima pubblica

Il *versione di anteprima pubblica di agosto* è incentrato sulle correzioni di bug, stabilizzazione del prodotto e colmando i vuoti nella scenari esistenti.

_0.32.8 contiene correzioni per un paio delle regressioni trovate in 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Annuncio dell'estensione di importazione SQL Server. | &nbsp; |
| Gestione delle sessioni di SQL Server Profiler. | &nbsp; |
| Supporto del modello della sessione SQL Server Profiler. | &nbsp; |
| Miglioramenti di SQL Server Agent. | &nbsp; |
| Nuova estensione della community: Primo kit risponditore. | &nbsp; |
| Miglioramenti alla qualità della vita: Stringhe di connessione | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Correzioni di bug, agosto 2018

- Analizzare in una finestra dell'Editor di Query SQL usando il `Parse Syntax` comando.
- Correggere [problema #143](https://github.com/Microsoft/azuredatastudio/issues/143): Fare doppio clic se non si seleziona nel nome della variabile.
- Correggere [problema #387](https://github.com/Microsoft/azuredatastudio/issues/387): SQL DB icona corrispondente è rosso.
- Correggere [problema #825](https://github.com/Microsoft/azuredatastudio/issues/825): Richiesta: Connetti automaticamente al server corrente dopo lo Script come... 
- Correggere [problema #1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [voce Desktop] - valore ridondanti per nome & commento.
- Correggere [problema #1285](https://github.com/Microsoft/azuredatastudio/issues/1285): Le cause dell'applicazione sull'icona di aggiornamento per essere rimosso o sostituito in Windows.
- Correggere [problema #1317](https://github.com/Microsoft/azuredatastudio/issues/1317): Correggere il separatore decimale.
- Correggere [problema #1474](https://github.com/Microsoft/azuredatastudio/issues/1474): Annulla Modifica connessione disconnette la connessione corrente.
- Correggere [problema #1497](https://github.com/Microsoft/azuredatastudio/issues/1497): Visualizzare come le opzioni sono tagliate nella parte inferiore del grafico.
- Correggere [problema #1524](https://github.com/Microsoft/azuredatastudio/issues/1524): Shell/Dashboard: Le icone viewlet principale sono trascinabile e causare un arresto anomalo dell'app.
- Correggere [problema #1578](https://github.com/Microsoft/azuredatastudio/issues/1578): Non è possibile espandere/comprimere cartella browser file remoto facendo clic sul nome.
- Correggere [problema #1620](https://github.com/Microsoft/azuredatastudio/issues/1620): Suggerimento di funzionalità: Ottenere la stringa di connessione per la connessione esistente.
- Correggere [problema #1624](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox non cambia colore quando disabilitata.
- Correggere [problema #1728](https://github.com/Microsoft/azuredatastudio/issues/1728): Salva come JSON/EXCEL/CSV non funzionano.
- Correggere [problema #1744](https://github.com/Microsoft/azuredatastudio/issues/1744): Riquadro risultati perde le posizioni di scorrimento quando si passa tra le schede.
- Correggere [problema #1748](https://github.com/Microsoft/azuredatastudio/issues/1748): Messaggio di errore durante il salvataggio ora file seconde (e successive) di Excel.
- Correggere [problema #1782](https://github.com/Microsoft/azuredatastudio/issues/1782): Modificare i dati: cella non viene ripristinato al valore originale sul premendo ESC.
- Correggere [problema #1836](https://github.com/Microsoft/azuredatastudio/issues/1836): file con estensione SQL non associati di SQL Operations Studio.
- Correggere [problema #1850](https://github.com/Microsoft/azuredatastudio/issues/1850): N digitando ' durante la digitazione a N ' '.
- Correggere [problema #1985](https://github.com/Microsoft/azuredatastudio/issues/1985): Copia dalla griglia di risultati di query è disattivata per 1 colonna.
- Correggere [problema #1998](htpts://github.com/Microsoft/azuredatastudio/pull/1998): Aggiungere la versione di Visual Studio Code sulla finestra di dialogo.
- Correggere [problema #2042](https://github.com/Microsoft/azuredatastudio/pull/2042): Agent: Abilitato per importare le query dal file sql.
- Correggere [problema #2091](https://github.com/Microsoft/azuredatastudio/issues/2091): Non è possibile usare una scelta rapida Ctrl + C per copiare dal riquadro dei risultati.
- Correggere [problema #2099](https://github.com/Microsoft/azuredatastudio/pull/2099): Aggiunta di altre opzioni di saveAsCsv.
- Correggere [problema #2107](https://github.com/Microsoft/azuredatastudio/issues/2107): Aggiornare l'icona del documento per i documenti di Dashboard e Profiler.
- Correggere [problema #2129](https://github.com/Microsoft/azuredatastudio/pull/2129): Salva posizione di scorrimento di modifica dei dati quando si cambia scheda.
- Correggere [problema #2152](https://github.com/Microsoft/azuredatastudio/issues/2152): Indicatore di riga della griglia dei risultati in base Zero.

### <a name="known-issues-august-2018"></a>Problemi noti, agosto 2018

- [Problema #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Salva con nome solo Salva prima riga di dati di Excel
- [Problema #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Non è possibile connettersi in Ubuntu 16.04 per SQL in un contenitore

## <a name="july-2018"></a>Luglio 2018

19 luglio 2018 &nbsp;  /  &nbsp; versione: 0.31.4 &nbsp;  /  &nbsp; anteprima pubblica

Il *versione di anteprima pubblica di luglio* è incentrato sugli elementi seguenti:

- La versione iniziale degli scenari di configurazione SQL Server Agent.
- SQL Server Profiler della sessione e visualizzazione modello miglioramenti.
- Costante correzioni di bug per il cliente ha segnalato problemi di GitHub.

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| [SQL Server Agent per l'estensione di SQL Operations Studio](sql-server-agent-extension.md) miglioramenti. | Aggiunta visualizzazione di avvisi, operatori e proxy e le icone nel riquadro sinistro.<br/><br/>Finestre di dialogo aggiunta per nuovo processo nuovo passaggio di processo, nuovo avviso e il nuovo operatore.<br/><br/>Aggiunta Elimina processo, eliminare avvisi e Delete-operatore (pulsante destro del mouse).<br/><br/>Aggiunta la visualizzazione esecuzioni precedenti.<br/><br/>Aggiunti i filtri per ogni nome di colonna. |
| [SQL Server Profiler per l'estensione di SQL Operations Studio](sql-server-profiler-extension.md) miglioramenti. | Aggiungere 5 modelli predefiniti per visualizzare gli eventi estesi.<br/><br/>Nome della connessione Server/Database aggiunto.<br/><br/>Aggiunta del supporto per le istanze del Database SQL di Azure.<br/><br/>Suggerimento aggiunto Profiler viene chiuso quando scheda è chiusa quando il Profiler è ancora in esecuzione. |
| Versione dell'estensione di script di combinazione. | &nbsp; |
| Punti di procedura guidata e l'estensibilità di finestra di dialogo aggiunti per gli autori delle estensioni. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Correzioni di bug, luglio 2018

- Correggere [emettere 728](https://github.com/Microsoft/azuredatastudio/issues/728): Nessuna risposta al Aggiungi connessione in macOS
- Correggere [emettere 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): Visualizzazione di testo della griglia di risultati è un disastro per caratteri internazionali
- Correggere [emettere 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): Finestra di dialogo backup: Browser file dell'interfaccia utente viene interrotto
- Correggere [emettere 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): Numero di righe interessate
- Correggere [emettere 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): Non è possibile connettersi a qualsiasi origine dati
- Correggere [emettere 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError quando ci si connette al Server
- Correggere [emettere 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): Le finestre di dialogo di estensione hanno smesso di funzionare
- Correggere [emettere 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): BUG: Interpretazione dei dati HTML in una colonna
- Correggere [emettere 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): Estendibilità: se si aggiunge un provider di connessione disinstallazione non verrà mai rimosso dall'elenco
- Correggere [emettere 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Estensioni Sqlops: queryeditor.connect() si connette al database di destinazione, ma dell'interfaccia utente non viene visualizzato che l'editor è connesso
- Correggere [emettere 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): Grafico le dimensioni di 10 DB superiore non funziona nelle istanze di maiuscole / minuscole
- Correggere [emettere 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): definizione del tipo di errore di digitazione sqlops.d.ts causa implicita 'any'
- Correggere [emettere 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Errore de Ortografia
- Correggere [emettere 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): L'impostazione iconPath in ButtonComponent dopo la chiamata di component() non modifica icona
- Correggere [emettere 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): Una migliore organizzazione di tabelle

## <a name="june-2018"></a>Giugno 2018

20 giugno 2018 &nbsp;  /  &nbsp; versione: 0.30.6 &nbsp;  /  &nbsp; anteprima pubblica

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| **SQL Server Profiler per SQL Operations Studio _Preview_**  versione iniziale di estensione. | &nbsp; |
| Il nuovo **SQL Data Warehouse** estensione include i widget di dashboard personalizzabili avanzato esporre informazioni dettagliate nel tuo data warehouse. | Ciò consente di sbloccare gli scenari principali per la gestione e ottimizzazione del data warehouse per assicurarti che è ottimizzato per prestazioni coerenti. |
| **Modificare "applicazione di filtri e l'ordinamento dei dati"** supportano. | &nbsp; |
| **SQL Server Agent per SQL Operations Studio _Preview_**  miglioramenti dell'estensione per i processi e la cronologia processo viste. | &nbsp; |
| Migliorato **guidata & finestra di dialogo dell'interfaccia utente generatore Framework** API di estendibilità. | &nbsp; |
| Aggiornare il codice sorgente di Visual Studio Code piattaforma. | Integrato le versioni seguenti:<br/>&bull; &nbsp; [Marzo 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [Aprile 2018 (1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>Consente di risolvere i problemi di GitHub, giugno 2018

- Richiesta di funzionalità ([emettere 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Verificare i risultati della larghezza della colonna di adattamento della griglia per i dati e ricordare le modifiche manuali se si esegue nuovamente la stessa query.
- Correggere [emettere 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Show devono aggiungere messaggi e pulsante Aggiungi account account quando l'account collegato è vuota.
- Correggere [emettere 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): Scheda account collegato viene interrotta quando la visualizzazione è compressa.
- Correggere [emettere 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): Arresti anomali del servizio di strumenti di SQL all'apertura di file con estensione SQL dal disco.
- Correggere [emettere 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Parola chiave SQL "BETWEEN" mancante.
- Correggere [emettere 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Parola chiave 'MATCH' arresti anomali del servizio di strumenti SQL.
- Correggere [emettere 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): "Nuovo Profiler" opzione del menu di scelta rapida in Esplora oggetti non esegue alcuna operazione.
- Correggere [emettere 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): Piano di query "Spiegazione" editor di query viene interrotta.

## <a name="may-2018"></a>Mese di maggio 2018

7 marzo 2018 &nbsp;  /  &nbsp; versione: 0.29.3 &nbsp;  /  &nbsp; anteprima pubblica

Il *potrebbe Public Preview* è incentrato su stabilizzazione e correzioni di bug.

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Annuncio relativo all'estensione di Redgate SQL Search disponibile in Gestione estensioni. | &nbsp; |
| Localizzazione della community disponibile per 10 lingue. | Tedesco, spagnolo, francese, italiano, giapponese, coreano, portoghese, russo, cinese semplificato e cinese tradizionale. |
| Modifiche alla raccolta di dati di telemetria. | &bull; &nbsp; Raccolta di dati di telemetria ridotto.<br/>&bull; &nbsp; Migliore esperienza di rifiuto.<br/>&bull; &nbsp; Collegamenti del prodotto all'informativa sulla Privacy. |
| Gestione estensioni ha Marketplace migliorata esperienza. | Consente di individuare più facilmente le estensioni della community. |
| Estensione di SQL Agent. | &bull; &nbsp; Processi.<br/>&bull; &nbsp; Miglioramento apportato alla visualizzazione cronologia processo. |
| Aggiornamenti per whoisactive ed estensioni di rapporti del Server. | &nbsp; |
| Migliorate di gestione Dashboard di proprietà di scorrimento. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>Risolvere i problemi di GitHub

- Correggere [emettere 703](https://github.com/Microsoft/azuredatastudio/issues/703): Immissione di testo simile a HTML nei dati di modifica provoca valore da visualizzare in modo non corretto finché l'aggiornamento
- Correggere [emettere 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb dipendenza del pacchetto
- Correggere [emettere 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Parola chiave 'distinct' non è evidenziata
- Correggere [emettere 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Modificare i dati di ripristino non funziona riga
- Correggere [emettere 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Estensione di SQL Agent e la barra di stato
- Correggere [emettere 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Ridimensionamento di SQL Agent non dopo la modifica delle dimensioni di windows

## <a name="april-2018"></a>Aprile 2018

25 aprile 2018 &nbsp;  /  &nbsp; versione: 0.28.6 &nbsp;  /  &nbsp; anteprima pubblica

Il *versione di anteprima pubblica di aprile* include miglioramenti e correzioni di bug.

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Miglioramenti per l'estensione di SQL Agent Preview: | &nbsp; |
| &nbsp; &nbsp; &nbsp; Supporto migliorato per i file. | &bull; &nbsp; File di grandi dimensioni.<br/>&bull; &nbsp; File protetti, per il salvataggio di amministratore protetto.<br/>&bull; &nbsp; L'archiviazione \>256M file all'interno di SQL Operations Studio. |
| &nbsp; &nbsp; &nbsp; Terminale integrato di divisione. | Lavorare contemporaneamente con più terminali open. |
| &nbsp; &nbsp; &nbsp; Installa più veloce e tempi di avvio. | Installazione ridotta di stampa di file su disco numero piedi. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>Risolvere i problemi di GitHub, aprile 2018

- Correggere [emettere 37](https://github.com/Microsoft/azuredatastudio/issues/37): Quando il Visualizzatore grafico genera un errore, si verifica un comportamento imprevisto.
- Correggere [emettere 462](https://github.com/Microsoft/azuredatastudio/issues/462): Richiesta di funzionalità: Opzione per i gruppi di Server per essere espanso per impostazione predefinita.
- Correggere [emettere 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense - suggerimento non valido per 'update' comando.
- Correggere [emettere 967](https://github.com/Microsoft/azuredatastudio/issues/967): Piano di query previsti quando seleziona showplan XML nella griglia di risultati.
- Correggere [emettere 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): Aggiungere le parentesi quadre per ms_foreachdb chiamata da flyfishingdba.
- Correggere [emettere 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): Errore durante l'handshake SSL/TLS pre-login.
- Correggere [emettere 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): Visualizzazione di insights Cancella prima di visualizzare l'errore.
- Correggere [emettere 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): Nuove azioni di query in Esplora-widget e ripristino vengono interrotte.
- Correggere [emettere 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): Dashboard Output windows pop-up con il messaggio di errore per il Database SQL di Azure.
- Correggere [emettere 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): Finestra di dialogo connessione Mostra errore è necessario un Server alla visualizzazione iniziale.
- Correggere [emettere 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): Gruppi di server è ora necessario un doppio clic per espandere.
- Correggere [emettere 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): Sfondo del controllo di selezione è semi-trasparente.
- Correggere [emettere 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Risolvere i problemi di accessibilità di tutti a contrasto elevato in SQL Operations Studio.
- Correggere [emettere 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): Estensione non riesce a eseguire il collegamento di aggiornamento "scaricare manualmente" passa a una posizione non valida.
- Correggere [emettere 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): V scorrimento non funziona nella scheda Home.
- Correggere [emettere 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): Schede dell'estensione SQL ha smesso di funzionare.

### <a name="visual-studio-code-121-platform"></a>Visual Studio Code 1.21 piattaforma

Un'evidenziazione per l'anteprima pubblica di aprile è l'aggiornamento del codice sorgente per la piattaforma pari a 1,21 codice di Visual Studio. Verrà visualizzata diversi aggiornamenti per l'editor principale e workbench dal punto di 1.19 sincronizzazione precedente. Alcuni esempi includono quanto segue:

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| [Nuove notifiche dell'interfaccia utente](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui). | Gestire e controllare le notifiche di SQL Operations Studio con facilità. |
| [Integrato suddivisione Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals). | Lavorare con più terminali Apri contemporaneamente. |
| [Salvare i file di grandi dimensioni e protetti](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges). | Salvare amministratore protetto e \>256M file all'interno di SQL Operations Studio. |
| [Migliorato il supporto di file di grandi dimensioni](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements). | Ottimizzazioni del buffer di testo per i file di grandi dimensioni. |
| [Funzionalità di ricerca migliorata impostazioni](https://code.visualstudio.com/updates/v1_20#_settings-search). | Trovare facilmente la corretta impostazione con la ricerca del linguaggio naturale. |
| [Frammenti di codice globale](https://code.visualstudio.com/updates/v1_20#_global-snippets). | Creare frammenti di codice che è possibile usare in tutti i tipi di file. |
| [Selezione multipla Esplora](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer). | Eseguire azioni su più file contemporaneamente. |
| [Errori e avvisi in Esplora](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer). | Spostarsi rapidamente tra gli errori nella base di codice. |
| [Trascinare e rilasciare, copiare e incollare dati tra windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support). | Spostare i file tra finestre aperte di SQL Operations Studio. |
| [Supporto di modulo secondario GIT](https://code.visualstudio.com/updates/v1_20#_git-submodules). | Eseguire operazioni di Git per i repository Git annidati. |
| [Supporto di lettura dello schermo terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support). | Dispone ora di terminale integrato **ottimizzato per la lettura dello schermo** modalità. |
| [Layout centrato editor](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout). | Ottimizzare il codice visualizza sullo schermo. |
| [I risultati della ricerca orizzontale (anteprima)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | È possibile ora risultati della ricerca di visualizzazione in un pannello orizzontale. |
| &nbsp; | &nbsp; |

Per altri dettagli, estrarre il [note sulla versione di Visual Studio Code febbraio](https://code.visualstudio.com/updates/v1_21)e il [note sulla versione di Visual Studio Code gennaio](https://code.visualstudio.com/updates/v1_20).

Per ulteriori informazioni, vedere il [log delle modifiche](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018"></a>Marzo 2018

28 marzo 2018 &nbsp;  /  &nbsp; versione: 0.27.3 &nbsp;  /  &nbsp; anteprima pubblica

Il *versione di anteprima pubblica di marzo* continua a risolvere i principali problemi di GitHub ed è incentrato su come migliorare la nostra storia di estendibilità. In particolare, è stato aggiunto il pannello di gestione delle estensioni, è stata migliorata la gestione delle dashboard e sono stati introdotti il supporto a SQL Agent e le estensioni di insight. Questa versione include i miglioramenti seguenti:

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Migliorato il modello di estendibilità delle dashboard tramite l'aggiunta del supporto di schede per gli insight e riquadri di configurazione. | Aggiunto il pannello ESTENSIONI, che consente la semplice acquisizione delle estensioni.<br/><br/>Le estensioni del dashboard per sp\_whoisactive dal [whoisactive.com](http://www.whoisactive.com).<br/><br/>Per informazioni dettagliate, vedere [estendono le funzionalità di SQL Operations Studio](extensions.md). |
| Aggiunte ulteriori [API di estendibilità per le connessioni ed Esplora Oggetti](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API). | &nbsp; |
| Correzioni dei [problemi di GitHub](https://github.com/Microsoft/azuredatastudio/issues) ad alto impatto sui clienti. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>Febbraio 2018

15 febbraio 2018 &nbsp;  /  &nbsp; versione: 0.26.7 &nbsp;  /  &nbsp; anteprima pubblica

Il *anteprima pubblica di febbraio* include alcuni suggerimenti sulle funzionalità e correzioni di bug con priorità alta. Questa versione include i miglioramenti seguenti:

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Introduzione a installazione di aggiornamento automatico, che fornisce una notifica quando una nuova versione è disponibile come download. | &nbsp; |
| La finestra di dialogo di connessione **Database** campo è ora un elenco di riepilogo a discesa popolato in modo dinamico che contiene un elenco di database popolati dal server specificato. | &nbsp; |
| Introdotta l'API di estensibilità di connessione. | &nbsp; |
| Aggiunta l'integrazione dell'editor di codice di Visual Studio 1.19. | &nbsp; |
| Aggiornato il componente JustinPealing/query-plan per ottenere diversi miglioramenti sul visualizzatore dei piani di query. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>Risoluzione dei problemi, febbraio 2018

- Correggere [emettere 6](https://github.com/Microsoft/azuredatastudio/issues/6): Mantieni connessione e il database selezionato quando si apre nuove schede di query.
- Correggere [emettere 22](https://github.com/Microsoft/azuredatastudio/issues/22): 'Nome del server' e ' Database' - possibile questi essere elenchi a discesa anziché le caselle di testo?
- Correggere [emettere 549](https://github.com/Microsoft/azuredatastudio/issues/549): Installazione invisibile all'utente silent/molto comporta apertura dopo l'installazione dell'applicazione.
- Correggere [emettere 481](https://github.com/Microsoft/azuredatastudio/issues/481): Aggiungere l'opzione "Controlla aggiornamenti".
- Correzioni riguardanti l'editor SQL e il completamento automatico:
  - Correggere [emettere 584](https://github.com/Microsoft/azuredatastudio/issues/584): Parola chiave "Completo" non è evidenziato da IntelliSense.
  - Correggere [emettere 345](https://github.com/Microsoft/azuredatastudio/issues/345): Colorare le funzioni SQL all'interno dell'editor.
  - Corretto il [problema 300](https://github.com/Microsoft/azuredatastudio/issues/300): In una stringa [#tempData] il carattere finale"]" verrà visualizzato di colore verde.
  - Correggere [emettere 225](https://github.com/Microsoft/azuredatastudio/issues/225): Mancata corrispondenza di colore (parola chiave).
  - Correggere [emettere 60](https://github.com/Microsoft/azuredatastudio/issues/60): Sql non valido colore l'evidenziazione della sintassi quando si usa la tabella temporanea nella clausola from.

## <a name="january-2018"></a>Gennaio 2018

17 gennaio 2018 &nbsp;  /  &nbsp; versione: 0.25.4 &nbsp;  /  &nbsp; anteprima pubblica

L'*anteprima pubblica di gennaio* include alcuni suggerimenti sulle funzionalità e correzioni di bug con priorità alta.  Questa versione include i miglioramenti seguenti:

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| Le connessioni server salvate sono disponibili nella finestra di dialogo di connessione. | &nbsp; |
| Abilitare l'uscita Hot,  disattivata per impostazione predefinita. Per abilitarla vedere [impostazione uscita Hot](settings.md#hot-exit). | &nbsp; |
| Ogni scheda è ora contraddistinta dal colore del relativo gruppo di server. La colorazione della scheda è disattivata per impostazione predefinita, per abilitare vedere [impostazione del colore di una scheda](settings.md#tab-color). | &nbsp; |
| Modificata l'etichetta *Nome Server* in *Server* nella finestra di dialogo di connessione. | &nbsp; |
| Corretto il comando non funzionante *Esegui Query corrente*. | &nbsp; |
| Corretto il bug dello scripting di interruzione di tracina e rilascia. | &nbsp; |
| Corretta l'icona del Menu Start bloccata in modo non corretto. | &nbsp; |
| Aggiunta l'icona mancante dell'Account di Azure. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>Dicembre 2017

Il 19 dicembre 2017 &nbsp;  /  &nbsp; versione: 0.24.1 &nbsp; / &nbsp; Public Preview

L'*anteprima pubblica di dicembre* include diverse correzioni di bug in tutte le aree di funzionalità, nonché i miglioramenti seguenti:

&nbsp;

| Cambia | Dettagli |
| :----- | :------ |
| La finestra di dialogo per l'aggiunta automatica della regola del firewall è ora disponibile per consentire la connessione a Database SQL di Azure e Azure SQL Data Warehouse. | &nbsp; |
| Aggiunta l'installazione di Windows e i pacchetti di installazione Linux DEB e RPM. | &nbsp; |
| Aggiunto l'editor di layout della dashboard. | &nbsp; |
| Aggiunti i comandi *Script come ALTER* e *Script come EXECUTE*. | &nbsp; |
| Aggiunto il comando *Esegui la query corrente con il piano effettivo*. | &nbsp; |
| Integrato l'editor di codice di Visual Studio 1.18.1. | &nbsp; |
| Abilitato il caricamento dei file con estensione VSIX. | &nbsp; |
| Supporta la sintassi di iterazione batch "GO N". | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>Novembre 2017

15 novembre 2017 &nbsp;  /  &nbsp; versione: 0.23.6

- Versione iniziale di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="next-steps"></a>Passaggi successivi

Seguire una delle guide rapide qui sotto per iniziare:

- [Connettersi ed eseguire query in SQL Server](quickstart-sql-server.md)
- [Connettersi ed eseguire query in Database SQL di Azure](quickstart-sql-database.md)
- [Connettersi ed eseguire query in Azure Data Warehouse](quickstart-sql-dw.md)

Contribuire a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
