---
title: Istruzione FLWOR e iterazione (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4c95d86b64c28bbf78b111f21de7afd58b44616f
ms.sourcegitcommit: 1f10e9df1c523571a8ccaf3e3cb36a26ea59a232
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2018
ms.locfileid: "51858666"
---
# <a name="flwor-statement-and-iteration-xquery"></a>Istruzione e iterazione FLWOR (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery definisce la sintassi di iterazione delle espressioni FLWOR. FLWOR è l'acronimo di `for`, `let`, `where`, `order by` e `return`.  
  
 Un'istruzione FLWOR è costituita dalle parti seguenti:  
  
-   Una o più clausole FOR che associano una o più variabili iteratore alle sequenze di input.  
  
     Le sequenze di input possono essere altre espressioni XQuery, ad esempio espressioni XPath, e corrispondono a sequenze di nodi o a sequenze di valori atomici. È possibile costruire sequenze di valori atomici utilizzando valori letterali o funzioni costruttore. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è consentito utilizzare nodi XML costruiti come sequenze di input.  
  
-   Una clausola `let` facoltativa. che assegna un valore alla variabile specificata per un'iterazione specifica. L'espressione assegnata può essere un'espressione XQuery, quale un'espressione XPath, e può restituire una sequenza di nodi o una sequenza di valori atomici. È possibile costruire sequenze di valori atomici utilizzando valori letterali o funzioni costruttore. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è consentito utilizzare nodi XML costruiti come sequenze di input.  
  
-   Una variabile iteratore. È possibile includere un'asserzione facoltativa del tipo in tale variabile tramite la parola chiave `as`.  
  
-   Una clausola `where` facoltativa. Tale clausola applica un predicato di filtro all'iterazione.  
  
-   Una clausola `order by` facoltativa.  
  
-   Espressione `return`. L'espressione nella clausola `return` costruisce il risultato dell'istruzione FLWOR.  
  
 Ad esempio, tramite la query riportata di seguito viene eseguita l'iterazione sugli elementi <`Step`> del primo centro di produzione e viene restituito il valore stringa dei nodi <`Step`>:  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 Questo è il risultato:  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 La query seguente è analoga alla precedente, tranne per il fatto che viene eseguita sulla colonna XML tipizzata Instructions della tabella ProductModel. Tramite la query viene eseguita l'iterazione su tutte le fasi di produzione, corrispondenti agli elementi <`step`>, nel primo centro di lavorazione per un prodotto specifico.  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   `$Step` è la variabile iteratore.  
  
-   Il [espressione di percorso](../xquery/path-expressions-xquery.md), `//AWMI:root/AWMI:Location[1]/AWMI:step`, genera la sequenza di input. che è la sequenza dei nodi elemento figlio <`step`> del primo nodo elemento <`Location`>.  
  
-   Non viene utilizzata la clausola del predicato facoltativa `where`.  
  
-   Tramite l'espressione `return` viene restituito un valore stringa dall'elemento <`step`>.  
  
 Il [funzione string (XQuery)](../xquery/data-accessor-functions-string-xquery.md) viene usato per recuperare il valore della stringa di <`step`> nodo.  
  
 Risultato parziale:  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 Negli esempi seguenti vengono illustrate sequenze di input aggiuntive consentite:  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], non sono consentite sequenze eterogenee. In particolare, non sono consentite le sequenze che contengono una combinazione di valori atomici e nodi.  
  
 Iterazione viene spesso usata in combinazione con il [costruzione di strutture XML](../xquery/xml-construction-xquery.md) formati di sintassi nella trasformazione di dati XML, come illustrato nella query successiva.  
  
 Nel database di esempio AdventureWorks, le istruzioni di produzione archiviato nel **istruzioni** della colonna della **Production. ProductModel** tabella hanno il formato seguente:  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 Tramite la query seguente viene creata la nuova struttura XML, in cui gli elementi <`Location`> e gli attributi del centro di lavorazione vengono restituiti come elementi figlio:  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 Query:  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Tramite l'istruzione FLWOR viene recuperata una sequenza di elementi <`Location`> per un prodotto specifico.  
  
