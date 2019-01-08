---
title: I termini del Glossario ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c02447379b713a7d3b1c6dd72af8c3860098a68c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52528022"
---
# <a name="ado-glossary-terms"></a>Termini del Glossario ADO
In questo argomento definisce termini rilevanti per ADO.

## <a name="a"></a>A
 Un URL completo URL assoluto che specifica il percorso di una risorsa che si trova su Internet o intranet. Vedere anche *URL* e *URL relativo*.

 Registrazione automatica, in-process componente COM che spesso ha un elemento visivo in fase di progettazione o di esecuzione del controllo ActiveX. Controlli ActiveX sono inoltre in grado di comunicare con un contenitore di documenti attivi, ad esempio Microsoft Internet Explorer.

 ADISAPI (avanzata dei dati Internet Server Application Programming Interface) di DLL ISAPI che fornisce l'analisi, controllo di automazione, il marshalling di Recordset e creazione del pacchetto MIME. Il componente ADISAPI funziona tramite l'API fornita da Internet Information Services (IIS). Vedere anche *ISAPI*.

 funzione di aggregazione In una query, una funzione, ad esempio COUNT, AVG o STDEV che consente di calcolare un valore usando tutte le righe in una colonna di una tabella. Nella scrittura di espressioni e nella programmazione, è possibile utilizzare le funzioni di aggregazione SQL (inclusi i tre elencati in precedenza) e funzioni di aggregazione sui domini per determinare le statistiche diverse.

 alias un nome alternativo è assegnato a una colonna o espressione in un'istruzione SQL SELECT, spesso più breve o più significativa. Ad esempio, BobSales è l'alias dell'istruzione SELECT seguente: "Selezionare wr Sales come BobSales da SalesDB". Un alias può essere utilizzato per assegnare dinamicamente le colonne per le associazioni del controllo sull'oggetto DataControl.

 threading apartment COM di un modello di threading in cui si verificano tutte le chiamate a un oggetto in un unico thread. Nel threading apartment COM Sincronizza ed effettua il marshalling di chiamate. Vedere anche *COMmddefcom*.

 operazione asincrona di un'operazione che restituisce il controllo al programma chiamante senza attendere il completamento dell'operazione. Prima che l'operazione è stata completata, continua l'esecuzione di codice. Vedere anche *operazione sincrona*.

## <a name="b"></a>B
 mapping di una voce di associazione di un campo in una tabella a una variabile. Nelle estensioni ADO di Visual C++, **Recordset** mapping dei campi per le variabili di C/C++.

 maschera di bit un valore numerico previsto per confrontare i valori di bit per bit con altri valori numerici, in genere per le opzioni di flag di parametri o valori restituiti. In genere questo confronto viene eseguito con gli operatori logici bit per bit, ad esempio **e** e **oppure** in Visual Basic **&** e **&#124;** in C++.

 Ad esempio, l'oggetto ADO **FieldAttributeEnum** valori possono essere usati come maschere di bit per determinare gli attributi di un campo. Si supponga di che voler determinare se un campo non è aggiornabile. È stato possibile effettuare questa verifica con l'espressione seguente in Visual Basic:`Field.Attributes AND adFldUpdatable`

 Se il risultato è TRUE, il campo è aggiornabile.

 aggiungere un segnalibro un indicatore che identifica in modo univoco una riga all'interno di un set di righe in modo che un utente può passare rapidamente a esso.

 oggetto business un oggetto che esegue un set definito di operazioni, ad esempio la convalida dei dati o logica della regola business. Gli oggetti business si trovano in genere nel livello intermedio.

 regola di business la combinazione di modifiche di convalida, verifiche di accesso, le ricerche nel database, i criteri e trasformazioni algoritmiche che costituiscono un'azienda di attività di business. Noto anche come *logica di business*.

