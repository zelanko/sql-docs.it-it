---
title: Regole di confronto e supporto Unicode | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1985e7c3fc55f6783c88569c196713050fa40287
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918947"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
  Le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forniscono regole di ordinamento e proprietà di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati per i dati. Le regole di confronto usate con dati di tipo carattere, quali `char` e `varchar`, definiscono la tabella codici e i caratteri corrispondenti che possono essere rappresentati per quel tipo di dati. Sia che si installi una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si ripristini il backup di un database o si stabiliscano connessioni tra database server e client, è importante comprendere i requisiti delle impostazioni locali, l'ordinamento e la modalità di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati dei dati da usare. Per visualizzare l'elenco delle regole di confronto disponibili nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql).  
  
 Selezionando le regole di confronto per un server, un database, una colonna o un'espressione, vengono assegnate determinate caratteristiche ai dati che influiranno sui risultati di molte operazioni eseguite nel database. Ad esempio, quando viene costruita una query tramite ORDER BY, l'ordinamento del set di risultati può dipendere dalle regole di confronto applicate al database o specificate in una clausola COLLATE al livello di espressione della query.  
  
 Per usare in modo ottimale il supporto delle regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario approfondire la conoscenza dei termini specificati in questo argomento e delle relative relazioni con le caratteristiche dei dati.  
  
  
###  <a name="Collation_Defn"></a> Confronto  
 Le regole di confronto specificano i modelli di bit che rappresentano i caratteri in un set di dati. Le regole di confronto determinano inoltre le regole in base alle quali i dati vengono ordinati e confrontati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'archiviazione di oggetti con regole di confronto diverse in un singolo database. Per le colonne non Unicode, l'impostazione delle regole di confronto specifica la tabella codici dei dati e i caratteri che possono essere rappresentati. Per i dati spostati tra colonne non Unicode, è necessaria la conversione dalla tabella codici di origine a quella di destinazione.  
  
 I risultati di un'istruzione[!INCLUDE[tsql](../../includes/tsql-md.md)] possono variare se l'istruzione viene eseguita nel contesto di database diversi che utilizzano impostazioni diverse per le regole di confronto. Se possibile, usare regole di confronto standardizzate per l'organizzazione. In questo modo, non è necessario specificare esplicitamente le regole di confronto in ogni carattere o espressione Unicode. Se è necessario usare oggetti con impostazioni diverse per tabelle codici e regole di confronto, codificare le query in modo da considerare la precedenza delle regole di confronto. Per altre informazioni, vedere [Precedenza delle regole di confronto (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql).  
  
 Le opzioni associate alle regole di confronto sono: distinzione tra maiuscole e minuscole, distinzione tra caratteri accentati e non accentati, distinzione Kana e distinzione di larghezza. Tali opzioni vengono specificate aggiungendole al nome delle regole di confronto. Ad esempio, le regole di confronto `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` prevedono: distinzione tra maiuscole e minuscole, distinzione tra caratteri accentati e non accentati, distinzione Kana e distinzione di larghezza. Nella tabella riportata di seguito viene descritto il comportamento associato a queste opzioni.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Distinzione maiuscole/minuscole (_CS)|Opera una distinzione tra lettere maiuscole e minuscole. Se viene selezionata questa opzione, le lettere minuscole precedono le versioni maiuscole corrispondenti nell'ordinamento. Se questa opzione non viene selezionata, le regole di confronto non effettueranno distinzione tra maiuscole e minuscole. Ovvero, in SQL Server non viene operata una distinzione tra lettere maiuscole e minuscole, che vengono considerate identiche ai fini dell'ordinamento. È possibile selezionare in modo esplicito l'esclusione della distinzione tra maiuscole e minuscole specificando _CI.|  
