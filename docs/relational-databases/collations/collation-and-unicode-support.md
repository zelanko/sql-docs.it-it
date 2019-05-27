---
title: Regole di confronto e supporto Unicode | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97e66c1c276131876a8a74ab49627f43374cb78f
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775035"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forniscono regole di ordinamento e proprietà di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati per i dati. Le regole di confronto usate con dati di tipo carattere, quali **char** e **varchar** , definiscono la tabella codici e i caratteri corrispondenti che possono essere rappresentati per quel tipo di dati. Sia che si installi una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si ripristini il backup di un database o si stabiliscano connessioni tra database server e client, è importante comprendere i requisiti delle impostazioni locali, l'ordinamento e la modalità di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati dei dati da usare. Per visualizzare l'elenco delle regole di confronto disponibili nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md).    
    
Selezionando le regole di confronto per un server, un database, una colonna o un'espressione, vengono assegnate determinate caratteristiche ai dati che influiscono sui risultati di molte operazioni eseguite nel database. Ad esempio, quando viene costruita una query tramite `ORDER BY`, l'ordinamento del set di risultati può dipendere dalle regole di confronto applicate al database o specificate in una clausola `COLLATE` al livello di espressione della query.    
    
Per usare in modo ottimale il supporto delle regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario approfondire la conoscenza dei termini specificati in questo argomento e delle relative relazioni con le caratteristiche dei dati.    
    
##  <a name="Terms"></a> Termini delle regole di confronto    
    
