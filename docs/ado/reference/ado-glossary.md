---
title: Glossario ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1af86e92d689f262833e1bc00d8caf0fb0c78b39
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709980"
---
# <a name="ado-glossary"></a>Glossario di ADO
In questo argomento definisce termini rilevanti per ADO.  
  
## <a name="a"></a>A  
 URL assoluto  
 URL completo che specifica il percorso di una risorsa che si trova su Internet o intranet. Vedere anche *URL* e *URL relativo*.  
  
 Controllo ActiveX  
 Registrazione automatica, in-process componente COM che spesso ha un elemento visivo in fase di progettazione o di esecuzione. Controlli ActiveX sono inoltre in grado di comunicare con un contenitore di documenti attivi, ad esempio Microsoft Internet Explorer.  
  
 ADISAPI (Advanced Data Internet Server Application Programming Interface)  
 Una DLL ISAPI che fornisce l'analisi, controllo di automazione, il marshalling di Recordset e creazione del pacchetto MIME. Il componente ADISAPI funziona tramite l'API fornita da Internet Information Services (IIS). Vedere anche *ISAPI*.  
  
 funzione di aggregazione  
 In una query, una funzione, ad esempio COUNT, AVG o STDEV che consente di calcolare un valore usando tutte le righe in una colonna di una tabella. Nella scrittura di espressioni e nella programmazione, è possibile utilizzare le funzioni di aggregazione SQL (inclusi i tre elencati in precedenza) e funzioni di aggregazione sui domini per determinare le statistiche diverse.  
  
 alias  
 Nome alternativo assegnato a una colonna o espressione in un'istruzione SQL SELECT, spesso più breve o più significativa. Ad esempio, BobSales è l'alias dell'istruzione SELECT seguente: "Selezionare wr Sales come BobSales da SalesDB". Un alias può essere utilizzato per assegnare dinamicamente le colonne per le associazioni del controllo sull'oggetto DataControl.  
  
 threading apartment  
 Un modello di threading COM in cui si verificano tutte le chiamate a un oggetto in un unico thread. Nel threading apartment COM Sincronizza ed effettua il marshalling di chiamate. Vedere anche *COMmddefcom*.  
  
 operazione asincrona  
 Un'operazione che restituisce il controllo al programma chiamante senza attendere il completamento dell'operazione. Prima che l'operazione è stata completata, continua l'esecuzione di codice. Vedere anche *operazione sincrona*.  
  
## <a name="b"></a>B  
 voce binding  
 Un mapping tra un campo in una tabella e una variabile. Nelle estensioni ADO di Visual C++, **Recordset** mapping dei campi per le variabili di C/C++.  
  
 Maschera di bit  
 Un valore numerico è progettato per confrontare i valori di bit per bit con gli altri valori numerici, in genere per contrassegnare le opzioni di parametro o i valori restituiti. In genere questo confronto viene eseguito con gli operatori logici bit per bit, ad esempio **e** e **oppure** in Visual Basic **&** e **&#124;** in C++.  
  
 Ad esempio, l'oggetto ADO **FieldAttributeEnum** valori possono essere usati come maschere di bit per determinare gli attributi di un campo. Si supponga di che voler determinare se un campo non è aggiornabile. È stato possibile effettuare questa verifica con l'espressione seguente in Visual Basic:`Field.Attributes AND adFldUpdatable`  
  
 Se il risultato è TRUE, il campo è aggiornabile.  
  
 segnalibro  
 Un indicatore che identifica in modo univoco una riga all'interno di un set di righe in modo che un utente può passare rapidamente a esso.  
  
 oggetto business  
 Oggetto che esegue un set definito di operazioni, ad esempio logica della regola business o la convalida dei dati. Gli oggetti business si trovano in genere nel livello intermedio.  
  
 regola di Business  
 La combinazione di modifiche di convalida, verifiche di accesso, le ricerche nel database, i criteri e trasformazioni algoritmiche che costituiscono un'azienda di attività di business. Noto anche come *logica di business*.  
  