## <a name="c"></a>c
 calcolato espressione un'espressione non costante, ma il cui valore dipende da altri valori. Per poter essere valutata, un'espressione calcolata necessario ottenere e calcolare i valori da altre origini, in genere in altri campi o righe.

 riferimento di capitolo oggetto a un intervallo di righe da un'origine dati. In ADO un capitolo viene in genere un riferimento a un'altra **Recordset**.

 Le colonne a capitoli consentono di definire un *padre-figlio* relazione in cui il *padre* è la **Recordset** contenente la colonna a capitoli e  *figlio* è il **Recordset** rappresentato dal capitolo.

 Un alias che fa riferimento alla colonna aggiunta al padre di capitolo-alias.

 Un mapping di un set di caratteri di set di caratteri per i relativi valori numerici. Ad esempio, Unicode è un carattere a 16 bit impostato in grado di codifica dei caratteri noti tutti e usato come uno standard di codifica dei caratteri in tutto il mondo.

 elemento figlio il lato dipendente di una relazione gerarchica. Un elemento figlio è un nodo in una struttura gerarchica che include un altro nodo sopra di esso (più vicino alla radice). Vedere anche *figlio-alias*, *relazione padre-figlio*, *padre*.

 alias-figlio un alias che fa riferimento all'elemento figlio. Vedere anche *alias*, *figlio*.

 CLSID (identificatore di classe) un identificatore univoco universale (UUID) che identifica un componente COM. Ogni componente COM ha valore CLSID corrispondente nel Registro di sistema Windows in modo che può essere caricato da altre applicazioni. Vedere anche *ProgID*, *COM*.

 livello logico di livello un client di un sistema distribuito che presenta in genere i dati ed elabora l'input da parte dell'utente, detta anche il *front-end*. In genere, il livello client richiede dati da un server in base all'input, quindi formatta e visualizza il risultato. Vedere anche *livello intermedio*, *livello di origine dati*, *un'applicazione distribuita*.

 COM (Component Object Model) A binario standard che consente agli oggetti di interoperabilità in un ambiente di rete indipendentemente dalla lingua in cui sono state sviluppate o nei computer che si trovino. Tecnologie basate su COM, includono i controlli ActiveX, automazione e il collegamento e incorporamento (OLE). Consente a un oggetto per esporne la funzionalità agli altri componenti e alle applicazioni host. Definisce come l'oggetto espone sé sia come questa esposizione funziona tra processi e tra reti. COM definisce anche il ciclo di vita dell'oggetto.

 File di componente binario COM - ad esempio con estensione dll, ocx e alcuni file .exe - che supporta lo standard di COM per fornire gli oggetti. Questo file contiene codice per uno o più class factory, le classi COM, voci di registro, il codice di caricamento e così via.

 operatore di confronto un operatore che confronta due espressioni e restituisce un valore booleano.

 Un parametro di criteri che può essere espresso come ">" (maggiore di), "\<" (minore di), "=" (uguale), "> =" (maggiore o uguale), "< =" (minore o uguale a), "<>" (non uguale), o "like" (criteri di ricerca).

 componente di un oggetto che incapsula i dati e codice e fornisce un set ben definito di servizi disponibili pubblicamente.

 file composto un'implementazione di COM strutturato archiviazione per i file. Un file composto Archivia oggetti separati in un file singolo, strutturato costituito da due elementi principali: gli oggetti di archiviazione e gli oggetti flusso. Insieme, il loro funzionamento, ad esempio un file system all'interno di un file.

 Un numero di file singoli associato insieme in un file fisico. Ogni singolo file in un file composto è accessibile come se fosse un unico file fisico.

 costante un valore numerico o stringa che non cambia. Enumerazioni di ADO denominate (costanti enumerate) utilizzabile nel codice anziché i valori effettivi, ad esempio, **adUseClient** è una costante il cui valore è 3. (Anche enumerazione = 3). Vedere anche *enumerazione*.

 cursore di un elemento di database che controlla la navigazione tra i record, aggiornabilità dei dati e la visibilità delle modifiche apportate al database da altri utenti.

