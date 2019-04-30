---
title: Programmazione ADO in Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 232b7c739e274ba9252c14dd28e739934cbd42e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63142970"
---
# <a name="visual-c-ado-programming"></a>Programmazione ADO in Visual C++
Il riferimento all'API ADO viene descritta la funzionalità delle ADO application programming interface (API) usando una sintassi simile a Microsoft Visual Basic. Anche se i destinatari sono tutti gli utenti, programmatori ADO utilizzano svariati linguaggi come Visual Basic, Visual C++ (con e senza il **#import** (direttiva)) e Visual J++ (con il pacchetto di classe ADO/WFC).  

> [!NOTE]
> Microsoft è terminato il supporto per Visual J++ nel 2004.

 Per gestire questa diversità il [ADO per gli indici di sintassi Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) forniscono una sintassi specifica del linguaggio Visual C++ con collegamenti a descrizioni comune di funzionalità, parametri, comportamenti e così via, nell'API Riferimento.  
  
 ADO viene implementato con le interfacce COM (Component Object Model). Tuttavia, risulta più semplice per i programmatori di lavorare con COM in alcuni linguaggi di programmazione rispetto ad altri. Ad esempio, quasi tutti i dettagli di utilizzo di COM vengono gestiti in modo implicito per i programmatori Visual Basic, mentre i programmatori Visual C++ devono essere eseguite direttamente.  
  
 Le sezioni seguenti riepilogano i dettagli per i programmatori di C e C++ utilizzando ADO e il **#import** direttiva. L'applicazione è incentrata sui tipi di dati specifici di COM (**Variant**, **BSTR**, e **SafeArray**) e la gestione degli errori ( com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Usando la direttiva del compilatore #import  
 Il **#import** direttiva del compilatore Visual C++ semplifica l'utilizzo di proprietà e metodi ADO. La direttiva accetta il nome di un file contenente una libreria dei tipi, ad esempio la DLL ADO (Msado15.dll) e genera file di intestazione contenenti le dichiarazioni typedef, i puntatori intelligenti per interfacce e costanti enumerate. Ogni interfaccia incapsulato, o con wrapper, in una classe.  
  
 Per ogni operazione all'interno di una classe (vale a dire, una chiamata di metodo o proprietà), non vi è una dichiarazione per chiamare l'operazione direttamente (ovvero, la forma dell'operazione "raw") e una dichiarazione per chiamare l'operazione non elaborato e genera un errore COM se l'operazione non riesce a eseguire succ essfully. Se l'operazione è una proprietà, è in genere una direttiva del compilatore che crea una sintassi alternativa per l'operazione che ha una sintassi come Visual Basic.  
  
 Operazioni che recuperano il valore di una proprietà con nomi nel formato **ottenere**_proprietà_. Operazioni che impostano il valore di una proprietà con nomi nel formato **inserito**_proprietà_. Operazioni che impostano il valore di una proprietà con un puntatore a un oggetto ADO hanno il formato dei nomi **PutRef**_proprietà_.  
  
 È possibile ottenere o impostare una proprietà con le chiamate di questi moduli:  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>Proprietà direttive using  
 Il **declspec**  direttiva del compilatore è un'estensione del linguaggio C specifiche di Microsoft che dichiara una funzione usata come una proprietà per avere una sintassi alternativa. Di conseguenza, è possibile impostare o ottenere valori di una proprietà in modo simile a Visual Basic. Ad esempio, è possibile impostare e ottenere una proprietà in questo modo:  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 Si noti che non è al codice:  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 Il compilatore genererà l'appropriato **ottenere**_-_, **Put**-, o **PutRef**_proprietà_ chiamata in base quale sintassi alternativa viene dichiarato e indica se la proprietà viene letta o scritta.  
  
 Il **declspec**  direttiva del compilatore può solo dichiarare **ottenere**, **put**, o **Ottieni** e **put** sintassi alternativa per una funzione. Operazioni di sola lettura hanno solo una **ottenere** dichiarazione; le operazioni di sola scrittura avere solo una **put** dichiarazione; le operazioni che sono di lettura e scrittura entrambi questi elementi sono **ottenere** e **put** dichiarazioni.  
  
 Solo due dichiarazioni sono possibili con questa direttiva; Tuttavia, ogni proprietà può avere tre funzioni di proprietà: **Ottenere**_proprietà_, **Put**_proprietà_, e **PutRef**_proprietà_. In tal caso, solo due forme di proprietà hanno la sintassi alternativa.  
  
 Ad esempio, il **comandi** oggetto **ActiveConnection** proprietà è dichiarata con una sintassi alternativa per **Ottieni**_ActiveConnection_e **PutRef**_ActiveConnection_. Il **PutRef**-sintassi è un'ottima scelta perché in pratica, è in genere consigliabile inserire un elemento aperto **connessione** oggetto (vale a dire, una **connessione** puntatore all'oggetto) in questo proprietà. D'altra parte, il **Recordset** oggetto presenta **ottenere**-, **Put**-, e **PutRef**_ActiveConnection_operazioni, ma nessuna sintassi alternativa.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>Raccolte, il metodo GetItem e la proprietà dell'elemento  

 ADO definisce diverse raccolte, che include **i campi**, **parametri**, **proprietà**, e **errori**. In Visual C++, il **GetItem (_indice_)** metodo restituisce un membro della raccolta. *Indice* è un **Variant**, il cui valore è un indice numerico del membro della raccolta o una stringa contenente il nome del membro.  
  
 Il **declspec**  direttiva del compilatore dichiara il **articoli** della proprietà come una sintassi alternativa per ogni raccolta fondamentale **GetItem ()** (metodo). La sintassi alternativa Usa le parentesi quadre e ha un aspetto simile a un riferimento della matrice. In generale, le due forme di aspetto simile al seguente:  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 Ad esempio, assegnare un valore a un campo di un **Recordset** oggetto, denominato  **_rs_**, derivata dal **autori** tabella il **pubs** database. Usare la **Item ()** proprietà a cui accedere la terza **campo** del **Recordset** oggetto **campi** (raccolte vengono indicizzate dalla raccolta uguale a zero; si suppone che il terzo campo viene denominato  **_au\_fname_**). Chiamare quindi il **Value ()** metodo sul **campo** oggetto al quale assegnare un valore stringa.  
  
 Ciò può essere espresso in Visual Basic nelle risorse seguenti quattro modi (gli ultimi due formati siano univoci a Visual Basic; altri linguaggi non dispongono di equivalenti):  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 È l'equivalente in Visual C++ per le prime due forme precedente:  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 - oppure - (la sintassi alternativa per il **valore** proprietà vengono visualizzata anche)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 Per esempi di scorrere una raccolta, vedere la sezione "Raccolte di ADO" di "Riferimento ADO".  
  