|Distinzione caratteri accentati/non accentati (_AS)|Opera una distinzione tra caratteri accentati e non accentati. Ad esempio, 'un 'non è uguale a'???'. Se questa opzione non viene selezionata, le regole di confronto non effettueranno distinzione tra caratteri accentati e non accentati. Ovvero, in SQL Server non viene opera una distinzione tra caratteri accentati e non accentati, che vengono considerati identici ai fini dell'ordinamento. È possibile selezionare in modo esplicito l'esclusione della distinzione tra caratteri accentati e non accentati specificando _AI.|  
|Distinzione Kana (_KS)|Consente di distinguere tra i due tipi di caratteri kana giapponesi: Hiragana e Katakana. Se questa opzione non viene selezionata, le regole di confronto non effettuano distinzione tra caratteri Kana. Ovvero, in SQL Server i caratteri Hiragana e Katakana vengono considerati identici ai fini dell'ordinamento. Omettere questa opzione è il solo metodo per specificare di non effettuare la distinzione Kana.|  
|Distinzione larghezza (_WS)|Opera una distinzione tra caratteri a larghezza intera e caratteri a metà larghezza. Se questa opzione non viene selezionata, SQL Server considera identiche le rappresentazioni con caratteri a larghezza intera e a metà larghezza dello stesso carattere ai fini dell'ordinamento. Omettere questa opzione è il solo metodo per specificare di non effettuare la distinzione larghezza.|  
  
 In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati i seguenti set di regole di confronto:  
  
 Regole di confronto di Windows  
 Le regole di confronto di Windows definiscono regole per l'archiviazione dei dati di tipo carattere basate sulle impostazioni locali del sistema Windows associate. Per le regole di confronto di Windows, il confronto dei dati non Unicode è implementato mediante lo stesso algoritmo dei dati Unicode. Le regole di confronto di base di Windows specificano l'alfabeto o la lingua da usare quando viene applicato l'ordinamento del dizionario, nonché la tabella codici usata per l'archiviazione di dati di tipo carattere non Unicode. Sia l'ordinamento Unicode che quello non Unicode sono compatibili con i confronti di stringhe di una versione specifica di Windows. In questo modo viene garantita la consistenza tra i tipi di dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli sviluppatori possono ordinare le stringhe all'interno delle applicazioni mediante le stesse regole usate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).  
  
 Regole di confronto binarie  
 Le regole di confronto binarie ordinano i dati in base alla sequenza di valori codificati definiti dalle impostazioni locali e dal tipo di dati. Per tali regole è prevista la distinzione tra maiuscole e minuscole. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le regole di confronto binarie definiscono le impostazioni locali e la tabella codici ANSI che verranno usate. In questo modo viene applicato un ordinamento binario. Grazie alla loro semplicità, le regole di confronto binarie consentono di migliorare le prestazioni dell'applicazione. Per i tipi di dati non Unicode, il confronto dei dati è basato sui punti di codice definiti nella tabella codici ANSI. Per i tipi di dati Unicode, il confronto dei dati è basato sui punti di codice Unicode. Per le regole di confronto binarie nei tipi di dati Unicode, le impostazioni locali non vengono considerate ai fini dell'ordinamento dei dati. Ad esempio, l'utilizzo di Latin_1_General_BIN e Japanese_BIN su dati Unicode restituisce risultati di ordinamento identici.  
  
 Esistono due tipi di regole di confronto binarie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: le regole di confronto meno recenti `BIN` e le regole di confronto più recenti `BIN2`. Nelle regole di confronto `BIN2` tutti i caratteri vengono ordinati in base ai relativi punti di codice. Nelle regole di confronto `BIN` solo il primo carattere viene ordinato in base al punto di codice e i restanti caratteri vengono ordinati in base ai relativi valori di byte. Poiché la piattaforma Intel si avvale di un'architettura little endian, i caratteri di codice Unicode vengono sempre scambiati con i byte archiviati.  
  
 regole di confronto di SQL Server  
 Le regole di confronto[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_*) garantiscono la compatibilità di ordinamento con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le regole di ordinamento del dizionario per i dati non Unicode sono compatibili con qualsiasi routine di ordinamento fornita dai sistemi operativi Windows. Tuttavia l'ordinamento dei dati Unicode è compatibile con una versione specifica di regole di ordinamento di Windows. Poiché le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] differiscono per i dati non Unicode e i dati Unicode, confrontando gli stessi dati verranno visualizzati risultati diversi, a seconda del tipo di dati sottostante. Per altre informazioni, vedere [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql).  
  
