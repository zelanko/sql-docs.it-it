---
title: Che cosa sono le novità di SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 711b577b737b48012e1bed0a52ba599cf17b3d8f
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685758"
---
# <a name="whats-new-in-sql-server-2017-analysis-services"></a>Che cosa sono le novità di SQL Server 2017 Analysis Services
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

SQL Server 2017 Analysis Services vedere alcuni dei più importanti miglioramenti rispetto a SQL Server 2012. Dopo il successo della modalità tabulare (introdotta in SQL Server 2012 Analysis Services), questa versione, i modelli tabulari rende più potente che mai.

Modalità multidimensionale e Power Pivot per la modalità SharePoint sono graffatura per molte distribuzioni di Analysis Services. Nel ciclo di vita del prodotto di Analysis Services, queste modalità sono avanzate. Non sono presenti nuove funzionalità per una delle modalità seguenti in questa versione. Tuttavia, sono inclusi correzioni di bug e miglioramenti delle prestazioni.

Le funzionalità descritte di seguito sono inclusi in SQL Server 2017 Analysis Services. Ma per poter sfruttare i vantaggi di essi, è necessario usare anche le versioni più recenti di [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) e [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS). SSDT e SSMS vengono aggiornati ogni mese con le funzionalità nuove e migliorate che in genere coincidano con nuove funzionalità di SQL Server.  

Sebbene sia importante conoscere tutte le nuove funzionalità, è anche importante sapere ciò che viene deprecato e non più utilizzate in questa versione e le versioni future. Assicurarsi di consultare [compatibilità con le versioni precedenti (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md).

Diamo un'occhiata ad alcune delle principali nuove funzionalità in questa versione.

## <a name="1400-compatibility-level-for-tabular-models"></a>Livello di compatibilità 1400 per i modelli tabulari
  Per usufruire delle numerose nuove funzionalità e le funzionalità descritte in questo caso, i modelli tabulari nuovi o esistenti devono essere impostati o aggiornati a livello di compatibilità 1400. Non è possibile distribuire i modelli con livello di compatibilità 1400 in SQL Server 2016 SP1 o versioni precedenti né effettuare il downgrade a livelli di compatibilità inferiori. Per altre informazioni, vedere [a livello di compatibilità per i modelli tabulari di Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).
  
In SSDT è possibile selezionare il nuovo livello di compatibilità 1400 durante la creazione di nuovi progetti di modelli tabulari. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


Per aggiornare un modello tabulare esistente in SSDT, in Esplora soluzioni fare doppio clic su **Model. bim**e quindi in **delle proprietà**, impostare il **a livello di compatibilità** proprietà  **SQL Server 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

È importante tenere a mente quando si aggiorna un modello esistente a 1400, è possibile effettuare il downgrade. Assicurarsi di mantenere un backup del database modello tabulari 1200.

## <a name="modern-get-data-experience"></a>Funzionalità moderna per il recupero di dati
Se si desidera importare dati da origini dati in modelli tabulari del server, SQL Server Data Tools (SSDT) introduce il moderno **recupera dati** una migliore esperienza per i modelli a livello di compatibilità 1400. Questa nuova funzionalità si basa su una funzionalità simile in Power BI Desktop e Microsoft Excel 2016. L'esperienza di recupero dati moderna offre funzionalità di mashup dei dati e trasformazione dei dati un'enorme utilizzando il generatore delle query di ottenere dati e le espressioni M.

L'esperienza di recupero dati moderna offre supporto per un'ampia gamma di origini dati. In futuro, gli aggiornamenti includono il supporto per ancora di più.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 Un'interfaccia utente intuitiva e potente consente di selezionare i dati e le funzionalità di trasformazione/mashup dei dati più facile che mai.

![Mashup avanzate](../analysis-services/media/as-get-data-advanced.png)


Il moderno recupero di dati e le funzionalità di mashup M non si applicano a upraded i modelli tabulari esistenti dal livello di compatibilità 1200 per 1400. La nuova esperienza si applica solo ai nuovi modelli creati a livello di compatibilità 1400.

## <a name="encoding-hints"></a>Hint di codifica
Questa versione introduce gli hint di codifica, una funzionalità avanzata consente di ottimizzare l'elaborazione (aggiornamento dei dati) di modelli tabulari di grandi dimensioni in memoria. Per comprendere meglio la codifica, vedere [sulle prestazioni di ottimizzazione dei modelli tabulari in SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) white paper per comprendere meglio la codifica.

* Valore di codifica offre le prestazioni delle query migliori per le colonne che in genere vengono usate solo per le aggregazioni.

* La codifica hash è preferita per le chiavi esterne e colonne group by (spesso valori di tabella delle dimensioni). Colonne di tipo stringa sono sempre hash con codificata.

Le colonne numeriche possono usare uno di questi metodi di codifica. Quando Analysis Services inizia l'elaborazione di una tabella, se una tabella è vuota (con o senza partizioni) o viene eseguita un'operazione di elaborazione di tabella completa, i valori di esempi vengono forniti per ogni colonna numerica determinare se applicare valore o la codifica hash . Per impostazione predefinita, la codifica di valore viene scelto quando l'esempio di valori distinct nella colonna è abbastanza grande: in caso contrario, la codifica hash in genere fornisce una migliore compressione. È possibile che Analysis Services modificare il metodo di codifica dopo che la colonna è parzialmente elaborata ulteriormente le informazioni sulla distribuzione dei dati in base e riavviare il processo di codifica. Tuttavia, si aumenta il tempo di elaborazione ed è inefficiente. Il white paper sulla regolazione delle prestazioni viene illustrata la nuova codifica in modo più dettagliato e viene descritto come rilevare usando SQL Server Profiler.

Hint di codifica consente i creatori di modelli specificare una preferenza per il metodo di codifica specificato conoscenza pregressa di profiling dei dati e/o in risposta a nuova codifica gli eventi di traccia. Poiché l'aggregazione in colonne con codifica hash è più lento rispetto a quanto applicati alle colonne di valore codificato, codifica del valore potrebbe essere specificata come hint per tali colonne. Non è garantito che la preferenza viene applicata. È un hint anziché un'impostazione. Per specificare un hint di codifica, impostare la proprietà EncodingHint sulla colonna. I valori possibili sono "Default", "Value" e "Hash". Il frammento seguente di metadati basati su JSON nel file Model. bim Specifica valore di codifica per la colonna Sales Amount.

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

## <a name="ragged-hierarchies"></a>Gerarchie incomplete
Nei modelli tabulari è possibile modellare le gerarchie padre-figlio. Le gerarchie con un numero di livelli diverso sono spesso definite gerarchie incomplete. Per impostazione predefinita, le gerarchie di questo tipo presentano spazi vuoti nei livelli al di sotto del figlio minore. Di seguito è riportato un esempio di una gerarchia incompleta in un organigramma:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

In questa versione è stata introdotta la proprietà **Hide Members** (Nascondi membri). È possibile impostare la proprietà **Hide Members** (Nascondi membri) relativa a una gerarchia su **Hide blank members**(Nascondi membri vuoti).

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > I membri vuoti nel modello sono rappresentati da un valore vuoto di DAX, non da una stringa vuota.

Quando la proprietà è impostata su **Hide blank members**(Nascondi membri vuoti) e il modello è distribuito, nei client di creazione report come Excel viene visualizzata una versione più leggibile della gerarchia.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)