## <a name="d"></a>D
 Il processo di associazione di oggetti o i controlli di un'applicazione a un'origine dati di associazione dati. Un controllo associato a un'origine dati viene chiamato un *controllo con associazione a dati*.

 Il contenuto di un controllo con associazione a dati è associato i valori da un database. Ad esempio, un controllo griglia associata a un **Recordset** oggetto può essere aggiornato quando le righe nel **Recordset** vengono aggiornati. Quando i nuovi valori vengono recuperati per il **Recordset**, nuovi valori vengono visualizzati nella griglia.

 provider di dati Software che espone i dati a un'applicazione ADO direttamente o tramite un provider di servizi. Vedere anche provider di servizi.

 data shaping di una tecnica che consente di Usa una sintassi formalizzata (chiamato **forma language**) per definire un specializzato **Recordset** oggetto (chiamato un *a forma di Recordset*) che contiene dati non solo, ma fa riferimento anche a loro **Recordset** oggetti e/o valori calcolati in base i loro **Recordset** oggetti.

 livello logico A livello di un sistema distribuito che rappresenta un computer che esegue un sistema DBMS, ad esempio un database di SQL Server dell'origine dati. Vedere anche *livello client*, *livello intermedio*, *un'applicazione distribuita*.

 Protocollo di transito A DCOM che consente ai componenti COM comunicare direttamente tra loro attraverso una rete. Vedere anche *COM*, *componente*.

 DDL (Data Definition Language) le istruzioni SQL che definiscono, in contrapposizione per manipolare i dati. Lo schema di un database viene creato o modificato tramite il linguaggio DDL. Ad esempio, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **revocare** sono istruzioni SQL DDL.

 Un flusso di testo o binario di flusso predefinito (rappresentato da un **Stream** oggetto) associato al **Record** o **Recordset** oggetti quando si utilizza provider OLE DB specifici, ad esempio il Provider Microsoft OLE DB per Internet Publishing. Il flusso predefinito include in genere il contenuto di un file, ad esempio il codice HTML per la radice di un sito Web.

 programma l'applicazione distribuita A scritto in modo che l'elaborazione può essere suddivise tra più computer in rete. In genere, un'applicazione distribuita è suddiviso in presentazione, logica di business e dati livelli di archivio, o *livelli*. Vedere anche il livello client, livello intermedio, livello di origine dati.

 disconnesso A Recordset **Recordset** oggetto in una cache client che non ha più una connessione in tempo reale al server. Se l'origine dati originale deve accedere nuovamente per qualche motivo, ad esempio l'aggiornamento dei dati, la connessione deve essere ristabilita. Tuttavia, le raccolte, proprietà e metodi di un disconnessa **Recordset** rimangono comunque accessibili.

 DML (Data Manipulation Language) tali istruzioni SQL che modificano, anziché per definire, i dati. I valori in un database siano selezionati e modificati con DML. Ad esempio, **inserire**, **UPDATE**, **Elimina**, e **selezionare** sono istruzioni DML SQL.

 provider dell'origine documento una speciale classe di provider che gestiscono le cartelle e documenti. Quando un documento è rappresentato da un **Record** oggetto o una cartella dei documenti è rappresentato da un **Recordset** dell'oggetto, il provider di origine del documento consente di popolare gli oggetti con un set univoco di campi che Descrive le caratteristiche del documento, anziché il documento vero e proprio. Vedere anche record di risorse.

 DSN (DSN) la raccolta di informazioni utilizzata per connettere l'applicazione a un database ODBC specifico. Gestione Driver ODBC Usa queste informazioni per creare una connessione al database. Un DSN può essere archiviato in un file (DSN su file) o nel Registro di sistema Windows (DSN computer).

 proprietà dinamiche A proprietà specifiche di un provider di dati o il servizio di cursore. Il **proprietà** raccolta di un oggetto viene popolato automaticamente con queste ("dinamico"). Un oggetto non dispone di alcuna proprietà dinamica fino a quando non è connesso a un'origine dati tramite un provider di dati specifico. Vedere anche i dati provider, cursore.