## <a name="com-specific-data-types"></a>Tipi di dati COM specifici  
 In generale, qualsiasi tipo di dati di Visual Basic che trova nella Guida di riferimento API ADO ha un equivalente di Visual C++. Sono inclusi i tipi di dati standard, ad esempio **unsigned char** per Visual Basic **Byte**, **breve** per **intero**, e  **lungo** per **lungo**. Cerca in Indexesto la sintassi di vedere esattamente che cosa è necessaria per gli operandi di un determinato metodo o proprietà.  
  
 Le eccezioni a questa regola sono i tipi di dati specifici a COM: **Variante**, **BSTR**, e **SafeArray**.  
  
### <a name="variant"></a>Variant  
 Oggetto **Variant** è un tipo di dati strutturato che contiene un membro del valore e un membro del tipo di dati. Oggetto **Variant** può contenere un'ampia gamma di altri tipi di dati tra un'altra variante, BSTR, valore booleano, puntatore IDispatch o IUnknown, valuta, data e così via. COM fornisce inoltre metodi che rendono più semplice convertono un tipo di dati in un altro.  
  
 Il **variant_t** incapsula e gestisce le **Variant** tipo di dati.  
  
 Quando il riferimento all'API ADO che un metodo o proprietà operando assume un valore, in genere significa che il valore viene passato una **variant_t**.  
  
 Questa regola è vera in modo esplicito quando le **parametri** sezione negli argomenti della Guida di riferimento API ADO indica che un operando è un **Variant**. Unica eccezione riguarda la documentazione indica in modo esplicito dell'operando accetta un tipo di dati standard, ad esempio **lungo** oppure **Byte**, o un'enumerazione. Un'altra eccezione si verifica quando l'operando accetta una **stringa**.  
  
