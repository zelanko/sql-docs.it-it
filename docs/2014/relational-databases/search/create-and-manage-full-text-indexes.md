---
title: Creare e gestire indici full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a41f11b200ffe5dfc91479ea54095fd24c90699a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011551"
---
# <a name="create-and-manage-full-text-indexes"></a>Creazione e gestione di indici full-text
  Le informazioni contenute negli indici full-text vengono utilizzate dal motore di ricerca full-text per compilare query full-text che consentono di cercare rapidamente parole o combinazioni di parole specifiche in una tabella. In un indice full-text vengono archiviate informazioni su parole significative e sulla relativa posizione all'interno di una o più colonne di una tabella di database. Un indice full-text è un tipo speciale di indice funzionale basato su token compilato e gestito dal motore di ricerca full-text per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il processo di compilazione di un indice full-text è diverso da quello di altri tipi di indici. Anziché creare un albero B basato su un valore archiviato in una riga specifica, il motore di ricerca full-text compila una struttura con indice invertito, compresso e in pila dai singoli token dal testo indicizzato.  Le dimensioni di un indice full-text sono limitate solo dalle risorse di memoria disponibili del computer in cui viene eseguita l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]gli indici full-text sono integrati nel Motore di database anziché risiedere nel file system come nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un nuovo database, il catalogo full-text è ora un oggetto virtuale che non appartiene ad alcun filegroup. Si tratta semplicemente di un concetto logico che fa riferimento a un gruppo di indici full-text. Si noti tuttavia che durante l'aggiornamento di un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , ovvero qualsiasi catalogo full-text contenente file di dati, viene creato un nuovo filegroup. Per altre informazioni, vedere [Aggiornamento della ricerca full-text](upgrade-full-text-search.md).  
  
> [!NOTE]  
>  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, il motore di ricerca full-text si trova nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anziché in un servizio distinto. L'integrazione del motore di ricerca full-text nel Motore di database consente di ottimizzare la gestibilità della ricerca full-text, l'esecuzione delle query miste e le prestazioni generali.  
  
 È consentito un solo indice full-text per tabella. Per creare un indice full-text su una tabella, quest'ultima deve contenere una colonna singola, univoca e non Null. È possibile compilare un indice full-text su colonne di tipo `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary` e `varbinary(max)` che possono essere indicizzate per la ricerca full-text. La creazione di un indice full-text in colonne con tipo di dati `varbinary`, `varbinary(max)`o `image` o `xml` richiede la specifica di una colonna del tipo. Una *colonna del tipo* è una colonna di tabella in cui è possibile archiviare l'estensione file (doc, pdf, xls e così via) del documento in ogni riga.  
  
 Il processo di creazione e gestione di un indice full-text è definito *popolamento* (noto anche come *ricerca per indicizzazione*). Sono disponibili tre tipi di popolamento dell'indice full-text: popolamento completo, popolamento basato sul rilevamento delle modifiche e popolamento incrementale basato su timestamp. Per altre informazioni sugli indici full-text, vedere [Popolamento degli indici full-text](populate-full-text-indexes.md).  
  