## <a name="e"></a>E
 Elenco di un'enumerazione di costanti denominate. I valori enumerati non devono essere univoci. Tuttavia il nome di ogni valore deve essere univoco all'interno dell'ambito in cui è definita l'enumerazione. In ADO, le enumerazioni vengono usate per il parametro numerico e restituiscono valori, aggiungere un significato al codice ADO e proteggere allo sviluppatore di valori numerici (che possono cambiare da una versione a altra). Ad esempio, per aprire un valore statico **Recordset**, utilizzare il **adOpenStatic** valore enumerato: `Recordset.Open ,,adOpenStatic`

 Detta anche *costante enumerata*. Vedere anche *costante*.

 evento un'azione che viene riconosciuta da un oggetto, per cui è possibile scrivere codice per rispondere. Gli eventi possono essere generati dall'esecuzione del comando, il completamento delle transazioni, navigazione del recordset e gli aggiornamenti dei dati, tra le altre azioni. Vedere anche *gestore dell'evento*.

 gestore eventi un gestore eventi è il codice che viene eseguito quando si verifica un evento. Vedere anche l'evento.

## <a name="h"></a>H
 routine del gestore oggetto che gestisce una condizione comune e relativamente semplice o operazione, ad esempio gestione degli errori di ripristino o i dati.

 A Recordset gerarchici **Recordset** che contiene l'altra **Recordset**. Vedere anche data shaping, capitolo.

 Per altre informazioni, vedere [accesso alle righe in un Recordset gerarchico](../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).

 gerarchia In generale, una gerarchia è una struttura di pertinenza maggiore con un alto livello e livelli subordinati. In ADO, gerarchica **recordset** vengono usati per rappresentare la relazione padre-figlio tra un record e un capitolo. Anche in ADO **Record** e **Stream** gli oggetti possono essere utilizzati per accedere a strutture ad albero gerarchica, ad esempio documenti e una cartella. Include anche ADO MD **gerarchia** oggetti per rappresentare una relazione tra i livelli di una dimensione in un cubo OLAP. Vedere anche recordset gerarchici, relazione padre-figlio, capitolo, struttura ad albero.

## <a name="i-l"></a>I-L
 Set ISAPI (Internet Server Application Programming Interface) di funzioni per i server Internet, ad esempio un Server Windows NT® Server o Windows 2000 in esecuzione Microsoft® Internet Information Services (IIS).

 Chiave di una o più colonne in una tabella che identificano in modo univoco una riga. spesso usati per indicizzare una tabella.

## <a name="m"></a>M
 Il processo di creazione di pacchetti, l'invio e disassemblaggio parametri del metodo dell'interfaccia di marshalling attraverso i limiti di thread o processo.

 Il livello logico in un sistema distribuito tra un'interfaccia utente o client Web e il database di livello intermedio. Si tratta in genere in cui vengono create istanze degli oggetti business. Il livello intermedio è una raccolta di regole di business e le funzioni che generano e operano al momento della ricezione di informazioni. Per ottenere questo risultato tramite regole business che possono cambiare di frequente e pertanto vengono incapsulate in componenti che sono fisicamente separati dalla logica dell'applicazione stessa. Noto anche come *livello del server applicazioni*. Vedere anche applicazioni distribuite, livello client, livello di origine dati.

 MIME (estensione di posta elettronica Internet multiuso) An Internet protocol originariamente sviluppato per consentire lo scambio di messaggi di posta elettronica con contenuto avanzato tra ambienti di posta elettronica, macchina e rete eterogenea. In pratica, MIME è anche stato adottato ed esteso da applicazioni non di posta elettronica.

 MIME è uno standard che consente di essere pubblicate e leggere in Internet i dati binari. L'intestazione di un file con dati binari contiene il tipo MIME dei dati. informa i programmi client (browser Web e pacchetti di posta elettronica, ad esempio) che dovranno gestire i dati in modo diverso rispetto a testo normale. Ad esempio, l'intestazione di un documento Web che contiene un'immagine JPEG contiene il tipo MIME specifico nel formato file JPEG. In questo modo un browser visualizzare il file con il relativo visualizzatore JPEG, se presente.