> [!NOTE]
>  Quando si aggiorna un'istanza in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_*) per assicurare la compatibilità con le istanze esistenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché le regole di confronto predefinite per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono definite durante la configurazione, è importante specificare attentamente le impostazioni delle regole di confronto quando le condizioni riportate di seguito sono vere:  
> 
>  -   Il codice dell'applicazione dipende dal comportamento di regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti.  
> -   È necessario archiviare dati di tipo carattere in più lingue.  
  
 L'impostazione delle regole di confronto è supportata ai seguenti livelli di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 Regole di confronto a livello di server  
 Le regole di confronto predefinite del server vengono impostate durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e diventano le regole predefinite anche per i database di sistema e per tutti i database utente. Si noti che non è possibile selezionare le regole di confronto solo Unicode durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , perché non sono supportate come regole di confronto a livello server.  
  
 Una volta che le regole di confronto sono state assegnate al server, non è possibile modificarle se non esportando tutti i dati e gli oggetti di database, ricostruendo il database `master` e importando tutti i dati e gli oggetti di database. Anziché modificare le regole di confronto predefinite di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare quelle desiderate al momento della creazione di nuovi database o colonne di database.  
  
 Regole di confronto a livello di database  
 Quando viene creato o modificato un database, è possibile usare la clausola COLLATE dell'istruzione CREATE DATABASE o ALTER DATABASE per specificare regole di confronto predefinite del database. Se non viene specificata alcuna regola di confronto, al database vengono assegnate le regole di confronto del server.  
  
 Non è possibile modificare le regole di confronto del database di sistema se non modificandole per il server.  
  
 Le regole di confronto del database vengono usate per tutti i metadati nel database e rappresentano l'impostazione predefinita per tutte le colonne stringa, gli oggetti temporanei, i nomi di variabili e qualsiasi altra stringa usata nel database. Quando le regole di confronto di un database utente vengono modificate, è possibile che si verifichino conflitti tra le regole di confronto quando vengono eseguite query nelle tabelle temporanee di accesso al database. Le tabelle temporanee sono sempre archiviate nel database di sistema `tempdb`, che utilizzerà le regole di confronto per l'istanza. L'esecuzione di query di confronto dei dati di tipo carattere tra database utente e `tempdb` può non riuscire se le regole di confronto causano un conflitto nella valutazione dei dati di tipo carattere. È possibile risolvere il problema specificando la clausola COLLATE nella query. Per altre informazioni, vedere [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations).  
  
 Regole di confronto a livello di colonna  
 Quando una tabella viene creata o modificata, è possibile specificare regole di confronto per ciascuna colonna di stringhe di caratteri utilizzando la clausola COLLATE. Se non si specificano regole di confronto, alla colonna verranno assegnate le regole di confronto predefinite del database.  
  
 Regole di confronto a livello di espressione  
 Le regole di confronto a livello di espressione vengono impostate al momento dell'esecuzione di un'istruzione e interessano la modalità di restituzione di un set di risultati. In questo modo i risultati dell'ordinamento ORDER BY possono essere specifici delle impostazioni locali. Per implementare regole di confronto a livello di espressione, usare una clausola COLLATE simile alla seguente:  
  
```  
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;  
```  
  
  
###  <a name="Locale_Defn"></a> Impostazioni locali  
 Le impostazioni locali rappresentano un set di informazioni associate a un paese o a una lingua. Possono includere il nome e l'identificatore della lingua parlata, lo script usato per la scrittura della lingua e le convenzioni culturali. Le regole di confronto possono essere associate a uno o più set di impostazioni locali. Per altre informazioni, vedere [ID delle impostazioni locali assegnati da Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).  
  
  
###  <a name="Code_Page_Defn"></a> Code Page  
 Una tabella codici è un set ordinato di caratteri di uno script specifico nel quale a ogni carattere viene associato un indice numerico o un valore punto di codice. Per tabella codici di Windows si intende in genere un *set di caratteri* o *charset*. Queste tabelle vengono usate per supportare i set di caratteri e i layout di tastiera impiegati per le diverse impostazioni locali di Windows.  
  
  
###  <a name="Sort_Order_Defn"></a> Sort Order  
 L'ordinamento specifica il modo in cui vengono ordinati i valori dei dati. e influisce sui risultati del confronto dei dati stessi. I dati vengono ordinati tramite regole di confronto e possono essere ottimizzati tramite indici.  
  
  