### <a name="bstr"></a>BSTR  
 Oggetto **BSTR** (**B**asic **STR**ing) è un tipo di dati strutturato che contiene una stringa di caratteri e la lunghezza della stringa. COM fornisce metodi per allocare, manipolare e senza una **BSTR**.  
  
 Il **bstr_t** incapsula e gestisce le **BSTR** tipo di dati.  
  
 Quando il riferimento all'API ADO indica una proprietà o metodo accetta un **stringa** valore, significa che il valore è sotto forma di un **bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>Esegue il cast di classi bstr_t e variant_t  
 Non è spesso necessario al codice in modo esplicito un **variant_t** oppure **bstr_t** in un argomento di un'operazione. Se il **variant_t** oppure **bstr_t** classe ha un costruttore che corrisponde al tipo di dati dell'argomento, il compilatore genererà l'appropriato **variant_t** o**bstr_t**.  
  
 Tuttavia, se l'argomento è ambiguo, vale a dire, il tipo di dati corrisponde a più di un costruttore, è necessario eseguire il cast dell'argomento con tipo di dati appropriato per richiamare il costruttore corretto.  
  
 Ad esempio, la dichiarazione per il **Recordset:: Open** metodo è:  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 Il `ActiveConnection` argomento accetta un riferimento a un **variant_t**, che è possibile codificare una stringa di connessione o un puntatore a un elemento aperto **connessione** oggetto.  
  
 I valori corretti **variant_t** verrà costruita in modo implicito se si passa una stringa, ad esempio "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", o un puntatore, ad esempio "`(IDispatch *) pConn`".  
  
> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.  
  
 Oppure è possibile codificare in modo esplicito un **variant_t** che contiene un puntatore, ad esempio "`_variant_t((IDispatch *) pConn, true)`". Il cast, `(IDispatch *)`, risolve l'ambiguità con un altro costruttore che accetta un puntatore a interfaccia IUnknown.  
  
 È fondamentale, ma raramente menzionato dei fatti, che ADO è un'interfaccia IDispatch. Ogni volta che un puntatore a un oggetto ADO deve essere passato come un **Variant**, è necessario eseguire il cast di tale puntatore come puntatore a un'interfaccia IDispatch.  
  
 Nell'ultimo caso codice in modo esplicito il secondo argomento booleano del costruttore facoltativo, valore predefinito di `true`. Questo argomento fa sì che il **Variant** costruttore chiamare relativo **AddRef**metodo (), che compensa automaticamente la chiamata ADO le **_variant_t::Release**() (metodo) al termine della chiamata di metodo o proprietà ADO.  
  
### <a name="safearray"></a>SafeArray  
 Oggetto **SafeArray** è un tipo di dati strutturato che contiene una matrice di altri tipi di dati. Oggetto **SafeArray** viene chiamato *sicuro* perché contiene informazioni relative ai limiti di ciascuna dimensione della matrice e limita l'accesso agli elementi della matrice entro tali limiti.  
  
 Quando il riferimento all'API ADO che un metodo o proprietà accetta o restituisce una matrice, significa che il metodo o proprietà accetta o restituisce un **SafeArray**, non è una matrice di C/C++ nativa.  
  
 Ad esempio, il secondo parametro del **Connection** oggetto **OpenSchema** metodo richiede una matrice di **Variant** valori. Quelli **Variant** i valori devono essere passati come elementi di un **SafeArray**e che **SafeArray** deve essere impostato come valore di un altro **Variant** . Che altro **Variant** che viene passato come secondo argomento della **OpenSchema**.  
  
 Esempi di come ulteriormente, il primo argomento del **trovare** metodo è un **Variant** il cui valore è una matrice unidimensionale **SafeArray**; ogni degli argomenti facoltativi primi e secondo dei **AddNew** è una matrice unidimensionale **SafeArray**; e il valore restituito del **GetRows** metodo è un **Variant** cui valore è un oggetto bidimensionale **SafeArray**.  
  
