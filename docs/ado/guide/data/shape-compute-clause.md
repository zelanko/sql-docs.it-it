---
title: Forma clausola COMPUTE | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78abac5ccbade0b686176f432618b4abc35ccab
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201790"
---
# <a name="shape-compute-clause"></a>Clausola COMPUTE di Shape
Una clausola COMPUTE di shape genera un elemento padre **Recordset**, le cui colonne sono costituiti da un riferimento all'elemento figlio **Recordset**; facoltativo colonne il cui contenuto è capitolo, nuovo, o le colonne calcolate, o risultato dell'esecuzione di funzioni di aggregazione sull'elemento figlio **Recordset** o una forma precedentemente **Recordset**; e tutte le colonne dall'elemento figlio **Recordset** elencati in facoltativo nella clausola.  
  
## <a name="syntax"></a>Sintassi  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Descrizione  
 Come indicato di seguito sono riportate le parti di questa clausola:  
  
 *child-command*  
 È costituita da uno dei seguenti:  
  
-   Un comando di query all'interno di parentesi graffe ("{}") che restituisce un elemento figlio **Recordset** oggetto. Viene eseguito il comando per il provider di dati sottostante e la relativa sintassi dipende dai requisiti del provider. Si tratterà in genere il linguaggio SQL, anche se ADO non richiede alcun linguaggio di query specifico.  
  
-   Il nome di un oggetto esistente data shaping **Recordset**.  
  
-   Un altro comando shape.  
  
-   La parola chiave nella tabella, seguita dal nome di una tabella nel provider di dati.  
  
 *child-alias*  
 Un alias utilizzato per fare riferimento il **Recordset** restituiti dal *comando figlio.* Il *figlio-alias* è obbligatorio nell'elenco delle colonne nella clausola COMPUTE e definisce la relazione tra padre e figlio **Recordset** oggetti.  
  
 *appended-column-list*  
 Un elenco in cui ogni elemento definisce una colonna nell'elemento padre generato. Ogni elemento contiene una colonna a capitoli, una nuova colonna, una colonna calcolata oppure un valore risultante da una funzione di aggregazione sull'elemento figlio **Recordset**.  
  
 *grp-field-list*  
 Un elenco di colonne padre e figlio **Recordset** gli oggetti che specifica la modalità di raggruppamento delle righe nell'elemento figlio.  
  
 Per ogni colonna di *grp-dall'elenco di campi* è una colonna corrispondente nel padre e figlio **Recordset** oggetti. Per ogni riga nell'elemento padre **Recordset**, il *elenco di campi grp* le colonne hanno valori univoci e l'elemento figlio **Recordset** fa riferimento l'elemento padre riga è costituito esclusivamente da figlio righe la cui proprietà *elenco di campi grp* colonne hanno gli stessi valori di riga padre.  
  
 Se la clausola BY viene inclusa, l'elemento figlio **Recordset**di righe verranno raggruppate in base alle colonne nella clausola COMPUTE. L'elemento padre **Recordset** conterranno una riga per ogni gruppo di righe nell'elemento figlio **Recordset**.  
  
 Se la clausola BY viene omessa, l'intero figlio **Recordset** viene considerato come un singolo gruppo e l'elemento padre **Recordset** conterranno esattamente una riga. Tale riga fa riferimento l'intero figlio **Recordset**. Omettere la clausola BY consente di calcolare le aggregazioni "totale complessivo" sull'intero figlio **Recordset**.  
  
 Ad esempio:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Indipendentemente dalla modalità padre **Recordset** viene formata (utilizzano calcolo o l'accodamento), conterrà una colonna a capitoli che viene utilizzata per metterlo a un elemento figlio **Recordset**. Se si desidera, l'elemento padre **Recordset** può anche contenere le colonne che contengono funzioni di aggregazione (SUM, MIN, MAX e così via) nelle righe figlio. Sia l'elemento padre e figlio **Recordset** possono contenere colonne che contengono un'espressione nella riga nel **Recordset**, nonché le colonne che sono elencate le nuove e inizialmente vuota.  
  
## <a name="operation"></a>Operazione  
 Il *figlio-command* è stato rilasciato il provider, che restituisce un figlio **Recordset**.  
  
 La clausola COMPUTE specifica le colonne dell'elemento padre **Recordset**, che può essere un riferimento all'elemento figlio **Recordset**, una o più aggregazioni, un'espressione calcolata o le nuove colonne. Se è presente una clausola BY, le colonne definisce inoltre vengono aggiunti all'elemento padre **Recordset**. Specifica la clausola BY come le righe dell'elemento figlio **Recordset** sono raggruppati.  
  
 Si supponga, ad esempio, che si dispone di una tabella, denominata dati demografici, che è costituito da campi di stato, città e popolazione. (Figure popolamento della tabella vengono fornite esclusivamente come esempio).  
  
|State|Città|Popolazione|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|o|Medford|200,000|  
|o|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
|WA|Tacoma|500,000|  
|o|Corvallis|300,000|  
  
 A questo punto, eseguire questo comando shape:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Questo comando apre una data shaping **Recordset** con due livelli. Livello padre è un oggetto generato **Recordset** con una colonna aggregata (`SUM(rs.population)`), una colonna che fa riferimento l'elemento figlio **Recordset** (`rs`) e una colonna per il raggruppamento figlio **Recordset** (`state`). Il livello figlio è il **Recordset** restituito dal comando di query (`select * from demographics`).  
  
 L'elemento figlio **Recordset** righe di dettaglio saranno raggruppati per stato, ma in caso contrario, in nessun ordine particolare. Vale a dire, i gruppi non sarà in ordine alfabetico o numerico. Se si desidera che l'elemento padre **Recordset** per essere ordinati, è possibile utilizzare il **Recordset ordinamento** metodo per ordinare l'elemento padre **Recordset**.  
  
 È ora possibile passare l'elemento padre aperto **Recordset** e accedere ai dettagli figlio **Recordset** oggetti. Per altre informazioni, vedere [accesso alle righe in un Recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Padre risultante e Recordset di dettagli figlio  
  
### <a name="parent"></a>Parent  
  
|SUM (rs. Basata sulla popolazione)|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|Riferimento a proprietà child1|CA|  
|1,200,000|Riferimento a child2|WA|  
|1,100,000|Riferimento a child3|o|  
  
## <a name="child1"></a>Child1  
  
|State|Città|Popolazione|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
  
## <a name="child2"></a>Child2  
  
|State|Città|Popolazione|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|Città|Popolazione|  
|-----------|----------|----------------|  
|o|Medford|200,000|  
|o|Portland|400,000|  
|o|Corvallis|300,000|  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso alle righe in un Recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Panoramica del Data Shaping](../../../ado/guide/data/data-shaping-overview.md)   
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Provider necessari per il Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Clausola APPEND per Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)   
 [Proprietà Value (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Funzioni di Visual Basic, Applications Edition](../../../ado/guide/data/visual-basic-for-applications-functions.md)
