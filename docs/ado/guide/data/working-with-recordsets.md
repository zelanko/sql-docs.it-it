---
title: Uso dei recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2378d438c575ad54a89f09c4c9ddcb157c246ffd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508748"
---
# <a name="working-with-recordsets"></a>Utilizzo dei recordset
Il **Recordset** oggetto offre funzionalità incorporate che consentono di ottimizzare l'ordine dei dati nel set di risultati, per cercare un record specifico in base ai criteri che viene fornito e anche per ottimizzare le operazioni di ricerca tramite indici. Se queste funzionalità sono disponibili per l'utilizzo dipende dal provider e in alcuni casi, ad esempio quella del [indice](../../../ado/reference/ado-api/index-property.md) proprietà - la struttura dell'origine dati stessa.  
  
## <a name="arranging-data"></a>Disposizione dei dati  
 Spesso, il modo più efficiente per ordinare i dati nel **Recordset** specificando una clausola ORDER BY nel comando SQL utilizzato per restituire i risultati a esso. Tuttavia, potrebbe essere necessario modificare l'ordine dei dati in un **Recordset** che è già stato creato. È possibile usare la **ordinamento** proprietà per stabilire l'ordine in cui le righe di una **Recordset** vengono attraversati. Inoltre, il **filtro** proprietà determina quali righe risultano accessibili quando si attraversano le righe.  
  
 Il **ordinamento** proprietà imposta o restituisce un **stringa** i nomi di valore che indica il campo nel **Recordset** sul quale eseguire l'ordinamento. Ogni nome è separato da una virgola e, facoltativamente, è seguito da uno spazio e la parola chiave **ASC** (che consente di ordinare il campo in ordine crescente) o **DESC** (che consente di ordinare il campo in ordine decrescente). Per impostazione predefinita, se non viene specificata alcuna parola chiave, il campo viene ordinato in ordine crescente.  
  
 L'operazione di ordinamento è efficiente poiché i dati non sono fisicamente ordinati, sono possibile accedere nell'ordine specificato da un indice.  
  
 Il **ordinamento** proprietà richiede la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà viene impostata su **adUseClient**. Verrà creato un indice temporaneo per ogni campo specificato nel **ordinamento** proprietà se non ne esiste già.  
  
 Impostando il **ordinamento** proprietà in una stringa vuota verrà ripristinato l'ordine originale delle righe ed eliminare indici temporanei. Gli indici esistenti non verranno eliminati.  
  
 Si supponga che un **Recordset** contiene tre campi denominati *firstName*, *middleInitial*, e *lastName*. Impostare il **ordinamento** proprietà sulla stringa "`lastName DESC, firstName ASC`", che ordinerà i **Recordset** in base al cognome in ordine decrescente e quindi al nome in ordine crescente. Il secondo nome viene ignorato.  
  
 Nessun campo di cui viene fatto riferimento in una stringa di criteri di ordinamento può essere denominato "ASC" o "DESC" in quanto tali nomi siano in conflitto con le parole chiave **ASC** e **DESC**. Assegnare a un campo con un alias di un nome in conflitto con il **AS** parola chiave nella query che restituisce il **Recordset**.  
  
 Per altre informazioni sulle **Recordset** applicazione di filtri, vedere "Filtraggio dei risultati" più avanti in questo argomento.  
  
