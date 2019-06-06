---
title: Filtra proprietà | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d68f0e74e4bbfb275cbe23641c72eca4c941559
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697970"
---
# <a name="filter-property"></a>Proprietà Filter
Indica un filtro per i dati in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti

Imposta o restituisce un **Variant** valore, che può contenere uno dei seguenti elementi:  
  
-   **Stringa di criteri:** Una stringa costituita da uno o più clausole singoli concatenate **AND** oppure **OR** operatori.  
  
-   **Matrice di segnalibri:** Matrice di segnalibro univoco che puntano ai record in più valori di **Recordset** oggetto.  
  
-   Oggetto [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) valore.  
  
## <a name="remarks"></a>Note

Usare la **filtro** proprietà allo schermo in modo selettivo i record in un **Recordset** oggetto. Filtrati **Recordset** diventa il cursore corrente. Altre proprietà che restituiscono valori basati sull'oggetto corrente **cursore** interessati, ad esempio [proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ Proprietà RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), e [proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Impostando il **filtro** proprietà su un nuovo valore specifico del record corrente è passata al primo record che soddisfano il nuovo valore.
  
La stringa di criteri è costituita da clausole nel formato *valore dell'operatore FieldName* (ad esempio, `"LastName = 'Smith'"`). È possibile creare clausole composte da singole clausole con l'operatore di concatenazione **AND** (ad esempio, `"LastName = 'Smith' AND FirstName = 'John'"`) o **OR** (ad esempio, `"LastName = 'Smith' OR LastName = 'Jones'"`). Per le stringhe di criteri, usare le linee guida seguenti:

-   *FieldName* deve essere un nome di campo valido dal **Recordset**. Se il nome del campo contiene spazi, è necessario racchiudere il nome nelle parentesi quadre.  
  
-   Operatore deve essere uno dei seguenti: \<, >, \<=, > =, <>, =, o **, ad esempio**.  
  