## <a name="c"></a>c  
 espressione calcolata  
 Un'espressione che non è costante, ma il cui valore dipende da altri valori. Per poter essere valutata, un'espressione calcolata necessario ottenere e calcolare i valori da altre origini, in genere in altri campi o righe.  
  
 Capitolo  
 Un riferimento a un intervallo di righe da un'origine dati. In ADO un capitolo viene in genere un riferimento a un'altra **Recordset**.  
  
 Le colonne a capitoli consentono di definire un *padre-figlio* relazione in cui il *padre* è la **Recordset** contenente la colonna a capitoli e  *figlio* è il **Recordset** rappresentato dal capitolo.  
  
 capitolo-alias  
 Un alias che fa riferimento alla colonna aggiunta all'elemento padre.  
  
 set di caratteri  
 Mapping di un set di caratteri per i relativi valori numerici. Ad esempio, Unicode è un carattere a 16 bit impostato in grado di codifica dei caratteri noti tutti e usato come uno standard di codifica dei caratteri in tutto il mondo.  
  
 child  
 Il lato dipendente di una relazione gerarchica. Un elemento figlio è un nodo in una struttura gerarchica che include un altro nodo sopra di esso (più vicino alla radice). Vedere anche *figlio-alias*, *relazione padre-figlio*, *padre*.  
  
 alias-figlio  
 Un alias che fa riferimento all'elemento figlio. Vedere anche *alias*, *figlio*.  
  
 CLSID (identificatore di classe)  
 Un identificatore univoco universale (UUID) che identifica un componente COM. Ogni componente COM ha valore CLSID corrispondente nel Registro di sistema Windows in modo che può essere caricato da altre applicazioni. Vedere anche *ProgID*, *COM*.  
  
 livello client  
 Un livello logico di un sistema distribuito che presenta in genere i dati ed elabora l'input da parte dell'utente, detta anche il *front-end*. In genere, il livello client richiede dati da un server in base all'input, quindi formatta e visualizza il risultato. Vedere anche *livello intermedio*, *livello di origine dati*, *un'applicazione distribuita*.  
  
 COM (Component Object Model)  
 Binario standard che consente agli oggetti di interoperabilità in un ambiente di rete indipendentemente dalla lingua in cui sono state sviluppate o nei computer che si trovino. Tecnologie basate su COM, includono i controlli ActiveX, automazione e il collegamento e incorporamento (OLE). Consente a un oggetto per esporne la funzionalità agli altri componenti e alle applicazioni host. Definisce come l'oggetto espone sé sia come questa esposizione funziona tra processi e tra reti. COM definisce anche il ciclo di vita dell'oggetto.  
  
 Componente COM  
 File binario, ad esempio con estensione dll, ocx e alcuni file .exe - che supporta lo standard di COM per specificare gli oggetti. Questo file contiene codice per uno o più class factory, le classi COM, voci di registro, il codice di caricamento e così via.  
  
 Operatore di confronto  
 Un operatore che confronta due espressioni e restituisce un valore booleano.  
  
 Un parametro di criteri che può essere espresso come ">" (maggiore di), "\<" (minore di), "=" (uguale), "> =" (maggiore o uguale), "< =" (minore o uguale a), "<>" (non uguale), o "like" (criteri di ricerca).  
  
 componente  
 Oggetto che incapsula i dati e codice e fornisce un set ben definito di servizi disponibili pubblicamente.  
  
 file compositi  
 Un'implementazione di COM strutturato archiviazione per i file. Un file composto Archivia oggetti separati in un file singolo, strutturato costituito da due elementi principali: gli oggetti di archiviazione e gli oggetti flusso. Insieme, il loro funzionamento, ad esempio un file system all'interno di un file.  
  
 Un numero di file singoli associato insieme in un file fisico. Ogni singolo file in un file composto è accessibile come se fosse un unico file fisico.  
  
 constant  
 Valore numerico o stringa che non cambia. Enumerazioni di ADO denominate (costanti enumerate) utilizzabile nel codice anziché i valori effettivi, ad esempio, **adUseClient** è una costante il cui valore è 3. (Anche enumerazione = 3). Vedere anche *enumerazione*.  
  
 cursor  
 Un elemento di database che controlla la navigazione tra i record, aggiornabilità dei dati e la visibilità delle modifiche apportate al database da altri utenti.  
  