-   Il [funzione data (XQuery)](../xquery/data-accessor-functions-data-xquery.md) viene utilizzato per estrarre il valore di ogni attributo in modo che verranno aggiunti alla struttura XML risultante come nodi di testo anziché come attributi.  
  
-   L'espressione nella clausola RETURN costruisce la struttura XML desiderata.  
  
 Risultato parziale:  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>Utilizzo della clausola LET  
 È possibile utilizzare la clausola `let` per denominare espressioni ripetute a cui è possibile fare riferimento tramite la variabile. L'espressione assegnata a una variabile `let` viene inserita nella query ogni volta che viene fatto riferimento alla variabile nella query. Ciò significa che l'istruzione viene eseguita tante volte quante volte viene fatto riferimento all'espressione.  
  
 Nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)], le istruzioni di produzione contengono informazioni sugli strumenti richiesti e sulla posizione in cui vengono utilizzati. Nella query seguente viene utilizzata la clausola `let` per elencare gli strumenti richiesti per la compilazione di un modello di produzione e i percorsi in cui è necessario ogni strumento.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>Utilizzo della clausola where  
 È possibile usare il `where` clausola per filtrare i risultati di un'iterazione. Questa operazione viene illustrata nell'esempio seguente.  
  
 Il processo di produzione di una bicicletta passa attraverso una serie di centri di lavorazione, ognuno dei quali definisce una sequenza di fasi di produzione. La query seguente recupera solo i centri di lavorazione che producono un modello di bicicletta e prevedono un numero di fasi di produzione inferiore a tre, ovvero includono meno di tre elementi <`step`>.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il `where` parola chiave viene utilizzata la **Count ()** che consente di contare il numero di <`step`> gli elementi figlio in ogni centro di lavorazione.  
  
-   L'espressione `return` costruisce la struttura XML desiderata a partire dai risultati dell'iterazione.  
  
 Questo è il risultato:  
  
```  
<Location LocationID="30"/>   
```  
  
 Il risultato dell'espressione nella clausola `where` viene convertito in valore booleano tramite le regole seguenti, nell'ordine specificato. Si tratta delle stesse regole utilizzate per i predicati nelle espressioni di percorso, tranne per il fatto che non sono consentiti valori interi:  
  
1.  Se l'espressione `where` restituisce una sequenza vuota, il valore booleano effettivo è False.  
  
2.  Se l'espressione `where` restituisce un valore di tipo booleano semplice, quest'ultimo è il valore booleano effettivo.  
  
3.  Se l'espressione `where` restituisce una sequenza che contiene almeno un nodo, il valore booleano effettivo è True.  
  
4.  In caso contrario, viene restituito un errore statico.  
  
## <a name="multiple-variable-binding-in-flwor"></a>Associazione di più variabili in FLWOR  
 È possibile disporre di una singola espressione FLWOR che associa più variabili alle sequenze di input. Nell'esempio seguente, la query viene specificata su una variabile XML non tipizzata. Tramite l'espressione FLOWR viene restituito il primo elemento figlio <`Step`> in ogni elemento <`Location`>.  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il `for` espressione definisce `$Loc` e $`FirstStep` variabili.  
  
-   Il `two` espressioni `/ManuInstructions/Location` e `$FirstStep in $Loc/Step[1]`, sono correlate in quanto i valori di `$FirstStep` dipendono dai valori di `$Loc`.  
  
-   Tramite l'espressione associata a `$Loc` viene generata una sequenza di elementi <`Location`>. Per ogni elemento <`Location`>, tramite `$FirstStep` viene generata una sequenza costituita da un singolo elemento <`Step`>, ovvero un singleton.  
  
-   `$Loc` viene specificata nell'espressione associata alla variabile `$FirstStep`.  
  
 Questo è il risultato:  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 La query seguente è simile, ad eccezione del fatto che viene specificata sulla colonna Instructions, tipizzata **xml** colonna, delle **ProductModel** tabella. [Costruzione di strutture XML (XQuery)](../xquery/xml-construction-xquery.md) viene usato per generare il codice XML desiderato.  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   La clausola `for` definisce due variabili, `$WC` e `$S`. L'espressione associata a `$WC` genera una sequenza di centri di lavorazione per la produzione di un modello di bicicletta. L'espressione di percorso assegnata alla variabile `$S` genera una sequenza di fasi per ogni sequenza di centri di lavorazione nella variabile `$WC`.  
  