-   Valore è quello con cui si confronteranno i valori di campo (ad esempio, 'Smith', #, #8/24/95 12,345 o $50,00). Usare le virgolette singole con segni di cancelletto (#) con date e stringhe. Per i numeri, è possibile utilizzare la notazione scientifica i separatori decimali e simboli del dollaro. Se l'operatore **, ad esempio**, valore possa usare caratteri jolly. Solo l'asterisco (*) e segno di percentuale (%) i caratteri jolly sono consentiti e devono essere l'ultimo carattere nella stringa. Valore non può essere null.  
  
> [!NOTE]
>  Per includere le virgolette singole (') nel valore del filtro, usare due virgolette singole per rappresentare uno. Ad esempio, per filtrare in base, la stringa di criteri deve essere `"col1 = 'O''Malley'"`. Per includere virgolette all'inizio e alla fine del valore del filtro, racchiudere la stringa con segni di cancelletto (#). Ad esempio, per filtrare '1', la stringa di criteri deve essere `"col1 = #'1'#"`.  
  
-   Non vi è alcuna priorità tra AND e o. Le clausole possono essere raggruppate all'interno delle parentesi. Tuttavia, non è possibile raggruppare le clausole unite mediante l'operatore OR e quindi aggiungere il gruppo a un'altra clausola con l'operatore AND, come nel frammento di codice seguente:  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   In alternativa, è possibile creare il filtro seguente:  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   In un **, ad esempio** clausola, è possibile usare un carattere jolly all'inizio e alla fine del modello. Ad esempio, è possibile usare `LastName Like '*mit*'`. O con **, ad esempio** è possibile usare un carattere jolly solo alla fine del modello. Ad esempio `LastName Like 'Smit*'`.  
  
 Le costanti del filtro rendono più semplice risolvere singoli record conflitti durante la modalità di aggiornamento batch in quanto consente di visualizzare, ad esempio, solo i record che sono stati interessati durante l'ultima [metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) chiamata al metodo.  
  
Impostando il **filtro** proprietà stessa potrebbe non riuscire a causa di un conflitto con i dati sottostanti. Ad esempio, questo errore può verificarsi quando un record è già stato eliminato da un altro utente. In tal caso, il provider restituisce avvisi per i [raccolta di errori (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta, ma non arrestano l'esecuzione del programma. Solo se sono presenti conflitti in tutti i record richiesti, si verifica un errore in fase di esecuzione. Usare la [proprietà Status (Recordset ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà per individuare i record con conflitti.  
  
Impostando il **filtro** proprietà in una stringa di lunghezza zero ("") ha lo stesso effetto utilizzando il **adFilterNone** costante.
  
Ogni volta che il **filtro** è impostata, sposta la posizione corrente per il primo record in subset filtrato dei record nelle **Recordset**. Analogamente, quando la **filtro** proprietà è deselezionata, la posizione del record corrente viene spostato sul primo record nelle **Recordset**.

Si supponga che un **Recordset** viene applicato un filtro basato su un campo di un tipo variant, ad esempio il tipo sql_variant. Un errore (DISP_E_TYPEMISMATCH o 80020005) si verifica quando i sottotipi dei valori di campo e il filtro utilizzati nella stringa di criteri non corrispondono. Si supponga ad esempio:

- Oggetto **Recordset** oggetto (rs) contiene una colonna (C) di tipo sql_variant.
- E un campo di questo articolo è stato assegnato un valore pari a 1 del tipo I4. La stringa di criteri è impostata su `rs.Filter = "C='A'"` sul campo.

Questa configurazione genera l'errore durante la fase di esecuzione. Tuttavia, `rs.Filter = "C=2"` applicato sullo stesso campo non produrrà un errore. E il campo è escludere tramite filtro i set di record corrente.

Vedere le [proprietà Bookmark (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) proprietà per una spiegazione dei valori di segnalibro da cui è possibile compilare una matrice da usare con la proprietà di filtro.

Solo i filtri sotto forma di stringhe di criteri influiscono sul contenuto di un persistente **Recordset**. Un esempio di una stringa di criteri è `OrderDate > '12/31/1999'`. I filtri creati con una matrice di segnalibri o usando un valore compreso il **FilterGroupEnum**, non influiscono sul contenuto della classe resa persistente **Recordset**. Queste regole si applicano a Recordset creato con cursori sul lato client o lato server.
  
> [!NOTE]
>  Quando il flag adFilterPendingRecords si applica a un filtrato e modificata **Recordset** in modalità di aggiornamento batch, il risultante **Recordset** è vuoto se il filtro è basato sul campo di chiave di un chiave singola tabella e la modifica è stata apportata ai valori di campo chiave. I risultanti **Recordset** sarà non vuoto se viene soddisfatta una delle istruzioni seguenti:  
  
-   Il filtro è basato sui campi non chiave in una tabella di chiave singola.  
  
-   Il filtro è basato su tutti i campi in una tabella a più chiavi.  
  
-   Sono state apportate modifiche nei campi non chiave in una tabella di chiave singola.  
  
-   Sono state apportate modifiche su tutti i campi in una tabella a più chiavi.  
  
Nella tabella seguente sono riepilogati gli effetti delle **adFilterPendingRecords** in diverse combinazioni di filtri e le modifiche. La colonna a sinistra mostra le modifiche possibili. È possibile apportare modifiche in uno qualsiasi dei campi non chiave, il campo chiave in una tabella di chiave singola, o in uno qualsiasi dei campi chiave in una tabella a più chiavi. La prima riga Mostra il criterio di filtro. Filtro può essere basato su uno dei campi non chiave, il campo chiave in una tabella di chiave singola, o uno qualsiasi dei campi chiave in una tabella a più chiavi. Le celle intersecate mostrano i risultati. Oggetto **+** segno significa che tale applicazione **adFilterPendingRecords** comporterà una non vuota **Recordset**. Oggetto **-** meno (-) indica che un oggetto vuoto **Recordset**.  
  
||Chiavi non|Singola chiave|Più chiavi|
|-|--------------|----------------|-------------------|
|**Chiavi non**|+|+|+|
|**Singola chiave**|+|-|N/D|
|**Più chiavi**|+|N/D|+|
|||||
  
## <a name="applies-to"></a>Si applica a

[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche

[Esempio di proprietà RecordCount (VB) e di filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[esempio di proprietà RecordCount (VC + +) e filtro](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
 [Ottimizzare proprietà dinamica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