## <a name="finding-a-specific-record"></a>Ricerca di un Record specifico  
 In ADO il [trovare](../../../ado/reference/ado-api/find-method-ado.md) e [Seek](../../../ado/reference/ado-api/seek-method.md) metodi di individuazione di un record specifico in un **Recordset**. Il **trovare** metodo è supportato da una varietà di provider, ma è limitato a un criterio di ricerca singola. Il **Seek** metodo supporta la ricerca in più criteri, ma non è supportato da numerosi provider.  
  
 Gli indici sui campi possono migliorare notevolmente le prestazioni dei **trovare** (metodo) e **ordinamento** e **filtro** le proprietà del **Recordset** oggetto. È possibile creare un indice interno per un **campo** oggetto impostando la relativa proprietà dinamica [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) proprietà. Questa proprietà dinamica viene aggiunta al **le proprietà** insieme del **campo** dell'oggetto quando si imposta il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**. Tenere presente che questo indice è interno all'ADO non è possibile ottenere l'accesso ad esso o usarlo per altri scopi. Inoltre, questo indice è diverso dal [indice](../../../ado/reference/ado-api/index-property.md) proprietà delle **Recordset** oggetto.  
  
 Il **trovare** metodo consente di individuare rapidamente un valore all'interno di una colonna (campo) di un **Recordset**. È spesso possibile migliorare la velocità dei **trovare** metodo su una colonna con il **Optimize** proprietà per creare un indice su di esso.  
  
 Il **trovare** metodo limita la ricerca per il contenuto di un campo. Il **Seek** metodo è necessario disporre di un indice e ha anche altre limitazioni. Se è necessario eseguire la ricerca in più campi che non sono la base di un indice o se il provider non supporta gli indici, è possibile limitare i risultati usando il **filtro** proprietà delle **Recordset** oggetto.  
  