## <a name="d"></a>D  
 Associazione dati  
 Il processo di associazione di oggetti o i controlli di un'applicazione a un'origine dati. Un controllo associato a un'origine dati viene chiamato un *controllo con associazione a dati*.  
  
 Il contenuto di un controllo con associazione a dati è associato i valori da un database. Ad esempio, un controllo griglia associata a un **Recordset** oggetto può essere aggiornato quando le righe nel **Recordset** vengono aggiornati. Quando i nuovi valori vengono recuperati per il **Recordset**, nuovi valori vengono visualizzati nella griglia.  
  
 provider di dati  
 Software che espone i dati a un'applicazione ADO direttamente o tramite un provider di servizi. Vedere anche provider di servizi.  
  
 data shaping  
 Una tecnica che usa una sintassi formalizzata (chiamati **forma language**) per definire un'oggetto specifico **Recordset** oggetto (chiamato un *a forma di Recordset*) che non contiene solo i dati, ma anche i riferimenti ad altri **Recordset** oggetti e/o valori calcolati in base i loro **Recordset** oggetti.  
  
 livello di origine dati  
 Un livello logico di un sistema distribuito che rappresenta un computer che esegue un sistema DBMS, ad esempio un database di SQL Server. Vedere anche *livello client*, *livello intermedio*, *un'applicazione distribuita*.  
  
 DCOM  
 Un protocollo di rete che consente ai componenti COM comunicare direttamente tra loro attraverso una rete. Vedere anche *COM*, *componente*.  
  
 DDL (Data Definition Language)  
 Tali istruzioni SQL che definiscono, in contrapposizione per manipolare i dati. Lo schema di un database viene creato o modificato tramite il linguaggio DDL. Ad esempio, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **revocare** sono istruzioni SQL DDL.  
  
 flusso predefinito  
 Un flusso di testo o binari (rappresentato da un **Stream** oggetto) che è associato **Record** o **Recordset** oggetti quando si utilizza provider OLE DB specifici, ad esempio il Provider Microsoft OLE DB per Internet Publishing. Il flusso predefinito include in genere il contenuto di un file, ad esempio il codice HTML per la radice di un sito Web.  
  
 applicazione distribuita  
 Un programma scritto in modo che l'elaborazione può essere suddivise tra più computer in rete. In genere, un'applicazione distribuita è suddiviso in presentazione, logica di business e dati livelli di archivio, o *livelli*. Vedere anche il livello client, livello intermedio, livello di origine dati.  
  
 Recordset disconnesso  
 Oggetto **Recordset** oggetto in una cache client che non ha più una connessione in tempo reale al server. Se l'origine dati originale deve accedere nuovamente per qualche motivo, ad esempio l'aggiornamento dei dati, la connessione deve essere ristabilita. Tuttavia, le raccolte, proprietà e metodi di un disconnessa **Recordset** rimangono comunque accessibili.  
  
 DML (Data Manipulation Language)  
 Tali istruzioni SQL che modificano, anziché per definire, i dati. I valori in un database siano selezionati e modificati con DML. Ad esempio, **inserire**, **UPDATE**, **Elimina**, e **selezionare** sono istruzioni DML SQL.  
  
 provider di codice sorgente di documento  
 Una classe speciale di provider che gestiscono le cartelle e documenti. Quando un documento è rappresentato da un **Record** oggetto o una cartella dei documenti è rappresentato da un **Recordset** dell'oggetto, il provider di origine del documento consente di popolare gli oggetti con un set univoco di campi che Descrive le caratteristiche del documento, anziché il documento vero e proprio. Vedere anche record di risorse.  
  
 DSN (nome dell'origine dati)  
 Raccolta di informazioni usate per connettere l'applicazione a un database ODBC specifico. Gestione Driver ODBC Usa queste informazioni per creare una connessione al database. Un DSN può essere archiviato in un file (DSN su file) o nel Registro di sistema Windows (DSN computer).  
  
 proprietà dinamica  
 Proprietà specifiche di un provider di dati o il servizio di cursore. Il **proprietà** raccolta di un oggetto viene popolato automaticamente con queste ("dinamico"). Un oggetto non dispone di alcuna proprietà dinamica fino a quando non è connesso a un'origine dati tramite un provider di dati specifico. Vedere anche i dati provider, cursore.  
  
## <a name="e"></a>E  
 Enumerazione  
 Un elenco di costanti denominate. I valori enumerati non devono essere univoci. Tuttavia il nome di ogni valore deve essere univoco all'interno dell'ambito in cui è definita l'enumerazione. In ADO, le enumerazioni vengono usate per il parametro numerico e restituiscono valori, aggiungere un significato al codice ADO e proteggere allo sviluppatore di valori numerici (che possono cambiare da una versione a altra). Ad esempio, per aprire un valore statico **Recordset**, utilizzare il **adOpenStatic** valore enumerato: `Recordset.Open ,,adOpenStatic`  
  
 Detta anche *costante enumerata*. Vedere anche *costante*.  
  
 evento  
 Un'azione che viene riconosciuta da un oggetto, per cui è possibile scrivere codice per rispondere. Gli eventi possono essere generati dall'esecuzione del comando, il completamento delle transazioni, navigazione del recordset e gli aggiornamenti dei dati, tra le altre azioni. Vedere anche *gestore dell'evento*.  
  
 gestore dell'evento  
 Un gestore eventi è il codice che viene eseguito quando si verifica un evento. Vedere anche l'evento.  
  
## <a name="h"></a>H  
 gestore  
 Una routine che gestisce una condizione comune e relativamente semplice o operazione, ad esempio gestione degli errori di ripristino o i dati.  
  
 Recordset gerarchici  
 Oggetto **Recordset** che contiene l'altra **Recordset**. Vedere anche data shaping, capitolo.  
  
 Per altre informazioni, vedere [accesso alle righe in un Recordset gerarchico](../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 gerarchia  
 In generale, una gerarchia è una struttura di pertinenza maggiore con un alto livello e livelli subordinati. In ADO, gerarchica **recordset** vengono usati per rappresentare la relazione padre-figlio tra un record e un capitolo. Anche in ADO **Record** e **Stream** gli oggetti possono essere utilizzati per accedere a strutture ad albero gerarchica, ad esempio documenti e una cartella. Include anche ADO MD **gerarchia** oggetti per rappresentare una relazione tra i livelli di una dimensione in un cubo OLAP. Vedere anche recordset gerarchici, relazione padre-figlio, capitolo, struttura ad albero.  
  
## <a name="i-l"></a>I-L  
 ISAPI (Internet Server Application Programming Interface)  
 Un set di funzioni per i server Internet, ad esempio un Server Windows NT® Server o Windows 2000 in esecuzione Microsoft® Internet Information Services (IIS).  
  
 Chiave  
 Una o più colonne in una tabella che identificano in modo univoco una riga. spesso usati per indicizzare una tabella.  
  
## <a name="m"></a>M  
 Marshalling  
 Il processo di creazione di pacchetti, invio e disassemblaggio interfaccia dei parametri dei metodi attraverso i limiti di thread o processo.  
  
 Livello intermedio  
 Il livello logico in un sistema distribuito tra un'interfaccia utente o client Web e il database. Si tratta in genere in cui vengono create istanze degli oggetti business. Il livello intermedio è una raccolta di regole di business e le funzioni che generano e operano al momento della ricezione di informazioni. Per ottenere questo risultato tramite regole business che possono cambiare di frequente e pertanto vengono incapsulate in componenti che sono fisicamente separati dalla logica dell'applicazione stessa. Noto anche come *livello del server applicazioni*. Vedere anche applicazioni distribuite, livello client, livello di origine dati.  
  
 MIME (Multipurpose Internet Mail estensione)  
 Un protocollo Internet originariamente sviluppato per consentire lo scambio di messaggi di posta elettronica con contenuto avanzato tra ambienti di posta elettronica, macchina e rete eterogenea. In pratica, MIME è anche stato adottato ed esteso da applicazioni non di posta elettronica.  
  
 MIME è uno standard che consente di essere pubblicate e leggere in Internet i dati binari. L'intestazione di un file con dati binari contiene il tipo MIME dei dati. informa i programmi client (browser Web e pacchetti di posta elettronica, ad esempio) che dovranno gestire i dati in modo diverso rispetto a testo normale. Ad esempio, l'intestazione di un documento Web che contiene un'immagine JPEG contiene il tipo MIME specifico nel formato file JPEG. In questo modo un browser visualizzare il file con il relativo visualizzatore JPEG, se presente.  
  
## <a name="n-o"></a>N-O  
 node  
 Un elemento in una struttura ad albero gerarchica. Un nodo può essere la radice o figlio di un altro nodo. Un nodo può anche essere l'elemento padre di più figli. Vedere anche alla gerarchia, struttura ad albero, root, figlio, padre.  
  
 variabile oggetto  
 Variabile che contiene un riferimento a un oggetto. Ad esempio, `objCustomObject` è una variabile che punta a un oggetto di tipo OggettoPersonalizzato:`Set objCustomObject = CreateObject(adodb.Recordset)`  
  
 ODBC (Open Database Connectivity)  
 Standard del linguaggio interfaccia di programmazione utilizzata per connettersi a un'ampia gamma di origini dati. Questo è generalmente possibile accedervi tramite Pannello di controllo, in cui i nomi delle origini dati (DSN) possono essere assegnati a usare i driver ODBC specifici.  
  
 OLE DB  
 Un set di interfacce che espongono i dati da un'ampia gamma di origini tramite COM. Le interfacce OLE DB di offrono applicazioni con accesso uniforme ai dati archiviati in diverse origini dati. Queste interfacce supportano la quantità di funzionalità DBMS appropriato per l'origine dati, in modo da poter condividere i propri dati. Vedere anche COM.  
  
 il blocco ottimistico  
 Un tipo di blocco in cui la pagina di dati che contiene uno o più record, tra cui il record viene modificato, non è disponibile ad altri utenti solo mentre il record viene aggiornato mediante il **Update** (metodo), ma è disponibile prima e dopo il le chiamate a **Update**.  
  
 Blocco ottimistico viene usato quando le **Recordset** apertura dell'oggetto con il **LockType** parametro o una proprietà impostata su **adLockOptimistic** o  **adLockBatchOptimistic**. Vedere anche il blocco pessimistico.  
  
 valore ordinale  
 Posizione numerica di un elemento all'interno di un ordine. In una raccolta di ADO, il valore ordinale del primo elemento è zero (0). L'elemento successivo è uno (1) e così via.  
  
## <a name="p"></a>P  
 comando con parametri  
 Una query o un comando che consente di impostare i valori dei parametri prima dell'esecuzione del comando. Ad esempio, una stringa SQL può essere parametrizzata incorporando i marcatori di parametro nella stringa SQL (definito dal '?' caratteri). Quindi, l'applicazione specifica i valori per ogni parametro ed esegue il comando.  
  
 padre  
 Il controllo lato di una relazione gerarchica. In una struttura gerarchica, un elemento padre ha uno o più nodi figlio direttamente sotto di esso nella gerarchia. Vedere anche alias padre, figlio e relazione padre-figlio.  
  
 parent-alias  
 Un alias che fa riferimento all'elemento padre. Vedere anche alias, elemento padre.  
  
 relazione padre-figlio  
 Una relazione in una struttura gerarchica in cui l'elemento padre è un livello superiore e direttamente associato a uno o più figli. Un elemento figlio è a un livello inferiore e deve avere un elemento padre. Vedere anche l'elemento padre, figlio.  
  
 Il blocco pessimistico  
 Tipo di blocco in cui la pagina che contiene uno o più record, tra cui il record viene modificato, è disponibile ad altri utenti per garantire che un aggiornamento verrà eseguito. Comportamento di blocco pessimistico è definito dal provider OLE DB. In genere, i record sono bloccati durante la modifica e rimangono disponibili finché il **Update** metodo è stata completata.  
  
 Il blocco pessimistico è abilitato quando la **Recordset** apertura dell'oggetto con il **LockType** parametro o una proprietà impostata su **adLockPessimistic**. Vedere anche il blocco ottimistico.  
  
 Limitazione delle richieste  
 Ottimizzazione delle prestazioni basata sull'uso di raccolte di pre-allocare risorse, ad esempio gli oggetti o le connessioni al database. È più efficiente per disegnare una risorsa esistente dal pool di piuttosto che creare una nuova risorsa.  
  
 Identificatore programmatico (ProgID)  
 Un nome univoco mappato nel Registro di sistema di Windows da un'applicazione COM. Il ProgID di una connessione ADO è "ADODB. Connessione". Vedere anche CLSID e COM.  
  
 proxy  
 Un oggetto specifico dell'interfaccia che fornisce il marshalling dei parametri e la comunicazione necessaria per un client chiamare un oggetto applicazione che è in esecuzione in un ambiente di esecuzione diversi, ad esempio in un thread diverso o in un altro processo. Il proxy con il client si trova e comunica con uno stub corrispondente che si trova con l'oggetto applicazione che viene chiamato. Vedere anche dello stub.  
  
## <a name="r"></a>R  
 URL relativo  
 URL parziale che specifica una risorsa in Internet o intranet la cui posizione è relativa a un punto di partenza specificato da un URL assoluto o un oggetto connessione ADO equivalente. In effetti, il concatenati assoluto e relativo URL rappresentare un URL completo. Vedere anche URL e l'URL assoluto.  
  
 origine dati remota  
 Un'origine dati esistente in un altro computer, piuttosto che nel sistema locale (in esecuzione l'applicazione client).  
  
 record di risorse  
 Un record da un provider di codice sorgente di documento che contiene i campi per la definizione e la descrizione di un documento o cartella. Il documento stesso non è contenuto nel record di risorse, ma in genere sono accessibili tramite il flusso predefinito o un campo nel record di risorse che contiene un URL. Vedere anche provider di origine di documenti, flusso predefinito, URL.  
  
 set di righe  
 Un set di righe da un'origine dati, tutti con lo stesso schema del campo. Un set di righe può rappresentare alcuni o tutti i campi da una tabella. Un set di righe può anche rappresentare una tabella virtuale, creata da una query o un join di due o più tabelle. In ADO, i set di righe sono rappresentati dal **Recordset** oggetti.  
  
## <a name="s"></a>S  
 `Scope`  
 L'intervallo di riferimento per un oggetto o variabile o un intervallo di record in una tabella o una vista. Ad esempio, variabili locali possono fare riferimento solo all'interno della routine in cui sono stati definiti. Variabili pubbliche sono accessibili da un punto qualsiasi nell'applicazione. Gli oggetti, ad esempio il database corrente, sono nell'ambito se sono nel percorso di ricerca definita. Con una clausola di ambito in molti comandi, è possibile specificare gli intervalli dei record.  
  
 provider di servizi  
 Software che incapsula un servizio tramite producono e usano i dati, in modo da integrare le funzionalità nelle applicazioni ADO. Si tratta di un provider che non espone direttamente i dati, piuttosto fornisce un servizio, ad esempio l'elaborazione delle query. Il provider del servizio può elaborare i dati forniti da un provider di dati. Vedere anche il provider di dati.  
  
 data shaping Recordset  
 Oggetto **Recordset** le cui colonne sono state definite in modo specifico per contenere non solo i dati, ma anche i riferimenti (denominati capitoli) ad altri **Recordset** oggetti e/o valori calcolati in base altri **Recordset** oggetti.  
  
 pari livello  
 Qualsiasi due o più nodi in una struttura gerarchica che sono allo stesso livello nella gerarchia. Il nodo radice in una gerarchia non dispone di alcun elementi di pari livello.  
  
 stored procedure  
 Raccolta precompilata di codice, ad esempio le istruzioni SQL e istruzioni di controllo di flusso facoltative archiviate con un nome ed elaborate come unità. Le stored procedure vengono archiviate all'interno di un database; essi possono essere eseguite con un'unica chiamata da un'applicazione e consente le variabili dichiarate a livello utente, l'esecuzione condizionale e altre potenti funzionalità di programmazione.  
  
 Stub  
 Un oggetto specifico dell'interfaccia che fornisce il marshalling dei parametri e la comunicazione necessaria per un oggetto di applicazione ricevere le chiamate da un client in cui è in esecuzione in un ambiente di esecuzione diversi, ad esempio in un thread diverso o in un altro processo. Lo stub si trova con l'oggetto applicazione e comunica con un proxy corrispondente che si trova con il client che lo chiama. Vedere anche proxy.  
  
 nodo secondario  
 Vedere figlio.  
  
 operazione sincrona  
 Un'operazione avviata dal codice che viene completato prima che venga avviato l'operazione successiva. Vedere anche l'operazione asincrona.  
  
## <a name="t-z"></a>T-Z  
 Struttura ad albero  
 Una struttura che rappresenta una relazione gerarchica tra gli elementi (nodi). È presente un nodo al livello superiore di un albero (radice). Sotto la radice, possono essere presenti più elementi figlio. Ogni elemento figlio a sua volta potrebbe essere l'elemento padre di altri elementi figlio, pertanto la diramazione, ad esempio una struttura ad albero. Una cartella contenente i documenti e altre cartelle è un esempio tipico di una struttura ad albero. Vedere anche alla gerarchia, nodi, root, figlio, padre.  
  
 Server Web  
 Un computer che fornisce i servizi Web e le pagine per gli utenti di Internet e intranet.
