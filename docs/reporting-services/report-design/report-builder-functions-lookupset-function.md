---
title: Funzione LookupSet (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b4de3e21a214a9894f93b8aa2fcd8fd8c6328eb
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577405"
---
# <a name="report-builder-functions---lookupset-function"></a>Funzioni di Generatore report - Funzione LookupSet
  Viene restituito il set di valori corrispondenti per il nome specificato da un set di dati contenente coppie nome/valore.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parametri  
 *source_expression*  
 (**Variant**) Espressione valutata nell'ambito corrente che specifica il nome o la chiave da ricercare. Ad esempio, `=Fields!ID.Value`.  
  
 *destination_expression*  
 (**Variant**) Espressione valutata per ogni riga in un set di dati che specifica il nome o la chiave con cui stabilire la corrispondenza. Ad esempio, `=Fields!CustomerID.Value`.  
  
 *result_expression*  
 (**Variant**) Espressione valutata per la riga nel set di dati in cui *source_expression* = *destination_expression*, e che specifica il valore da recuperare. Ad esempio, `=Fields!PhoneNumber.Value`.  
  
 *set di dati*  
 Costante che specifica il nome di un set di dati nel report, ad esempio "InformazioniDiContatto".  
  
## <a name="return"></a>Return  
 Restituisce **VariantArray**o **Nothing** se non viene rilevata alcuna corrispondenza.  
  
## <a name="remarks"></a>Remarks  
 Usare **LookupSet** per recuperare un set di valori dal set di dati specificato per una coppia nome/valore in cui è presente una relazione uno-a-molti. Per un identificatore di cliente in una tabella, ad esempio, è possibile usare la funzione **LookupSet** per recuperare tutti i numeri di telefono relativi al cliente da un set di dati non associato all'area dati.  
  
 Tramite la funzione**LookupSet** vengono effettuate le operazioni seguenti:  
  
-   Valuta l'espressione di origine nell'ambito corrente.  
  
-   Valuta l'espressione di destinazione per ogni riga del set di dati specificato dopo che sono stati applicati i filtri, in base alle regole di confronto del set di dati specificato.  
  
-   Per ogni corrispondenza dell'espressione di origine e di destinazione, valuta l'espressione di risultato per quella riga nel set di dati.  
  
-   Restituisce il set di valori dell'espressione di risultato.  
  
 Per recuperare un singolo valore da un set di dati con coppie nome/valore per un nome specificato in cui è presente una relazione uno-a-uno, usare la [Funzione Lookup &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md). Per chiamare la funzione **Lookup** per un set di valori, usare la [Funzione Multilookup &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 Sono previste le restrizioni seguenti:  
  
-   La funzione**LookupSet** viene valutata dopo l'applicazione di tutte le espressioni di filtro.  
  
-   È supportato solo un livello di ricerca. Un'espressione di origine, destinazione o risultato non può includere un riferimento a una funzione di ricerca.  
  
-   Le espressioni di origine e di destinazione devono restituire lo stesso tipo di dati.  
  
-   Le espressioni di origine, di destinazione e di risultato non possono includere riferimenti a variabili di report o di gruppo.  
  
-   La funzione**LookupSet** non può essere usata come espressione per gli elementi del report seguenti:  
  
    -   Stringhe di connessione dinamiche per un'origine dati.  
  
    -   Campi calcolati in un set di dati.  
  
    -   Parametri di query in un set di dati.  
  
    -   Filtri in un set di dati.  
  
    -   Parametri di report.  
  
    -   Proprietà Report.Language.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, si supponga che la tabella sia associata a un set di dati che include un identificatore del territorio di vendita TerritoryGroupID. Un set di dati separato denominato "Stores" contiene l'elenco di tutti i negozi di un territorio e include l'ID dell'identificatore del territorio e il nome del negozio StoreName.  
  
 Nell'espressione seguente, **LookupSet** confronta il valore TerritoryGroupID con ID per ogni riga nel set di dati denominato "Stores". Per ogni corrispondenza, il valore del campo StoreName per quella riga viene aggiunto al set di risultati.  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
## <a name="example"></a>Esempio  
 Poiché tramite **LookupSet** viene restituita una raccolta di oggetti, non è possibile visualizzare direttamente l'espressione di risultato in una casella di testo. È possibile concatenare il valore di ogni oggetto nella raccolta come stringa.  
  
 Usare la funzione [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] Join **di** per creare una stringa delimitata da un set di oggetti. Usare una virgola come separatore per combinare gli oggetti in un'unica riga. In alcuni renderer, è possibile usare un avanzamento riga di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] (`vbCrLF`) come separatore per elencare ogni valore su una nuova riga.  
  
 L'espressione seguente, quando viene usata come proprietà Value per una casella di testo, usa **Join** per creare un elenco.  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
## <a name="example"></a>Esempio  
 Per caselle di testo che eseguono il rendering solo poche volte, è possibile scegliere di aggiungere un codice personalizzato per generare HTML per visualizzare i valori in una casella di testo. HTML in una casella di testo richiede altri processi di elaborazione, pertanto non è consigliabile per una casella di testo che viene sottoposta a rendering molte volte.  
  
 Copiare le seguenti funzioni di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] in un blocco di codice di una definizione del report. **MakeList** accetta la matrice di oggetti restituita in *result_expression* e compila un elenco non ordinato usando tag HTML. **Length** restituisce il numero di elementi della matrice di oggetti.  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
## <a name="example"></a>Esempio  
 Per generare HTML, è necessario chiamare la funzione. Incollare l'espressione seguente nella proprietà Value per la casella di testo e impostare il tipo di markup per il testo su HTML. Per altre informazioni, vedere [Aggiungere codice HTML a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md).  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