##  <a name="Unicode_Defn"></a> Supporto Unicode  
 Unicode è uno standard per il mapping dei punti di codice ai caratteri. Dato che è progettato per supportare tutti i caratteri di tutte le lingue del mondo, non è necessario che set di caratteri diversi vengano gestiti da tabelle codici diverse. Se vengono archiviati dati di tipo carattere che riflettono più lingue, usare sempre tipi di dati Unicode (`nchar`, `nvarchar` e `ntext`) anziché tipi di dati non Unicode (`char`, `varchar` e `text`).  
  
 Ai tipi di dati non Unicode sono associate numerose limitazioni, in quanto nei computer non Unicode sarà disponibile una sola tabella codici. Utilizzando tipi di dati Unicode è possibile ottenere prestazioni migliori, in quanto è necessario un minor numero di conversioni tramite la tabella codici. Le regole di confronto Unicode devono essere selezionate singolarmente a livello di database, di colonna o di espressione perché non sono supportate a livello di server.  
  
 Le tabelle codici usate da un client vengono determinate in base alle impostazioni del sistema operativo. Per impostare le tabelle codici del client nel sistema operativo Windows usare l'opzione **Impostazioni internazionali** del Pannello di controllo.  
  
 Quando si spostano dati da un server a un client, le regole di confronto del server potrebbero non essere riconosciute dai driver client meno recenti. Questa situazione può verificarsi quando si spostano dati da un server Unicode a un client non Unicode. La migliore opzione potrebbe consistere nell'aggiornare il sistema operativo client affinché vengano aggiornate le regole di confronto del sistema sottostanti. Se nel client è installato il software client del database, è possibile applicare un aggiornamento dei servizi a tale software.  
  
 È anche possibile tentare di usare regole di confronto diverse per i dati nel server. Scegliere regole di confronto per le quali viene eseguito il mapping a una tabella codici nel client.  
  
 Per usare le regole di confronto UTF-16 disponibili in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], è possibile selezionare una delle regole di confronto `_SC` dei caratteri supplementari (solo regole di confronto di Windows) per migliorare la ricerca e l'ordinamento di alcuni caratteri Unicode.  
  
 Per valutare i problemi relativi all'utilizzo di tipi di dati Unicode o non Unicode, è necessario eseguire il test dello scenario per verificare le differenze di prestazioni nell'ambiente specifico. È consigliabile standardizzare le regole di confronto usate nei sistemi presenti nell'ambito dell'organizzazione, quindi distribuire server e client Unicode laddove possibile.  
  
 In molti casi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interagirà con altri server o client e l'organizzazione potrà usare più standard di accesso ai dati tra applicazioni e istanze del server. I client[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono principalmente di due tipi:  
  
-   **Client Unicode** che usano OLE DB e ODBC (Open Database Connectivity) versione 3.7 o successive.  
  
-   **Client non Unicode** che usano DB-Library e ODBC versione 3.6 o precedenti.  
  
 Nella tabella seguente sono riportate informazioni sull'utilizzo di dati multilingue con diverse combinazioni di server Unicode e non Unicode.  
  
|Server|Client|Vantaggi o limitazioni|  
|------------|------------|-----------------------------|  
|Unicode|Unicode|Poiché i dati Unicode verranno usati in tutto il sistema, questo scenario fornisce prestazioni ottimali e la migliore protezione da eventuali danni ai dati recuperati. Si applica ad ADO (ActiveX Data Objects), OLE DB e ODBC versione 3.7 o successive.|  
|Unicode|Non Unicode|In questo scenario, in particolare con le connessioni tra un server in cui è in esecuzione un sistema operativo più recente e un client in cui è in esecuzione una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o di un sistema operativo, possono riscontrarsi limitazioni o errori quando si spostano i dati in un computer client. Per convertire i dati, verrà tentato il mapping tra i dati Unicode presenti sul server e una tabella codici corrispondente sul client non Unicode.|  
|Non Unicode|Unicode|Non si tratta di una configurazione ideale per l'utilizzo di dati multilingue. Non sarà possibile scrivere dati Unicode nel server non Unicode e potrebbero verificarsi problemi all'invio dei dati ai server che non rientrano nella tabella codici del server.|  
|Non Unicode|Non Unicode|Si tratta di uno scenario che presenta numerose limitazioni per i dati multilingue. È possibile usare solo una tabella codici.|  
  
  
##  <a name="Supplementary_Characters"></a> Caratteri supplementari  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fornisce i tipi di dati, ad esempio `nchar` e `nvarchar` per archiviare dati Unicode. Questi tipi di dati codificano il testo in un formato denominato *UTF-16*. L'Unicode Consortium assegna a ogni carattere un punto di codice univoco, che corrisponde a un valore nell'intervallo compreso tra 0x0000 e 0x10FFFF. Benché i caratteri più frequentemente usati siano associati a valori di punti di codice compresi in una parola a 16 bit in memoria e su disco, i caratteri con valori di punti di codice maggiori di 0xFFFF richiedono due parole a 16 bit consecutive. Questi caratteri sono denominati *caratteri supplementari*e le due parole a 16 bit consecutive sono denominate *coppie di surrogati*.  
  
 Se si utilizzano caratteri supplementari:  
  