## <a name="missing-and-default-parameters"></a>Parametri mancanti e predefiniti  
 Visual Basic consente parametri nei metodi mancanti. Ad esempio, il **Recordset** oggetto **Open** metodo presenta cinque parametri, ma è possibile ignorare i parametri intermedi e lasciare disattivato finali parametri. Un valore predefinito **BSTR** oppure **Variant** verrà sostituito a seconda del tipo di dati dell'operando mancante.  
  
 In C/C++, è necessario specificare tutti gli operandi. Se si desidera specificare un parametro mancante con tipo di dati è una stringa, specificare una **bstr_t** contenente una stringa null. Se si desidera specificare un parametro mancante con tipo di dati è un **Variant**, specificare un **variant_t** con un valore di DISP_E_PARAMNOTFOUND e un tipo di VT_ERROR. In alternativa, specificare l'equivalente **variant_t** costante, **vtMissing**, che viene fornito per il **#import** direttiva.  
  
 Sono tre metodi per l'uso tipico delle eccezioni **vtMissing**. Questi sono i **Execute** metodi del **connessione** e **comando** oggetti e il **NextRecordset** metodo il **Recordset** oggetto. Di seguito sono le relative firme:  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 I parametri *RecordsAffected* e *parametri*, sono disponibili informazioni utili a un **Variant**. *I parametri* è un parametro di input che specifica l'indirizzo di un **Variant** contenente un singolo parametro o una matrice di parametri, che modificheranno il comando in esecuzione. *RecordsAffected* è un parametro di output che specifica l'indirizzo di un **Variant**, in cui viene restituito il numero di righe interessate dal metodo.  
  
 Nel **comando** oggetto **Execute** metodo, indicare che viene specificato alcun parametro impostando *parametri* a una delle due `&vtMissing` (impostazione consigliata) o a il puntatore null (vale a dire **NULL** o zero (0)). Se *parametri* viene impostato al puntatore null, il metodo sostituisce internamente equivalente **vtMissing**e quindi completa l'operazione.  
  
 In tutti i metodi, indicare che il numero di record interessati non deve essere restituito impostando *RecordsAffected* al puntatore null. In questo caso, il puntatore null non è così tanta un parametro mancante come un valore che indica che il metodo deve ignorare il numero di record interessati.  
  
 Di conseguenza, per questi tre metodi, è consentito un elemento di codice, ad esempio:  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>Gestione degli errori  
 In COM, la maggior parte delle operazioni restituiscono un codice restituito HRESULT che indica se una funzione è stata completata. Il **#import** direttiva genera il codice wrapper intorno a ogni metodo "non elaborato" o una proprietà e controlla il valore HRESULT restituito. Se il valore HRESULT indica un esito negativo, il codice wrapper genera un errore COM da con il codice restituito HRESULT è com_issue_errorex (chiamata) come argomento. Gli oggetti di errore COM possono essere rilevati un **provare**-**catch** blocco. (Per i migliori risultati ottenere, intercettare un riferimento a un **com_error** oggetto.)  
  
 Tenere presente che si tratta di errori ADO: sono il risultato di errore in un'operazione di ADO. Gli errori restituiti dal provider sottostante vengono visualizzati come **errore** gli oggetti nel **connessione** oggetto **errori** raccolta.  
  
 Il **#import** direttiva crea solo errori routine di gestione per i metodi e proprietà dichiarate nella DLL di ADO. Tuttavia, è possibile sfruttare i vantaggi dell'errore stesso meccanismo di gestione mediante la scrittura di macro o inline una funzione di controllo degli errori personalizzata. Vedere l'argomento [estensioni di Visual C++](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), o il codice nelle sezioni seguenti per gli esempi.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual C++ gli equivalenti di convenzioni di Visual Basic  
 Di seguito è riportato un riepilogo di alcune convenzioni nella documentazione di ADO, codificati in Visual Basic, nonché i relativi equivalenti in Visual C++.  
  