-   L'istruzione return costruisce codice XML con una <`Step`> elemento che contiene la fase di produzione e il **LocationID** come attributo.  
  
-   Il **dichiarare spazio dei nomi predefinito** viene usato nel prologo della XQuery in modo che tutte le dichiarazioni dello spazio dei nomi nel codice XML risultante vengano visualizzate in corrispondenza dell'elemento di primo livello. rendendo in tal modo più leggibile il risultato. Per altre informazioni sugli spazi dei nomi predefinito, vedere [la gestione degli spazi dei nomi in XQuery](../xquery/handling-namespaces-in-xquery.md).  
  
 Risultato parziale:  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>Utilizzo della clausola order by  
 In XQuery, l'ordinamento viene eseguito utilizzando la clausola `order by` nell'espressione FLWOR. Le espressioni di ordinamento passate per il `order by` clausola deve restituire valori i cui tipi sono valide per il **gt** operatore. Ogni espressione di ordinamento deve restituire un singleton, ovvero una sequenza costituita da un singolo elemento. Per impostazione predefinita, l'ordinamento viene eseguito in ordine crescente. Facoltativamente, è possibile specificare un ordine crescente o decrescente per ogni espressione di ordinamento.  
  
> [!NOTE]  
>  Per i confronti di ordinamento sui valori stringa eseguiti dall'implementazione di XQuery in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono utilizzate sempre le regole di confronto binarie dei punti di codice Unicode.  
  
 La query seguente recupera tutti i numeri di telefono di un cliente specifico dalla colonna AdditionalContactInfo. I risultati vengono ordinati in base al numero di telefono.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Si noti che il [atomizzazione (XQuery)](../xquery/atomization-xquery.md) processo recupera il valore atomico del <`number`> elementi prima di passarlo a `order by`. È possibile scrivere l'espressione utilizzando il **data ()** (funzione), ma che non è necessario.  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 Questo è il risultato:  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 Anziché dichiarare gli spazi dei nomi nel prologo della query, è possibile dichiararli tramite WITH XMLNAMESPACES.  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 È inoltre possibile eseguire l'ordinamento in base al valore di attributo. Ad esempio, la query seguente consente di recuperare i nuovi elementi <`Location`> creati con gli attributi LocationID e LaborHours ordinati in base all'attributo LaborHours in ordine decrescente. Di conseguenza, vengono restituiti per primi i centri di lavorazione con il numero massimo di ore di manodopera.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Questo è il risultato:  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 Nella query seguente, i risultati vengono ordinati in base al nome dell'elemento. La query recupera le specifiche di un determinato prodotto dal catalogo prodotti. Le specifiche sono elementi figlio dell'elemento <`Specifications`>.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Tramite l'espressione `/p1:ProductDescription/p1:Specifications/*` vengono restituiti gli elementi figlio di <`Specifications`>.  
  
-   L'espressione `order by (local-name($a))` ordina la sequenza in base alla parte locale del nome dell'elemento.  
  
 Questo è il risultato:  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 I nodi in cui l'espressione di ordinamento restituisce una sequenza vuota vengono inseriti all'inizio della sequenza, come illustrato nell'esempio seguente:  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 Questo è il risultato:  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 È possibile specificare più criteri di ordinamento, come illustrato nell'esempio seguente in cui la query consente di ordinare gli elementi <`Employee`> innanzitutto in base ai valori dell'attributo Title e quindi in base ai valori dell'attributo Administrator.  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 Questo è il risultato:  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Le espressioni di ordinamento devono essere tipizzate in modo omogeneo. Per verificarlo, viene eseguito il controllo statico.  
  
-   Non è possibile controllare l'ordinamento di sequenze vuote.  
  
-   Non sono supportate le parole chiave empty least, empty greatest e collation nella clausola `order by`.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)  
  
  