-   I caratteri supplementari possono essere usati in operazioni di ordinamento e confronto solo con le versioni delle regole di confronto 90 o successive.  
  
-   Tutte le regole di confronto di livello _100 supportano l'ordinamento linguistico con caratteri supplementari.  
  
-   L'utilizzo dei caratteri supplementari in metadati, ad esempio in nomi di oggetti di database, non è supportato.  
  
-   A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], è possibile usare una nuova famiglia di regole di confronto per caratteri supplementari (SC) con i tipi di dati `nchar`, `nvarchar` e `sql_variant`. Ad esempio: `Latin1_General_100_CI_AS_SC`o, se si utilizzano regole di confronto giapponesi, `Japanese_Bushu_Kakusu_100_CI_AS_SC`.  
  
     Il flag SC può essere applicato a:  
  
    -   Regole di confronto di Windows versione 90  
  
    -   Regole di confronto di Windows versione 100  
  
     Il flag SC non può essere applicato a:  
  
    -   Regole di confronto di Windows senza versione, versione 80  
  
    -   Regole di confronto binarie BIN o BIN2  
  
    -   Regole di confronto SQL*  
  
 Nella tabella seguente viene confrontato il comportamento di alcune funzioni per i valori stringa e di alcuni operatori di stringa quando vengono usati caratteri supplementari con e senza regole di confronto SC.  
  
|Funzione per i valori stringa o operatore di stringa|Con regole di confronto SC|Senza regole di confronto SC|  
|---------------------------------|--------------------------|-----------------------------|  
|[CHARINDEX](/sql/t-sql/functions/charindex-transact-sql)<br /><br /> [LEN](/sql/t-sql/functions/len-transact-sql)<br /><br /> [PATINDEX](/sql/t-sql/functions/patindex-transact-sql)|La coppia di surrogati UTF-16 viene conteggiata come singolo punto di codice.|La coppia di surrogati UTF-16 viene conteggiata come due punti di codice.|  
|[LEFT](/sql/t-sql/functions/left-transact-sql)<br /><br /> [REPLACE](/sql/t-sql/functions/replace-transact-sql)<br /><br /> [REVERSE](/sql/t-sql/functions/reverse-transact-sql)<br /><br /> [RIGHT](/sql/t-sql/functions/right-transact-sql)<br /><br /> [SUBSTRING](/sql/t-sql/functions/substring-transact-sql)<br /><br /> [STUFF](/sql/t-sql/functions/stuff-transact-sql)|Queste funzioni considerano ogni coppia di surrogati un singolo punto di codice e funzionano come previsto.|Queste funzioni possono dividere qualsiasi coppia di surrogati e provocare risultati imprevisti.|  
|[NCHAR](/sql/t-sql/functions/nchar-transact-sql)|Restituisce il carattere corrispondente al valore del punto di codice Unicode specificato nell'intervallo compreso tra 0 e 0x10FFFF. Se il valore specificato è incluso nell'intervallo compreso tra 0 e 0xFFFF, viene restituito un carattere. Per valori superiori, viene restituito il surrogato corrispondente.|Un valore maggiore di 0xFFFF restituisce NULL anziché il surrogato corrispondente.|  
|[UNICODE](/sql/t-sql/functions/unicode-transact-sql)|Restituisce un punto di codice UTF-16 nell'intervallo compreso tra 0 e 0x10FFFF.|Restituisce un punto di codice UCS-2 nell'intervallo compreso tra 0 e 0xFFFF.|  
|[Carattere jolly per corrispondenze di singoli caratteri](/sql/t-sql/language-elements/wildcard-match-one-character-transact-sql)<br /><br /> [Carattere jolly per la mancata corrispondenza dei caratteri](/sql/t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql)|Sono supportati caratteri supplementari per tutte le operazioni con caratteri jolly.|Non sono supportati caratteri supplementari per queste operazioni con caratteri jolly. Sono supportati altri operatori jolly.|  
  
  
##  <a name="GB18030"></a> Supporto GB18030  
 GB18030 è uno standard separato usato nella Repubblica popolare Cinese per la codifica dei caratteri cinesi. In GB18030, i caratteri possono essere di 1, 2 o 4 byte di lunghezza. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre supporto per i caratteri con codifica GB18030 consentendone il riconoscimento al momento dell'ingresso nel server da un'applicazione client e la conversione e archiviazione come caratteri Unicode a livello nativo. Dopo essere stati archiviati nel server, tali caratteri vengono trattati come caratteri Unicode in tutte le operazioni successive. È possibile usare una qualsiasi regola di confronto cinese, preferibilmente la versione 100 più recente. Tutte le regole di confronto di livello _100 supportano l'ordinamento linguistico con caratteri GB18030. Se nei dati sono inclusi caratteri supplementari (coppie surrogate), è possibile usare le regole di confronto SC in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] per migliorare la ricerca e l'ordinamento.  
  
  