## <a name="n-o"></a>N-O
 nodo di un elemento in una struttura ad albero gerarchica. Un nodo può essere la radice o figlio di un altro nodo. Un nodo può anche essere l'elemento padre di più figli. Vedere anche alla gerarchia, struttura ad albero, root, figlio, padre.

 variabile di una variabile oggetto che contiene un riferimento a un oggetto. Ad esempio, `objCustomObject` è una variabile che punta a un oggetto di tipo OggettoPersonalizzato:`Set objCustomObject = CreateObject(adodb.Recordset)`

 ODBC (Open Database Connectivity) un'interfaccia di linguaggio di programmazione standard usato per connettersi a un'ampia gamma di origini dati. Questo è generalmente possibile accedervi tramite Pannello di controllo, in cui i nomi delle origini dati (DSN) possono essere assegnati a usare i driver ODBC specifici.

 OLE DB A set di interfacce che espongono i dati da un'ampia gamma di origini tramite COM. Le interfacce OLE DB di offrono applicazioni con accesso uniforme ai dati archiviati in diverse origini dati. Queste interfacce supportano la quantità di funzionalità DBMS appropriato per l'origine dati, in modo da poter condividere i propri dati. Vedere anche COM.

 ottimistica il blocco di un tipo di blocco in cui la pagina di dati che contiene uno o più record, tra cui il record viene modificato, è più disponibile per altri utenti solo quando il record viene aggiornato mediante la **Update** (metodo), ma è disponibile prima e dopo la chiamata a **Update**.

 Blocco ottimistico viene usato quando le **Recordset** apertura dell'oggetto con il **LockType** parametro o una proprietà impostata su **adLockOptimistic** o  **adLockBatchOptimistic**. Vedere anche il blocco pessimistico.

 valore ordinale la posizione numerica di un elemento all'interno di un ordine. In una raccolta di ADO, il valore ordinale del primo elemento è zero (0). L'elemento successivo è uno (1) e così via.

## <a name="p"></a>P
 query di oggetto comando con parametri o un comando che consente di impostare i valori dei parametri prima dell'esecuzione del comando. Ad esempio, una stringa SQL può essere parametrizzata incorporando i marcatori di parametro nella stringa SQL (definito dal '?' caratteri). Quindi, l'applicazione specifica i valori per ogni parametro ed esegue il comando.

 Il controllo lato di una relazione gerarchica padre. In una struttura gerarchica, un elemento padre ha uno o più nodi figlio direttamente sotto di esso nella gerarchia. Vedere anche alias padre, figlio e relazione padre-figlio.

 alias-padre un alias che fa riferimento all'elemento padre. Vedere anche alias, elemento padre.

 relazione di una relazione padre-figlio in una struttura gerarchica in cui l'elemento padre è un livello superiore e direttamente associato a uno o più figli. Un elemento figlio è a un livello inferiore e deve avere un elemento padre. Vedere anche l'elemento padre, figlio.

 tipo di blocco in cui il blocco pessimistico della pagina che contiene uno o più record, tra cui il record viene modificato, non è disponibile ad altri utenti per garantire che un aggiornamento verrà eseguito. Comportamento di blocco pessimistico è definito dal provider OLE DB. In genere, i record sono bloccati durante la modifica e rimangono disponibili finché il **Update** metodo è stata completata.

 Il blocco pessimistico è abilitato quando la **Recordset** apertura dell'oggetto con il **LockType** parametro o una proprietà impostata su **adLockPessimistic**. Vedere anche il blocco ottimistico.

 il pool di ottimizzazione delle prestazioni basata sull'uso di raccolte di pre-allocare risorse, ad esempio gli oggetti o le connessioni al database. È più efficiente per disegnare una risorsa esistente dal pool di piuttosto che creare una nuova risorsa.

 Identificatore programmatico (ProgID) un nome univoco mappato nel Registro di sistema di Windows da un'applicazione COM. Il ProgID di una connessione ADO è "ADODB. Connessione". Vedere anche CLSID e COM.

 proxy di un oggetto specifico dell'interfaccia che fornisce il marshalling dei parametri e la comunicazione necessaria per un client chiamare un oggetto applicazione che è in esecuzione in un ambiente di esecuzione diversi, ad esempio in un thread diverso o in un altro processo. Il proxy con il client si trova e comunica con uno stub corrispondente che si trova con l'oggetto applicazione che viene chiamato. Vedere anche dello stub.