### <a name="declaring-an-ado-object"></a>Dichiarazione di un oggetto ADO  
 In Visual Basic, una variabile oggetto ADO (in questo caso per un **Recordset** oggetto) viene dichiarato come segue:  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 La clausola "`ADODB.Recordset`", è il valore ProgID del **Recordset** dell'oggetto come definito nel Registro di sistema. Una nuova istanza di un **Record** oggetto viene dichiarato come segue:  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 oppure  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 In Visual C++, il **#import** direttiva genera dichiarazioni di tipo puntatore intelligente per tutti gli oggetti ADO. Ad esempio, una variabile che punta a un **recordset** oggetto è di tipo **RecordsetPtr**e viene dichiarata come segue:  
  
```cpp
_RecordsetPtr  rs;  
```
  
 Una variabile che punta a una nuova istanza di un **recordset** oggetto viene dichiarato come segue:  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 oppure  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 oppure  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 Dopo il **CreateInstance** viene chiamato il metodo, la variabile può essere usata come indicato di seguito:  
  
```cpp
rs->Open(...);  
```
  
 Si noti che in un caso, il "`.`" viene usato come se la variabile fosse un'istanza di una classe (`rs.CreateInstance`) e in altri casi, il "`->`" viene usato come se la variabile fosse un puntatore a un'interfaccia (`rs->Open`).  
  
 Una variabile può essere utilizzata in due modi poiché il "`->`" operatore viene sottoposto a overload per consentire a un'istanza di una classe si comporta come un puntatore a un'interfaccia. Un membro di classe privata della variabile di istanza contiene un puntatore ai **recordset** interfaccia; le "`->`" operatore restituisce tale puntatore; e il puntatore restituito accede ai membri del **Recordset**  oggetto.  
  
### <a name="coding-a-missing-parameter---string"></a>Codifica di un parametro mancante - stringa  
 Quando è necessario codificare un mancante **stringa** operando in Visual Basic, è sufficiente omettere l'operando. È necessario specificare l'operando in Visual C++. Codice di un **bstr_t** che dispone di una stringa vuota come valore.  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>Codifica di un parametro mancante - Variant  
 Quando è necessario codificare un mancante **Variant** operando in Visual Basic, è sufficiente omettere l'operando. È necessario specificare tutti gli operandi in Visual C++. La mancanza di codice **Variant** parametro con un **variant_t** impostato per il valore speciale DISP_E_PARAMNOTFOUND e digitare VT_ERROR. In alternativa, specificare **vtMissing**, che viene fornita da una costante predefinita equivalente le **#import** direttiva.  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 - oppure utilizzare-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>La dichiarazione di una variante  
 In Visual Basic, un **Variant** viene dichiarato con la **Dim** come segue:  
  
```vb
Dim VariableName As Variant  
```
  
 Nell'oggetto visivo C++, dichiarare una variabile come tipo **variant_t**. Alcuni schematica **variant_t** dichiarazioni sono illustrate di seguito.  
  
> [!NOTE]
>  Queste dichiarazioni forniscono un'idea approssimativa di cosa si trattasse del codice nel proprio programma. Per altre informazioni, vedere gli esempi seguenti e la documentazione di Visual C++.  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>Uso delle matrici di tipi Variant  
 In Visual Basic, matrici di **varianti** possono essere codificate con i **Dim** istruzione oppure è possibile usare il **matrice** funzionare, come illustrato nell'esempio di codice seguente:  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 L'oggetto visivo seguente C++ viene illustrato come utilizzare un **SafeArray** usato con un **variant_t**.  
  
#### <a name="notes"></a>Note  
 Le note seguenti corrispondono alle sezioni impostata come commentate nell'esempio di codice.  
  
1.  Ancora una volta, la funzione inline TESTHR() è definita per sfruttare i vantaggi del meccanismo di gestione degli errori esistente.  
  