## <a name="detail-rows"></a>Righe di dettaglio
È ora possibile definire un set di righe personalizzato che contribuisce a un valore di misura. La funzionalità Righe di dettaglio è paragonabile all'azione di drill-through predefinita nei modelli multidimensionali. Ciò consente agli utenti finali di visualizzare le informazioni in modo più dettagliato rispetto al livello aggregato. 

La tabella pivot seguente mostra i valori annuali di Internet Total Sales del modello tabulare di esempio di AdventureWorks. Per visualizzare le righe di dettaglio è possibile fare clic con il pulsante destro del mouse su una cella con un valore aggregato della misura e quindi scegliere **Mostra dettagli** .

![AS_Show_Details](../analysis-services/media/as-show-details.png)

Per impostazione predefinita, vengono visualizzati i dati associati nella tabella Internet Sales. Questo comportamento limitato spesso non è significativo per l'utente perché la tabella può non includere le colonne necessarie per visualizzare informazioni utili, ad esempio il nome del cliente e i dati relativi agli ordini. Con Righe di dettaglio, è possibile specificare una proprietà **Detail Rows Expression** (Espressione righe di dettaglio) per le misure.

#### <a name="detail-rows-expression-property-for-measures"></a>Proprietà Detail Rows Expression (Espressione righe di dettaglio) per le misure
La proprietà **Detail Rows Expression** (Espressione righe di dettaglio) per le misure consente agli autori di modelli di personalizzare le colonne e le righe restituite all'utente finale.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

Il [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) funzione DAX viene comunemente utilizzata in un'espressione di righe di dettaglio. L'esempio seguente definisce le colonne da restituire per le righe della tabella Internet Sales nel modello tabulare di esempio di AdventureWorks:

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

Con la proprietà definita e il modello distribuito, quando l'utente seleziona **Mostra dettagli**viene restituito un set di righe personalizzato che rispetta automaticamente il contesto del filtro della cella selezionata. In questo esempio vengono visualizzate solo le righe per il valore 2010:

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>Proprietà Default Detail Rows Expression (Espressione predefinita righe di dettaglio) per le tabelle
Oltre alle misure, anche le tabelle hanno una proprietà per definire un'espressione di righe di dettaglio. La proprietà **Default Detail Rows Expression** (Espressione predefinita righe di dettaglio) viene usata come impostazione predefinita per tutte le misure all'interno della tabella. Le misure che non è definita un'espressione eredita l'espressione dalla tabella e visualizzare il set di righe definito per la tabella. In questo modo il riutilizzo di espressioni e nuove misure aggiunte alla tabella in un secondo momento automaticamente eredita l'espressione.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>Funzione DAX DETAILROWS
In questa versione è inclusa una nuova funzione DAX `DETAILROWS` che restituisce il set di righe definito dall'espressione delle righe di dettaglio. Funziona in modo simile all'istruzione `DRILLTHROUGH` in MDX, che è anche compatibile con le espressioni delle righe di dettaglio definite nei modelli tabulari.