### <a name="find"></a>Trova  
 Il **trovare** metodo cerca una **Recordset** per la riga che soddisfa il criterio specificato. Facoltativamente, può essere specificata la direzione della ricerca, la riga iniziale e offset della riga iniziale. Se viene soddisfatto il criterio, la posizione della riga corrente è impostata sul record trovato. in caso contrario, la posizione è impostata su finale (o avvio) del **Recordset**in base alla direzione di ricerca.  
  
 Per il criterio, è possibile specificare solo un nome di colonna singola. In altre parole, questo metodo non supporta le ricerche a più colonne.  
  
 L'operatore di confronto per il criterio può essere"**>**"(maggiore),"**\<**" (minore di), "=" (uguale), "> =" (maggiore o uguale), "< =" (minore o uguale a), " <> "(non uguale), o"LIKE"(criteri di ricerca).  
  
 Il valore del criterio può essere una stringa, numero a virgola mobile o Data. Valori stringa sono delimitati da virgolette singole o doppie "" cancelletto (#) (ad esempio, "stato ="WA"" o "state = WA # #"). I valori delle date sono delimitati con segni di (cancelletto) "#" (ad esempio, "start_date > & 97/n. 7/22").  
  
 Se l'operatore di confronto è "like", il valore della stringa può contenere un asterisco (*) per trovare una o più occorrenze di qualsiasi carattere o una sottostringa. Ad esempio, "stato come sto\*'" corrisponde a Maine e Massachusetts. È possibile utilizzare anche gli asterischi iniziali e finali per trovare una sottostringa all'interno di valori. Ad esempio, "stato, ad esempio '\*come\*'" corrisponde a Alaska Arkansas e Massachusetts.  
  
 Gli asterischi sono utilizzabile solo alla fine di una stringa di criteri o insieme all'inizio e fine di una stringa di criteri, come illustrato in precedenza. È possibile usare l'asterisco come carattere jolly iniziale ('* str') o incorporati con caratteri jolly s\*r'). Ciò causerà un errore.  
  
### <a name="seek-and-index"></a>Ricerca e di indice  
 Usare la **Seek** metodo insieme al **indice** proprietà se il provider sottostante supporta gli indici per il **Recordset** oggetto. Usare la [supporta](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** metodo per determinare se il provider sottostante supporta **Seek**e il **Supports (adIndex)** metodo per determinare se il provider supporta gli indici. (Ad esempio, il [Provider OLE DB per Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) supporta **Seek** e **indice**.)  
  
 Se **Seek** non trovare la riga desiderata, nessun errore si verifica e la riga è posizionato alla fine delle **Recordset**. Impostare il **indice** proprietà per l'indice desiderato prima di eseguire questo metodo.  
  
 Questo metodo è supportato solo con i cursori sul lato server. Seek non è supportata quando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) valore della proprietà di **Recordset** oggetto è **adUseClient**.  
  
 Questo metodo può essere utilizzato solo quando la **Recordset** oggetto è stato aperto con un [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) pari a **adCmdTableDirect**.  
  
## <a name="filtering-the-results"></a>Filtrare i risultati  
 Il **trovare** metodo limita la ricerca per il contenuto di un campo. Il **Seek** metodo è necessario disporre di un indice e ha anche altre limitazioni. Se è necessario eseguire la ricerca in più campi che non sono la base di un indice o se il provider non supporta gli indici, è possibile limitare i risultati usando il **filtro** proprietà delle **Recordset** oggetto.  
  
 Usare la **filtro** proprietà allo schermo in modo selettivo i record in un **Recordset** oggetto. Filtrati **Recordset** diventa il cursore corrente, che significa che i record che non soddisfano le **filtro** criteri non sono disponibili nel **Recordset** fino a quando non la **Filtro** viene rimosso. Altre proprietà che restituiscono valori in base al cursore corrente sono interessati, ad esempio **esempio di AbsolutePosition**, **AbsolutePage**, **RecordCount**, e  **PageCount**. Infatti, impostando il **filtro** proprietà su un valore specifico sposterà il record corrente per il primo record che soddisfano il nuovo valore.  
  
 Il **filtro** proprietà accetta un argomento di tipo variant. Questo valore rappresenta uno dei tre metodi per l'uso di **filtro** proprietà: una stringa di criteri, un **FilterGroupEnum** costante o una matrice dei segnalibri. Per altre informazioni, vedere la sezione filtro con una stringa di criteri, il filtro con una costante e operazioni di filtro con i segnalibri più avanti in questo argomento.  
  
> [!NOTE]
>  Quando si conoscono i dati che si desidera selezionare, è in genere più efficiente per aprire una **Recordset** con un'istruzione SQL che consente di filtrare in modo efficace il set di risultati, anziché utilizzare il **filtro** proprietà.  
  
 Per rimuovere un filtro da un **Recordset**, utilizzare il **adFilterNone** costante. Impostando il **filtro** proprietà in una stringa di lunghezza zero ("") ha lo stesso effetto utilizzando il **adFilterNone** costante.  
  
### <a name="filtering-with-a-criteria-string"></a>Applicazione di filtri con una stringa di criteri  
 La stringa di criteri è costituito da clausole nel formato *valore dell'operatore FieldName* (ad esempio, `"LastName = 'Smith'"`). È possibile creare clausole composte da singole clausole con l'operatore di concatenazione **AND** (ad esempio, `"LastName = 'Smith' AND FirstName = 'John'"`) e **oppure** (ad esempio, `"LastName = 'Smith' OR LastName = 'Jones'"`). Usare le linee guida seguenti per le stringhe di criteri:  
  
-   *FieldName* deve essere un nome di campo valido dal **Recordset**. Se il nome del campo contiene spazi, è necessario racchiudere il nome nelle parentesi quadre.  
  
-   *Operatore* deve essere uno dei seguenti: **\<**, **>**, **\< =**, **>=** , **<>**, **=**, oppure **come**.  
  
-   *Valore* è il valore con cui si confronteranno i valori di campo (ad esempio `'Smith'`, `#8/24/95#`, `12.345`, o `$50.00`). Utilizzare le virgolette singole (') con le stringhe e caratteri cancelletto (`#`) con le date. Per i numeri, è possibile utilizzare la notazione scientifica i separatori decimali e simboli del dollaro. Se *Operator* viene **quali**, *valore* possono usare caratteri jolly. Solo l'asterisco (\*) e segno di percentuale (%) con caratteri jolly sono consentiti i caratteri e devono essere l'ultimo carattere nella stringa. *Valore* non può essere null.  
  
    > [!NOTE]
    >  Per includere le virgolette singole (') nel filtro *valore*, usare due virgolette singole per rappresentare uno. Ad esempio, per filtrare in base *o ' Malley*, la stringa di criteri deve essere `"col1 = 'O''Malley'"`. Per includere virgolette all'inizio e alla fine del valore del filtro, racchiudere la stringa di segni di cancelletto (#). Ad esempio, per filtrare in base *'1'*, la stringa di criteri deve essere `"col1 = #'1'#"`.  
  
 Non vi è alcuna priorità tra **AND** e **o**. Le clausole possono essere raggruppate all'interno delle parentesi. Tuttavia, non è possibile raggruppare le clausole unite da un **o** e quindi aggiungere il gruppo a un'altra clausola con l'operatore AND, come indicato di seguito.  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 In alternativa, è possibile creare il filtro come indicato di seguito.  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 In un **, ad esempio** clausola, è possibile usare un carattere jolly all'inizio e alla fine del modello (ad esempio, `LastName Like '*mit*'`) o solo alla fine del modello (ad esempio, `LastName Like 'Smit*'`).  
  
### <a name="filtering-with-a-constant"></a>Applicazione di filtri con una costante  
 Le costanti seguenti sono disponibili per il filtraggio **recordset**.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|I filtri per visualizzare solo i record interessati dall'ultima **eliminare**, **Risincronizza**, **UpdateBatch**, oppure **CancelBatch** chiamare.|  
|**adFilterConflictingRecords**|Filtri per visualizzare i record che non hanno superato l'ultimo aggiornamento batch.|  
|**adFilterFetchedRecords**|Filtri per visualizzare i record nella cache corrente, vale a dire, i risultati dell'ultima chiamata a recuperare i record dal database.|  
|**adFilterNone**|Rimuove il filtro corrente e ripristina tutti i record per la visualizzazione.|  
|**adFilterPendingRecords**|I filtri per visualizzare solo i record che sono stati modificati ma non sono ancora stati inviati al server. Applicabile solo per la modalità di aggiornamento batch.|  
  
 Le costanti del filtro rendono più semplice risolvere singoli record conflitti durante la modalità di aggiornamento batch in quanto consente di visualizzare, ad esempio, solo i record che sono stati interessati durante l'ultima **UpdateBatch** chiamata al metodo, come illustrato di esempio seguente.  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>Applicazione di filtri con i segnalibri  
 Infine, è possibile passare una matrice di varianti dei segnalibri per il **filtro** proprietà. Il cursore restituito conterrà solo i record il cui segnalibro è stato passato alla proprietà. Esempio di codice seguente crea una matrice di segnalibri dai record in una **Recordset** che hanno una "B" nel *ProductName* campo. Quindi passa la matrice per il **filtro** proprietà e visualizza le informazioni sull'oggetto risultante filtrato **Recordset**.  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>Creazione di un Clone di un Recordset  
 Usare la **Clone** metodo per creare più, Duplica **Recordset** oggetti, soprattutto se si vuole mantenere più di un record corrente in un determinato set di record. Usando il **Clone** è più efficiente rispetto alla creazione e apertura di un nuovo metodo **Recordset** oggetto con la stessa definizione dell'originale.  
  
 Il record corrente di un clone appena creato originariamente è impostato per il primo record. Puntatore al record corrente in clonato **Recordset** non è sincronizzato con l'originale o viceversa. È possibile spostarsi in modo indipendente in ognuna **Recordset**.  
  
 Le modifiche apportate a uno **Recordset** oggetto saranno visibili in tutti i suoi cloni indipendentemente dal tipo di cursore. Tuttavia, dopo l'esecuzione [Requery](../../../ado/reference/ado-api/requery-method.md) sull'originale **Recordset**, non è più cloni verranno sincronizzati con la versione originale.  
  
 Chiusura originale **Recordset** chiusa relative copie, non comporta la chiusura di una copia vicino originale o una delle altre copie.  
  
 È possibile clonare una **Recordset** oggetto solo se supporta segnalibri. I valori di segnalibro sono intercambiabili; vale a dire, un riferimento di segnalibro da una **Recordset** oggetto fa riferimento allo stesso record in uno qualsiasi dei suoi cloni.