2.  È sufficiente una matrice unidimensionale, pertanto è possibile utilizzare **SafeArrayCreateVector**, invece di uso generico **SAFEARRAYBOUND** dichiarazione e **SafeArrayCreate** funzione. Di seguito è riportato ciò che dovrebbe risultare il codice, come l'uso **SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  Lo schema identificato dalla costante enumerata **adSchemaColumns**, associato a quattro colonne del vincolo: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME e COLUMN_NAME. Pertanto, una matrice di **Variant** valori con quattro elementi viene creato. Quindi, viene specificato un valore di vincolo che corrisponde alla terza colonna, TABLE_NAME.  
  
     Il **Recordset** restituito è costituito da più colonne, un subset di cui sarà costituito dalle colonne vincoli. I valori delle colonne per ogni riga restituita come vincolo devono essere quello utilizzato per i valori del vincolo corrispondente.  
  
4.  Coloro che conoscono **SAFEARRAY** potrebbe essere sorprendente che **tuttavia**() non viene chiamato prima che l'uscita. In effetti, la chiamata **routine**in questo caso () genererà un'eccezione in fase di esecuzione. Il motivo è che il distruttore `vtCriteria` chiamerà **VariantClear**() quando il **variant_t** esce dall'ambito, che consente di liberare la **SafeArray**. La chiamata **tuttavia**, senza cancellare manualmente le **variant_t**, causerebbe il distruttore provare a cancellare un valore non valido **SafeArray** puntatore.  
  
     Se **routine** sono state chiamate, il codice sarebbe simile al seguente:  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     Tuttavia, è molto più semplice consentire la **variant_t** gestire il **SafeArray**.  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>Utilizzo di proprietà Get/Put/PutRef  
 In Visual Basic, il nome di una proprietà non è qualificato dal fatto che è recuperato, assegnato o assegnato un riferimento.  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 Questo esempio di Visual C++ viene illustrato il **ottenere**/**Put**/**PutRef**_proprietà_.  
  
#### <a name="notes"></a>Note  
 Le note seguenti corrispondono alle sezioni impostata come commentate nell'esempio di codice.  
  
1.  Questo esempio usa due forme di un argomento stringa mancante: una costante, esplicita **strMissing**e una stringa che il compilatore userà per creare una password temporanea **bstr_t** che sarà presente nell'ambito del  **Apri** (metodo).  
  
2.  Non è necessario eseguire il cast dell'operando `rs->PutRefActiveConnection(cn)` al `(IDispatch *)` perché il tipo dell'operando è già `(IDispatch *)`.  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>Utilizzo GetItem (x) e articolo [x]  
 In questo esempio di Visual Basic viene illustrata la sintassi standard e alternativa per **elemento**().  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 Viene illustrato in questo esempio di Visual C++ **elemento**.  
  
> [!NOTE]
>  La nota seguente corrisponde alle sezioni commentate nell'esempio di codice:  Quando si accede all'insieme con **elemento**, l'indice **2**, deve essere eseguito il cast a **long** in modo che venga richiamato un costruttore appropriato.  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>Esegue il cast di puntatori a oggetti ADO con (IDispatch *)  
 Nell'esempio di Visual C++ seguente viene illustrato l'utilizzo (IDispatch *) per puntatori a oggetti ADO cast.  
  
#### <a name="notes"></a>Note  
 Le note seguenti corrispondono alle sezioni impostata come commentate nell'esempio di codice.  
  
1.  Specificare un oggetto aperto **Connection** oggetto in codificato in modo esplicito **Variant**. Eseguire il cast con (IDispatch \*) in modo che verrà richiamato il costruttore corretto. Inoltre, impostare in modo esplicito la seconda **variant_t** parametro per il valore predefinito di **true**, in modo che il conteggio dei riferimenti di oggetto saranno corretti quando il **Recordset:: Open** Termina l'operazione.  
  
2.  L'espressione `(_bstr_t)`, non è un cast, ma un **variant_t** operatore che consente di estrarre una **bstr_t** stringa dal **Variant** restituito da **valore** .  
  
 L'espressione `(char*)`, non è un cast, ma un **bstr_t** operatore che estrae un puntatore alla stringa incapsulata in un **bstr_t** oggetto.  
  
 In questa sezione di codice vengono illustrati alcuni dei comportamenti di utili **variant_t** e **bstr_t** operatori.  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