La query DAX seguente restituisce il set di righe definito dall'espressione delle righe di dettaglio per la misura o la relativa tabella. Se non è definita alcuna espressione, vengono restituiti i dati per la tabella Internet Sales perché è quella che contiene la misura.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>Sicurezza a livello di oggetto
Questa versione introduce [sicurezza a livello di oggetto](../analysis-services/tabular-models/object-level-security.md) per tabelle e colonne. Oltre a limitare l'accesso ai dati di tabelle e colonne, è possibile proteggere i nomi di tabelle e colonne sensibili. Ciò consente di impedire a un utente malintenzionato di individuare una tabella esistente.

Sicurezza a livello di oggetto deve essere impostata usando i metadati basati su JSON, TMSL Tabular Model Scripting Language () o modello a oggetti tabulare (TOM). 

Ad esempio, il codice seguente consente di proteggere la tabella Product del modello tabulare di esempio di AdventureWorks impostando la proprietà **MetadataPermission** della classe **TablePermission** su **None**.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

## <a name="dynamic-management-views-dmvs"></a>Viste a gestione dinamica (DMV)
[Viste a gestione dinamica](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) sono le query in SQL Server Profiler che restituiscono informazioni sulle operazioni del server locale e lo stato del server.
Questa versione include miglioramenti [viste a gestione dinamica](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) per i modelli tabulari ai livelli di compatibilità 1200 e 1400.

[DISCOVER_CALC_DEPENDENCY](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset) ora funziona con i modelli tabulari 1200 e 1400. I modelli tabulari 1400 mostrano le dipendenze tra le partizioni M, le espressioni M e origini dati strutturate. Per altre informazioni, vedere la [blog di Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/).

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset) miglioramenti sono inclusi per questa DMV, che viene utilizzata da vari strumenti client per indicare misura dimensionalità. Ad esempio, la funzionalità di esplorazione nelle tabelle Pivot di Excel consente all'utente di cross-drill a dimensioni correlate alle misure selezionate. Questa versione corregge le colonne della cardinalità, che precedentemente venivano visualizzati valori non corretti.

## <a name="dax-enhancements"></a>Miglioramenti apportati a DAX
Questa versione include il supporto per funzionalità e nuove funzioni DAX. Per sfruttare i vantaggi, è necessario usare la versione più recente di SSDT. Per altre informazioni, vedere [funzioni DAX nuovo](https://msdn.microsoft.com/library/mt704075.aspx).

Una delle parti più importanti della nuova funzionalità del linguaggio DAX è il nuovo [operatore IN / funzione CONTAINSROW](https://msdn.microsoft.com/library/mt842621.aspx) per le espressioni DAX. È simile all'operatore [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) comunemente usato per specificare più valori in una clausola `WHERE` .

In precedenza, era pratica comune specificare filtri con più valori usando l'operatore logico `OR` , come illustrato nell'espressione di misura seguente:

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

Questo processo viene semplificato dall'operatore `IN` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

In questo caso, l'operatore `IN` fa riferimento a una tabella a colonna singola con 3 righe, una per ogni colore specificato. Si noti che nella sintassi del costruttore della tabella vengono usate le parentesi graffe.

Dal punto di vista funzionale, l'operatore `IN` equivale alla funzione `CONTAINSROW` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

L'operatore `IN` può essere usato in modo efficace anche con i costruttori di tabella. Ad esempio, per la misura seguente è specificato un filtro in base alle combinazioni di colore e categoria del prodotto:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

Se si usa il nuovo operatore `IN` , l'espressione di misura precedente è formulata nel modo seguente:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```

## <a name="additional-improvements"></a>Altri miglioramenti
Oltre a tutte le nuove funzionalità, Analysis Services, SSDT e SSMS includono anche i miglioramenti seguenti:

* Riutilizzo di gerarchia e di colonna rilevate nelle posizioni più utile nell'elenco di campi di Power BI.
* Relazioni di date per creare facilmente relazioni con dimensioni di data basate sui campi Data.
* Opzione di installazione predefinita di Analysis Services è ora per la modalità tabulare.
* Nuove origini dati recupera dati (Power Query).
* Editor DAX per SSDT.
* Supportano di origini dati DirectQuery esistenti per milione di query.
* Miglioramenti di SQL Server Management Studio, ad esempio la visualizzazione, modifica e il supporto per origini dati strutturate di script.



## <a name="see-also"></a>Vedere anche
[Note sulla versione di SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)   
[Novità di SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