##  <a name="Complex_script"></a> Supporto di lingue con alfabeti non latini  
 In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere supportata l'immissione, l'archiviazione, la modifica e la visualizzazione di lingue con alfabeti non latini. Le lingue con alfabeti non latini includono:  
  
-   Lingue che presentano una combinazione di testo scritto sia da destra verso sinistra sia da sinistra verso destra, ad esempio una combinazione di testo in arabo e inglese.  
  
-   Lingue i cui caratteri assumono una forma diversa a seconda della posizione oppure combinati con altri caratteri, ad esempio arabi, indiani e thai.  
  
-   Lingue come il thai che richiedono dizionari interni per il riconoscimento delle parole in quanto non vi sono interruzioni tra di loro.  
  
 Le applicazioni di database che interagiscono con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono usare controlli che supportano le lingue con alfabeti non latini. I form standard di Windows creati in codice gestito sono abilitati per le lingue con alfabeti non latini.  
  
  
##  <a name="Related_Tasks"></a> Attività correlate  
  
|Attività|Argomento|  
|----------|-----------|  
|Viene descritto come impostare o modificare le regole di confronto dell'istanza di SQL Server.|[Impostazione o modifica di regole di confronto del server](set-or-change-the-server-collation.md)|  
|Viene descritto come impostare o modificare le regole di confronto di un database utente.|[Impostare o modificare le regole di confronto del database](set-or-change-the-database-collation.md)|  
|Viene descritto come impostare o modificare le regole di confronto di una colonna nel database.|[Impostare o modificare le regole di confronto delle colonne](set-or-change-the-column-collation.md)|  
|Viene descritto come restituire informazioni sulle regole di confronto a livello di server, di database o di colonna.|[Visualizzazione di informazioni sulle regole di confronto](view-collation-information.md)|  
|Viene descritto come scrivere istruzioni Transact-SQL per aumentarne la portabilità da un linguaggio a un altro o per supportare più linguaggi con maggiore facilità.|[Scrittura di istruzioni Transact-SQL internazionali](write-international-transact-sql-statements.md)|  
|Viene descritto come modificare la lingua dei messaggi di errore e le preferenze di utilizzo e visualizzazione dei dati di tipo data, ora e valuta.|[Impostazione di una lingua di sessione](set-a-session-language.md)|  
  
  
##  <a name="Related_Content"></a> Contenuto correlato  
 [SQL Server Best Practices Collation Change](https://go.microsoft.com/fwlink/?LinkId=113891)  
  
 [SQL Server Best Practices Migration to Unicode](https://go.microsoft.com/fwlink/?LinkId=113890)  
  
 [Sito Web Unicode Consortium](https://go.microsoft.com/fwlink/?LinkId=48619)  
  
## <a name="see-also"></a>Vedere anche  
 [Regole di confronto dei database indipendenti](../databases/contained-database-collations.md)   
 [Scelta di una lingua durante la creazione di un indice full-text](../search/choose-a-language-when-creating-a-full-text-index.md)   
 [sys.fn_helpcollations (Transact-SQL)](https://msdn.microsoft.com/library/ms187963(SQL.130).aspx)  
  
  