## <a name="r"></a>R
 URL relativo A parzialmente qualificato URL che specifica una risorsa in Internet o intranet la cui posizione è relativa a un punto di partenza specificato da un URL assoluto o un oggetto connessione ADO equivalente. In effetti, il concatenati assoluto e relativo URL rappresentare un URL completo. Vedere anche URL e l'URL assoluto.

 Un'origine dati esistente in un altro computer, piuttosto che nel sistema locale (in cui l'applicazione client esegue) dell'origine dati remoti.

 record di risorse a un record da un provider di codice sorgente di documento che contiene i campi per la definizione e la descrizione di un documento o cartella. Il documento stesso non è contenuto nel record di risorse, ma in genere sono accessibili tramite il flusso predefinito o un campo nel record di risorse che contiene un URL. Vedere anche provider di origine di documenti, flusso predefinito, URL.

 set di righe A set di righe da un'origine dati, tutti con lo stesso schema del campo. Un set di righe può rappresentare alcuni o tutti i campi da una tabella. Un set di righe può anche rappresentare una tabella virtuale, creata da una query o un join di due o più tabelle. In ADO, i set di righe sono rappresentati dal **Recordset** oggetti.

## <a name="s"></a>S
 Definire l'ambito l'intervallo di riferimento per un oggetto o una variabile o un intervallo di record in una tabella o una vista. Ad esempio, variabili locali possono fare riferimento solo all'interno della routine in cui sono stati definiti. Variabili pubbliche sono accessibili da un punto qualsiasi nell'applicazione. Gli oggetti, ad esempio il database corrente, sono nell'ambito se sono nel percorso di ricerca definita. Con una clausola di ambito in molti comandi, è possibile specificare gli intervalli dei record.

 provider di servizi Software che incapsula un servizio, producono e usano i dati, in modo da integrare le funzionalità nelle applicazioni ADO. Si tratta di un provider che non espone direttamente i dati, piuttosto fornisce un servizio, ad esempio l'elaborazione delle query. Il provider del servizio può elaborare i dati forniti da un provider di dati. Vedere anche il provider di dati.

 la forma A Recordset **Recordset** le cui colonne sono state definite in modo specifico per contenere non solo i dati, ma anche i riferimenti (denominati capitoli) ad altri **Recordset** oggetti e/o valori calcolati in base altri **Recordset** oggetti.

 elemento di pari livello qualsiasi due o più nodi in una struttura gerarchica che sono allo stesso livello nella gerarchia. Il nodo radice in una gerarchia non dispone di alcun elementi di pari livello.

 la stored procedura precompilato raccolta di codice, ad esempio le istruzioni SQL e istruzioni di controllo di flusso facoltative archiviate con un nome ed elaborate come unità. Le stored procedure vengono archiviate all'interno di un database; essi possono essere eseguite con un'unica chiamata da un'applicazione e consente le variabili dichiarate a livello utente, l'esecuzione condizionale e altre potenti funzionalità di programmazione.

 stub di un oggetto specifico dell'interfaccia che fornisce il marshalling dei parametri e la comunicazione necessaria per un oggetto di applicazione ricevere le chiamate da un client in cui è in esecuzione in un ambiente di esecuzione diversi, ad esempio in un thread diverso o in un altro processo. Lo stub si trova con l'oggetto applicazione e comunica con un proxy corrispondente che si trova con il client che lo chiama. Vedere anche proxy.

 elemento figlio vedere sottonodo.

 operazione sincrona di un'operazione avviata dal codice che viene completata prima dell'operazione successiva venga avviato. Vedere anche l'operazione asincrona.

## <a name="t-z"></a>T-Z
 Struttura ad albero oggetto che rappresenta una relazione gerarchica tra gli elementi (nodi). È presente un nodo al livello superiore di un albero (radice). Sotto la radice, possono essere presenti più elementi figlio. Ogni elemento figlio a sua volta potrebbe essere l'elemento padre di altri elementi figlio, pertanto la diramazione, ad esempio una struttura ad albero. Una cartella contenente i documenti e altre cartelle è un esempio tipico di una struttura ad albero. Vedere anche alla gerarchia, nodi, root, figlio, padre.

 Server Web un computer che fornisce i servizi Web e le pagine per gli utenti di Internet e intranet.