##  <a name="tasks"></a>Attività comuni  
 **Per creare un indice full-text**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **Per modificare un indice full-text**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **Per eliminare un indice full-text**  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
 [Contenuto dell'articolo](#top)  
  
##  <a name="structure"></a>Struttura dell'indice full-text  
 Comprendere a fondo la struttura di un indice full-text è fondamentale per comprendere il funzionamento del motore di ricerca full-text. In questo argomento viene usato come esempio l'estratto seguente della tabella **Document** in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] . In questo estratto sono visualizzate solo due colonne, la colonna **DocumentID** e la colonna **Title** , e tre righe della tabella.  
  
 In questo esempio si suppone che nella colonna **Title** sia stato creato un indice full-text.  
  
|DocumentID|Titolo|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 Nella tabella seguente, Fragment 1, viene illustrato il contenuto dell'indice full-text creato nella colonna **Title** della tabella **Document** . Gli indici full-text contengono più informazioni rispetto a quelle riportate in questa tabella. La tabella è una rappresentazione logica di un indice full-text e ha solo scopo illustrativo. Per ottimizzare l'utilizzo del disco, le righe vengono archiviate in un formato compresso.  
  
 Si noti che i dati sono stati invertiti dai documenti originali. Questa inversione è dovuta al fatto che per le parole chiave viene eseguito il mapping agli ID documento. Per questo motivo, un indice full-text viene spesso definito come un indice invertito.  
  
 Si noti inoltre che la parola chiave "and" è stata rimossa dall'indice full-text, trattandosi di una parola non significativa, e che la rimozione di tali parole da un indice full-text può contribuire a risparmiare spazio su disco, migliorando di conseguenza le prestazioni delle query. Per altre informazioni sulle parole non significative e sugli elenchi di parole non significative, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 **Frammento 1**  
  
|Parola chiave|ColId|DocId|Occorrenza|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Manutenzione |1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
|Installazione|1|3|4|  
  
 La colonna **Parola chiave** contiene la rappresentazione di un singolo token estratto al momento dell'indicizzazione. I word breaker stabiliscono il modo in cui un token viene determinato.  
  
 La colonna **ColId** contiene un valore che corrisponde a una particolare colonna con indicizzazione full-text.  
  
 La `DocId` colonna contiene valori per un numero intero a otto byte che esegue il mapping a un particolare valore della chiave full-text in una tabella con indicizzazione full-text. Questo mapping è necessario se la chiave full-text non è un tipo di dati integer. In questi casi, i mapping tra i valori e `DocId` i valori della chiave full-text vengono mantenuti in una tabella separata denominata tabella di mapping docid. Per eseguire una query per questi mapping usare la stored procedure di sistema [sp_fulltext_keymappings](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql) . Per soddisfare una condizione di ricerca, è necessario creare un join tra i valori DocId della tabella precedente e la tabella DocId Mapping per recuperare le righe dalla tabella di base su cui viene eseguita la query. Se il valore della chiave full-text della tabella di base è di tipo integer, il valore viene utilizzato direttamente come DocId e non è necessario alcun mapping. Pertanto, l'utilizzo di valori chiave full-text di tipo integer può contribuire all'ottimizzazione delle query full-text.  
  
 La colonna **Occurrence** contiene un valore di tipo integer. Per ogni valore DocId è presente un elenco di valori di occorrenza corrispondenti agli offset relativi di una particolare parola chiave all'interno di DocId. I valori di occorrenza sono utili per determinare le corrispondenze di frase o prossimità, ad esempio frasi con valori di occorrenza numericamente adiacenti. Sono inoltre utili per calcolare i punteggi di pertinenza, ad esempio il numero di occorrenze di una parola chiave in un DocId può essere utilizzato per l'assegnazione del punteggio.  
  
 [Contenuto dell'articolo](#top)  
  
##  <a name="fragments"></a>Frammenti di indice full-text  
 L'indice full-text logico viene in genere suddiviso tra più tabelle interne. Ogni tabella interna viene definita un frammento di indice full-text. Alcuni di questi frammenti potrebbero contenere dati più recenti di altri. Ad esempio, se un utente aggiorna la riga seguente il cui DocId è 3 e per la tabella è impostato il rilevamento automatico delle modifiche, viene creato un nuovo frammento.  
  
|DocumentID|Titolo|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 Nell'esempio seguente, Fragment 2, il frammento contiene dati più recenti su DocId 3, rispetto a Fragment 1. Pertanto, quando viene eseguita una query per "Rear Reflector" i dati di Fragment 2 vengono utilizzati per DocId 3. Ogni frammento viene contrassegnato con un timestamp di creazione su cui è possibile eseguire query tramite la vista del catalogo [sys.fulltext_index_fragments](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql) .  
  
 **Frammento 2**  
  
|Parola chiave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 Come si può vedere da Fragment 2, le query full-text devono essere eseguite internamente su ogni frammento e le voci più obsolete devono essere eliminate. Un numero eccessivo di frammenti di indice full-text nell'indice full-text può causare un calo sensibile delle prestazioni di esecuzione delle query. Per ridurre il numero di frammenti, riorganizzare il catalogo full-text utilizzando l'opzione REORGANIZE dell'istruzione [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql) [!INCLUDE[tsql](../../includes/tsql-md.md)] . Questa istruzione consente di eseguire un' *unione nell'indice master*, ovvero un'unione dei frammenti in un singolo frammento più grande e la rimozione di tutte le voci obsolete dall'indice full-text.  
  
 Dopo essere stato riorganizzato, l'indice di esempio dovrebbe contenere le righe seguenti:  
  
|Parola chiave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Manutenzione |1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
  
 [Contenuto dell'articolo](#top)  
  
  