-   [Confronto](#Collation_Defn)    
    
-   [Impostazioni locali](#Locale_Defn)    
    
-   [Tabella codici](#Code_Page_Defn)    
    
-   [Ordinamento](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> Confronto    
Le regole di confronto specificano i modelli di bit che rappresentano i caratteri in un set di dati. Le regole di confronto determinano inoltre le regole in base alle quali i dati vengono ordinati e confrontati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'archiviazione di oggetti con regole di confronto diverse in un singolo database. Per le colonne non Unicode, l'impostazione delle regole di confronto specifica la tabella codici dei dati e i caratteri che possono essere rappresentati. Per i dati spostati tra colonne non Unicode, è necessaria la conversione dalla tabella codici di origine a quella di destinazione.    
    
I risultati di un'istruzione[!INCLUDE[tsql](../../includes/tsql-md.md)] possono variare se l'istruzione viene eseguita nel contesto di database diversi che utilizzano impostazioni diverse per le regole di confronto. Se possibile, usare regole di confronto standardizzate per l'organizzazione. In questo modo, non è necessario specificare esplicitamente le regole di confronto in ogni carattere o espressione Unicode. Se è necessario usare oggetti con impostazioni diverse per tabelle codici e regole di confronto, codificare le query in modo da considerare la precedenza delle regole di confronto. Per altre informazioni, vedere [Precedenza delle regole di confronto (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md).    
    
Alle regole di confronto sono associate le opzioni seguenti: distinzione tra maiuscole e minuscole, distinzione tra caratteri accentati e non accentati, distinzione dei caratteri Kana, distinzione di larghezza e distinzione dei selettori di variazione. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduce un'opzione aggiuntiva per la codifica [UTF-8](https://www.wikipedia.org/wiki/UTF-8). Tali opzioni vengono specificate aggiungendole al nome delle regole di confronto. Ad esempio, le regole di confronto `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8` prevedono distinzione tra maiuscole e minuscole, distinzione tra caratteri accentati e non accentati, distinzione dei caratteri Kana, distinzione di larghezza e codifica UTF-8. Sempre a titolo di esempio, le regole di confronto `Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS` prevedono le opzioni seguenti: nessuna distinzione tra lettere maiuscole e minuscole, nessuna distinzione tra caratteri accentati e non accentati, distinzione dei caratteri Kana, distinzione di larghezza, distinzione dei selettori di variazione e usano la codifica non Unicode. La tabella seguente descrive il comportamento associato a queste opzioni.    
    
|Opzione|Descrizione|    
|------------|-----------------|    
|Distinzione maiuscole/minuscole (_CS)|Opera una distinzione tra lettere maiuscole e minuscole. Se viene selezionata questa opzione, le lettere minuscole precedono le versioni maiuscole corrispondenti nell'ordinamento. Se questa opzione non viene selezionata, le regole di confronto non fanno distinzione tra maiuscole e minuscole. Ovvero, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera identiche le lettere maiuscole e minuscole ai fini dell'ordinamento. È possibile selezionare in modo esplicito l'esclusione della distinzione tra maiuscole e minuscole specificando _CI.|    
|Distinzione caratteri accentati/non accentati (_AS)|Opera una distinzione tra caratteri accentati e non accentati. Il carattere 'a', ad esempio, non viene considerato uguale ad 'ấ'. Se questa opzione non viene selezionata, le regole di confronto non fanno distinzione tra caratteri accentati e non accentati. Ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera identici i caratteri accentati e non accentati ai fini dell'ordinamento. È possibile selezionare in modo esplicito l'esclusione della distinzione tra caratteri accentati e non accentati specificando _AI.|    
|Distinzione Kana (_KS)|Opera una distinzione tra i due tipi di caratteri Kana giapponesi, ovvero Hiragana e Katakana. Se questa opzione non viene selezionata, le regole di confronto non effettuano distinzione tra caratteri Kana. Ovvero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera uguali i caratteri Hiragana e Katakana ai fini dell'ordinamento. Omettere questa opzione è il solo metodo per specificare di non effettuare la distinzione Kana.|    
|Distinzione larghezza (_WS)|Opera una distinzione tra caratteri a larghezza intera e caratteri a metà larghezza. Se questa opzione non viene selezionata, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera identiche le rappresentazioni con caratteri a larghezza intera e a metà larghezza dello stesso carattere ai fini dell'ordinamento. Omettere questa opzione è il solo metodo per specificare di non effettuare la distinzione larghezza.|    
|Distinzione dei selettori di variazione (_VSS) | Opera una distinzione tra vari selettori di variazione di simboli ideografici nelle regole di confronto giapponesi Japanese_Bushu_Kakusu_140 e Japanese_XJIS_140 introdotte inizialmente in [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. Una sequenza di variazione è costituita da un carattere di base e da un selettore di variazione aggiuntivo. Se questa opzione _VSS non è selezionata, le regole di confronto non fanno distinzione tra selettori di variazione e il selettore di variazione non viene considerato nel confronto. In altri termini, SQL Server considera identici, ai fini dell'ordinamento, i caratteri basati sullo stesso carattere con diversi selettori di variazione. Vedere anche  [Unicode Ideographic Variation Database](https://www.unicode.org/reports/tr37/)(Database di variazioni di simboli ideografici Unicode). <br/><br/> Le regole di confronto con distinzione tra selettori di variazione (_VSS) non sono supportate negli indici di ricerca full-text. Questi indici supportano solo le opzioni Distinzione caratteri accentati/non accentati (_AS), Distinzione Kana (_KS) e Distinzione larghezza (_WS). I motori di CLR e XML in SQL Server non supportano i selettori di variazione (_VSS).
|UTF-8 (_UTF8)|Abilita l'archiviazione dei dati con codifica UTF-8 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se questa opzione non viene selezionata, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa il formato di codifica non Unicode predefinito per i tipi di dati applicabili.| 
    
 In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati i seguenti set di regole di confronto:    
    
#### <a name="windows-collations"></a>Regole di confronto di Windows    
Le regole di confronto di Windows definiscono regole per l'archiviazione dei dati di tipo carattere basate sulle impostazioni locali del sistema Windows associate. Per le regole di confronto di Windows, il confronto dei dati non Unicode è implementato mediante lo stesso algoritmo dei dati Unicode. Le regole di confronto di base di Windows specificano l'alfabeto o la lingua da usare quando viene applicato l'ordinamento del dizionario, nonché la tabella codici usata per l'archiviazione di dati di tipo carattere non Unicode. Sia l'ordinamento Unicode che quello non Unicode sono compatibili con i confronti di stringhe di una versione specifica di Windows. In questo modo viene garantita la consistenza tra i tipi di dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli sviluppatori possono ordinare le stringhe all'interno delle applicazioni mediante le stesse regole usate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Windows_collation_name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md).    
    
#### <a name="binary-collations"></a>Regole di confronto binarie    
Le regole di confronto binarie ordinano i dati in base alla sequenza di valori codificati definiti dalle impostazioni locali e dal tipo di dati. Per tali regole è prevista la distinzione tra maiuscole e minuscole. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le regole di confronto binarie definiscono le impostazioni locali e la tabella codici ANSI da usare. In questo modo viene applicato un ordinamento binario. Grazie alla loro semplicità, le regole di confronto binarie consentono di migliorare le prestazioni dell'applicazione. Per i tipi di dati non Unicode, il confronto dei dati è basato sui punti di codice definiti nella tabella codici ANSI. Per i tipi di dati Unicode, il confronto dei dati è basato sui punti di codice Unicode. Per le regole di confronto binarie nei tipi di dati Unicode, le impostazioni locali non vengono considerate ai fini dell'ordinamento dei dati. Ad esempio, l'utilizzo di Latin_1_General_BIN e Japanese_BIN su dati Unicode restituisce risultati di ordinamento identici.    
    
Esistono due tipi di regole di confronto binarie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: le regole di confronto **BIN** meno recenti e quelle più recenti **BIN2** . Nelle regole di confronto **BIN2** tutti i caratteri vengono ordinati in base ai relativi punti di codice. Nelle regole di confronto **BIN** solo il primo carattere viene ordinato in base al punto di codice e i restanti caratteri vengono ordinati in base ai relativi valori di byte. Poiché la piattaforma Intel si avvale di un'architettura little endian, i caratteri di codice Unicode vengono sempre scambiati con i byte archiviati.    
    
#### <a name="sql-server-collations"></a>regole di confronto di SQL Server    
Le regole di confronto[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_\*) garantiscono la compatibilità di ordinamento con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le regole di ordinamento del dizionario per i dati non Unicode sono compatibili con qualsiasi routine di ordinamento fornita dai sistemi operativi Windows. Tuttavia l'ordinamento dei dati Unicode è compatibile con una versione specifica di regole di ordinamento di Windows. Dato che le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] differiscono per i dati non Unicode e i dati Unicode, confrontando gli stessi dati vengono visualizzati risultati diversi, a seconda del tipo di dati sottostante. Per altre informazioni, vedere [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).    
    
> [!NOTE]    
> Quando si aggiorna un'istanza in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_\*) per assicurare la compatibilità con le istanze esistenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché le regole di confronto predefinite per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono definite durante la configurazione, è importante specificare attentamente le impostazioni delle regole di confronto quando le condizioni riportate di seguito sono vere:    
>     
> -   Il codice dell'applicazione dipende dal comportamento di regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti.    
> -   È necessario archiviare dati di tipo carattere in più lingue.    
    
 L'impostazione delle regole di confronto è supportata ai seguenti livelli di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:    
    
#### <a name="server-level-collations"></a>Regole di confronto a livello di server   
Le regole di confronto predefinite del server vengono impostate durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e diventano le regole predefinite anche per i database di sistema e per tutti i database utente. Si noti che non è possibile selezionare le regole di confronto solo Unicode durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , perché non sono supportate come regole di confronto a livello server.    
    
Una volta che le regole di confronto sono state assegnate al server, non è possibile modificarle se non esportando tutti i dati e gli oggetti di database, ricostruendo il database **master** e importando tutti i dati e gli oggetti di database. Anziché modificare le regole di confronto predefinite di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare quelle desiderate al momento della creazione di nuovi database o colonne di database.    
    
#### <a name="database-level-collations"></a>Regole di confronto a livello di database    
Quando viene creato o modificato un database, è possibile usare la clausola COLLATE dell'istruzione CREATE DATABASE o ALTER DATABASE per specificare regole di confronto predefinite del database. Se non viene specificata alcuna regola di confronto, al database vengono assegnate le regole di confronto del server.    
    
Non è possibile modificare le regole di confronto del database di sistema se non modificandole per il server.    
    
Le regole di confronto del database vengono usate per tutti i metadati nel database e rappresentano l'impostazione predefinita per tutte le colonne stringa, gli oggetti temporanei, i nomi di variabili e qualsiasi altra stringa usata nel database. Quando le regole di confronto di un database utente vengono modificate, è possibile che si verifichino conflitti tra le regole di confronto quando vengono eseguite query nelle tabelle temporanee di accesso al database. Le tabelle temporanee sono sempre archiviate nel database di sistema **tempdb**, che usa le regole di confronto per l'istanza. L'esecuzione di query di confronto dei dati di tipo carattere tra database utente e **tempdb** può non riuscire se le regole di confronto causano un conflitto nella valutazione dei dati di tipo carattere. È possibile risolvere il problema specificando la clausola COLLATE nella query. Per altre informazioni, vedere [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).    
    
#### <a name="column-level-collations"></a>Regole di confronto a livello di colonna    
Quando una tabella viene creata o modificata, è possibile specificare regole di confronto per ciascuna colonna di stringhe di caratteri utilizzando la clausola COLLATE. Se non si specificano regole di confronto, alla colonna verranno assegnate le regole di confronto predefinite del database.    
    
#### <a name="expression-level-collations"></a>Regole di confronto a livello di espressione    
Le regole di confronto a livello di espressione vengono impostate al momento dell'esecuzione di un'istruzione e interessano la modalità di restituzione di un set di risultati. In questo modo i risultati dell'ordinamento ORDER BY possono essere specifici delle impostazioni locali. Per implementare regole di confronto a livello di espressione, usare una clausola COLLATE simile alla seguente:    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> Impostazioni locali    
Le impostazioni locali rappresentano un set di informazioni associate a un paese o a una lingua. Possono includere il nome e l'identificatore della lingua parlata, lo script usato per la scrittura della lingua e le convenzioni culturali. Le regole di confronto possono essere associate a uno o più set di impostazioni locali. Per altre informazioni, vedere [ID delle impostazioni locali assegnati da Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).    
    
###  <a name="Code_Page_Defn"></a> Code Page    
 Una tabella codici è un set ordinato di caratteri di uno script specifico nel quale a ogni carattere viene associato un indice numerico o un valore punto di codice. Per tabella codici di Windows si intende in genere un *set di caratteri* o *charset*. Queste tabelle vengono usate per supportare i set di caratteri e i layout di tastiera impiegati per le diverse impostazioni locali di Windows.     
###  <a name="Sort_Order_Defn"></a> Sort Order    
 L'ordinamento specifica il modo in cui vengono ordinati i valori dei dati. e influisce sui risultati del confronto dei dati stessi. I dati vengono ordinati tramite regole di confronto e possono essere ottimizzati tramite indici.    
    
##  <a name="Unicode_Defn"></a> Supporto Unicode    
Unicode è uno standard per il mapping dei punti di codice ai caratteri. Dato che è progettato per supportare tutti i caratteri di tutte le lingue del mondo, non è necessario che set di caratteri diversi vengano gestiti da tabelle codici diverse. Se vengono archiviati dati di tipo carattere che riflettono più lingue in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), usare tipi di dati Unicode (UTF-16) (**nchar**, **nvarchar** e **ntext**) anziché tipi di dati non Unicode (**char**, **varchar** e **text**). In alternativa, a partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], se si usano regole di confronto abilitate per UTF-8 (\_UTF8), i tipi di dati in precedenza non Unicode (**char** e **varchar**) diventano tipi di dati Unicode (UTF-8). 

> [!NOTE]
> [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] non modifica il comportamento dei tipi di dati Unicode (UTF-16) esistenti in precedenza (**nchar**, **nvarchar** e **ntext**).   
    
Ai tipi di dati non Unicode sono associate numerose limitazioni, perché nei computer non Unicode è disponibile una sola tabella codici. Utilizzando tipi di dati Unicode è possibile ottenere prestazioni migliori, in quanto è necessario un minor numero di conversioni tramite la tabella codici. Le regole di confronto Unicode devono essere selezionate singolarmente a livello di database, di colonna o di espressione perché non sono supportate a livello di server.    
    
Le tabelle codici usate da un client vengono determinate in base alle impostazioni del sistema operativo. Per impostare le tabelle codici del client nel sistema operativo Windows usare l'opzione **Impostazioni internazionali** del Pannello di controllo.    
    
Quando si spostano dati da un server a un client, le regole di confronto del server potrebbero non essere riconosciute dai driver client meno recenti. Questa situazione può verificarsi quando si spostano dati da un server Unicode a un client non Unicode. La migliore opzione potrebbe consistere nell'aggiornare il sistema operativo client affinché vengano aggiornate le regole di confronto del sistema sottostanti. Se nel client è installato il software client del database, è possibile applicare un aggiornamento dei servizi a tale software.    
    
È anche possibile tentare di usare regole di confronto diverse per i dati nel server. Scegliere regole di confronto con mapping a una tabella codici nel client.    
    
Per usare le regole di confronto UTF-16 disponibili in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e migliorare la ricerca e l'ordinamento di alcuni caratteri Unicode (solo regole di confronto Windows), è possibile selezionare una delle regole di confronto dei caratteri supplementari (\_SC) o una delle regole di confronto versione 140.    
 
Per usare le regole di confronto UTF-8 disponibili in [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e migliorare la ricerca e l'ordinamento di alcuni caratteri Unicode (solo regole di confronto Windows), è necessario selezionare regole di confronto abilitate per la codifica UTF-8 (\_UTF8).
 
-   Il flag UTF8 può essere applicato a:    
   
    -   Regole di confronto versione 90 
    
        > [!NOTE]
        > Solo quando esistono già regole di confronto che riconoscono i caratteri supplementari (\_SC) o con distinzione tra selettori di variazione (\_VSS) in questa versione.
    
    -   Regole di confronto versione 100    
    
    -   Regole di confronto versione 140   
    
    -   Regole di confronto BIN2<sup>1</sup>
    
-   Il flag UTF8 non può essere applicato a:    
    
    -   Regole di confronto versione 90 che non supportano caratteri supplementari (\_SC) o con distinzione tra selettori di variazione (\_VSS)    
    
    -   Regole di confronto binarie BIN o BIN2<sup>2</sup>    
    
    -   Regole di confronto di SQL \*  
    
<sup>1</sup> A partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3     
<sup>2</sup> Fino a [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3
    
Per valutare i problemi relativi all'utilizzo di tipi di dati Unicode o non Unicode, è necessario eseguire il test dello scenario per verificare le differenze di prestazioni nell'ambiente specifico. È consigliabile standardizzare le regole di confronto usate nei sistemi presenti nell'ambito dell'organizzazione, quindi distribuire server e client Unicode laddove possibile.    
    
In molti casi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interagisce con altri server o client e l'organizzazione può usare più standard di accesso ai dati tra applicazioni e istanze del server. I client[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono principalmente di due tipi:    
    
-   **Client Unicode** che usano OLE DB e ODBC (Open Database Connectivity) versione 3.7 o successive.    
    
-   **Client non Unicode** che usano DB-Library e ODBC versione 3.6 o precedenti.    
    
Nella tabella seguente sono riportate informazioni sull'utilizzo di dati multilingue con diverse combinazioni di server Unicode e non Unicode.    
    
|Server|Client|Vantaggi o limitazioni|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|Visto che i dati Unicode vengono usati in tutto il sistema, questo scenario offre prestazioni ottimali e la migliore protezione da eventuali danni ai dati recuperati. Si applica ad ADO (ActiveX Data Objects), OLE DB e ODBC versione 3.7 o successive.|    
|Unicode|Non Unicode|In questo scenario, in particolare con le connessioni tra un server in cui è in esecuzione un sistema operativo più recente e un client in cui è in esecuzione una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o di un sistema operativo, possono riscontrarsi limitazioni o errori quando si spostano i dati in un computer client. Per convertire i dati si tenta il mapping tra i dati Unicode presenti nel server e una tabella codici corrispondente nel client non Unicode.|    
|Non Unicode|Unicode|Non si tratta di una configurazione ideale per l'utilizzo di dati multilingue. Non sarà possibile scrivere dati Unicode nel server non Unicode e potrebbero verificarsi problemi all'invio dei dati ai server che non rientrano nella tabella codici del server.|    
|Non Unicode|Non Unicode|Si tratta di uno scenario che presenta numerose limitazioni per i dati multilingue. È possibile usare solo una tabella codici.|    
    
##  <a name="Supplementary_Characters"></a> Caratteri supplementari    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce tipi di dati, come **nchar** e **nvarchar**, per archiviare dati Unicode (UTF-16) in tutte le regole di confronto e tipi di dati, come **char** e **varchar** per archiviare dati Unicode (UTF-8) in regole di confronto abilitate per UTF-8 (\_UTF8). Questi tipi di dati codificano il testo in un formato denominato rispettivamente *UTF-16* e *UTF-8*. L'Unicode Consortium assegna a ogni carattere un punto di codice univoco, che corrisponde a un valore nell'intervallo compreso tra 0x0000 e 0x10FFFF. I caratteri usati più di frequente sono associati a valori di punti di codice compresi in una parola a 8 bit o a 16 bit in memoria e su disco, mentre i caratteri con valori di punti di codice maggiori di 0xFFFF richiedono da due a quattro parole a 8 bit consecutive (UTF-8) oppure due parole a 16 bit consecutive (UTF-16). Questi caratteri sono denominati *caratteri supplementari* e le parole a 8 bit o a 16 bit consecutive aggiuntive sono denominate *coppie di surrogati*.    
    
A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è possibile usare una nuova famiglia di regole di confronto per caratteri supplementari (\_SC) con i tipi di dati **nchar**, **nvarchar** e **sql_variant**. Ad esempio: `Latin1_General_100_CI_AS_SC`o, se si utilizzano regole di confronto giapponesi, `Japanese_Bushu_Kakusu_100_CI_AS_SC`. 
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] estende il supporto dei caratteri supplementari ai tipi di dati **char** e **varchar** con le nuove regole di confronto abilitate per UTF-8 (\_UTF8).   

A partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tutte le nuove regole di confronto supportano automaticamente i caratteri supplementari.

Se si utilizzano caratteri supplementari:    
    
-   I caratteri supplementari possono essere usati in operazioni di ordinamento e confronto solo con le versioni delle regole di confronto 90 o successive.    
    
-   Tutte le regole di confronto versione 100 supportano l'ordinamento linguistico con caratteri supplementari.    
    
-   L'utilizzo dei caratteri supplementari in metadati, ad esempio in nomi di oggetti di database, non è supportato.    
    
-   I database che usano le regole di confronto con caratteri supplementari (\_SC) non possono essere abilitati per la replica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo perché alcune delle tabelle di sistema e delle stored procedure create per la replica usano il tipo di dati legacy **ntext**, che non supporta i caratteri supplementari.  
    
-   Il flag SC può essere applicato a:    
    
    -   Regole di confronto versione 90    
    
    -   Regole di confronto versione 100    
    
-   Il flag SC non può essere applicato a:    
    
    -   Regole di confronto di Windows senza versione, versione 80    
    
    -   Regole di confronto binarie BIN o BIN2    
    
    -   Regole di confronto di SQL \*    
    
    -   Regole di confronto versione 140. Non devono necessariamente avere il flag SC perché supportano già i caratteri supplementari    
    
Nella tabella seguente viene confrontato il comportamento di alcune funzioni per i valori stringa e di alcuni operatori di stringa quando vengono usati caratteri supplementari con e senza regole di confronto che supportano caratteri complementari:    
    
|Funzione per i valori stringa o operatore di stringa|Con regole di confronto che supportano caratteri complementari|Senza regole di confronto che supportano caratteri complementari|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|La coppia di surrogati UTF-16 viene conteggiata come singolo punto di codice.|La coppia di surrogati UTF-16 viene conteggiata come due punti di codice.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|Queste funzioni considerano ogni coppia di surrogati un singolo punto di codice e funzionano come previsto.|Queste funzioni possono dividere qualsiasi coppia di surrogati e provocare risultati imprevisti.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|Restituisce il carattere corrispondente al valore del punto di codice Unicode specificato nell'intervallo compreso tra 0 e 0x10FFFF. Se il valore specificato è incluso nell'intervallo compreso tra 0 e 0xFFFF, viene restituito un carattere. Per valori superiori, viene restituito il surrogato corrispondente.|Un valore maggiore di 0xFFFF restituisce NULL anziché il surrogato corrispondente.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|Restituisce un punto di codice UTF-16 nell'intervallo compreso tra 0 e 0x10FFFF.|Restituisce un punto di codice UCS-2 nell'intervallo compreso tra 0 e 0xFFFF.|    
|[Carattere jolly per corrispondenze di singoli caratteri](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [Carattere jolly per la mancata corrispondenza dei caratteri](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|Sono supportati caratteri supplementari per tutte le operazioni con caratteri jolly.|Non sono supportati caratteri supplementari per queste operazioni con caratteri jolly. Sono supportati altri operatori jolly.|    
    
##  <a name="GB18030"></a> Supporto GB18030    
 GB18030 è uno standard separato usato nella Repubblica popolare Cinese per la codifica dei caratteri cinesi. In GB18030, i caratteri possono essere di 1, 2 o 4 byte di lunghezza. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre supporto per i caratteri con codifica GB18030 consentendone il riconoscimento al momento dell'ingresso nel server da un'applicazione client e la conversione e archiviazione come caratteri Unicode a livello nativo. Dopo essere stati archiviati nel server, tali caratteri vengono trattati come caratteri Unicode in tutte le operazioni successive. È possibile usare una qualsiasi regola di confronto cinese, preferibilmente la versione 100 più recente. Tutte le regole di confronto di livello _100 supportano l'ordinamento linguistico con caratteri GB18030. Se nei dati sono inclusi caratteri supplementari (coppie surrogate), è possibile usare le regole di confronto SC in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per migliorare la ricerca e l'ordinamento.    
    
##  <a name="Complex_script"></a> Supporto di lingue con alfabeti non latini    
 In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere supportata l'immissione, l'archiviazione, la modifica e la visualizzazione di lingue con alfabeti non latini. Le lingue con alfabeti non latini includono i siti seguenti:    
    
-   Lingue che presentano una combinazione di testo scritto sia da destra verso sinistra sia da sinistra verso destra, ad esempio una combinazione di testo in arabo e inglese.    
-   Lingue i cui caratteri assumono una forma diversa a seconda della posizione oppure combinati con altri caratteri, ad esempio arabi, indiani e thai.    
-   Lingue come il thai che richiedono dizionari interni per il riconoscimento delle parole in quanto non vi sono interruzioni tra di loro.    
    
Le applicazioni di database che interagiscono con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono usare controlli che supportano le lingue con alfabeti non latini. I form standard di Windows creati in codice gestito sono abilitati per le lingue con alfabeti non latini.    

##  <a name="Japanese_Collations"></a> aggiunte in  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
A partire da [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] sono supportate nuove famiglie di regole di confronto per il giapponese, con permutazioni di varie opzioni (\_CS, \_AS, \_KS, \_WS, \_VSS). 

Per elencare queste regole di confronto, è possibile eseguire una query nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

Tutte le nuove regole di confronto supportano in modo predefinito i caratteri supplementari. Per nessuna nuova regola di confronto esiste o è necessario il flag SC.

Queste regole di confronto sono supportate negli indici del motore di database, nelle tabelle ottimizzate per la memoria, negli indici columnstore e nei moduli compilati in modo nativo.

<a name="ctp23"></a>

## <a name="utf-8-support"></a>Supporto UTF-8

In [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] viene introdotto il supporto completo per la codifica dei caratteri di grande diffusione UTF-8 come codifica di importazione o esportazione o come regola di confronto di livello database o colonna per i dati di testo. La codifica UTF-8 è consentita nei tipi di dati `CHAR` e `VARCHAR` ed è abilitata quando si crea o si modifica la regola di confronto di un oggetto convertendola in una regola di confronto con il suffisso `UTF8`. 

Ad esempio da `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 è disponibile solo per le regole di confronto di Windows che supportano i caratteri supplementari. Questa funzionalità è stata introdotta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` consentono solo la codifica UTF-16 e rimangono invariati.

A seconda del set di caratteri in uso, questa funzionalità può offrire importanti risparmi di risorse di archiviazione. Se ad esempio si cambia il tipo di dati di una colonna esistente con stringhe ASCII (Latin) da `NCHAR(10)` in `CHAR(10)` usando una regola di confronto con supporto UTF-8, i requisiti di archiviazione vengono ridotti del 50%. Questa riduzione deriva dal fatto che `NCHAR(10)` richiede 20 byte per l'archiviazione, mentre `CHAR(10)` richiede solo 10 byte per la stessa stringa Unicode.

##  <a name="Related_Tasks"></a> Attività correlate    
    
|Attività|Argomento|    
|----------|-----------|    
|Viene descritto come impostare o modificare le regole di confronto dell'istanza di SQL Server.|[Impostazione o modifica di regole di confronto del server](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|Viene descritto come impostare o modificare le regole di confronto di un database utente.|[Impostare o modificare le regole di confronto del database](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|Viene descritto come impostare o modificare le regole di confronto di una colonna nel database.|[Impostare o modificare le regole di confronto delle colonne](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|Viene descritto come restituire informazioni sulle regole di confronto a livello di server, di database o di colonna.|[Visualizzazione di informazioni sulle regole di confronto](../../relational-databases/collations/view-collation-information.md)|    
|Viene descritto come scrivere istruzioni Transact-SQL più portabili da un linguaggio a un altro o supportano più linguaggi con maggiore facilità.|[Scrittura di istruzioni Transact-SQL internazionali](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|Viene descritto come modificare la lingua dei messaggi di errore e le preferenze di utilizzo e visualizzazione dei dati di tipo data, ora e valuta.|[Impostazione di una lingua di sessione](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> Contenuto correlato    
[SQL Server Best Practices Collation Change](https://go.microsoft.com/fwlink/?LinkId=113891)   (Procedure consigliate di SQL Server: modifica delle regole di confronto)  
[Usare il formato carattere Unicode per importare o esportare dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)        
[Scrittura di istruzioni Transact-SQL internazionali](../../relational-databases/collations/write-international-transact-sql-statements.md)     
[SQL Server Best Practices Migration to Unicode](https://go.microsoft.com/fwlink/?LinkId=113890) (Procedure consigliate di SQL Server: migrazione a Unicode) - non più aggiornato   
[Sito Web Unicode Consortium](https://go.microsoft.com/fwlink/?LinkId=48619)    
    
## <a name="see-also"></a>Vedere anche    
[Regole di confronto dei database indipendenti](../../relational-databases/databases/contained-database-collations.md)     
[Scelta di una lingua durante la creazione di un indice full-text](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)    
    
 
