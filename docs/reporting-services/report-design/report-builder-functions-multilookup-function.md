---
title: Funzione Multilookup (Generatore report) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 94883e68a4543c7fe98794d8b89dc38f05d2b410
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081193"
---
# <a name="report-builder-functions---multilookup-function"></a>Funzioni di Generatore report - Funzione Multilookup
  Viene restituito il set di valori di prima corrispondenza per il set di nomi specificato da un set di dati che contiene coppie nome/valore.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parametri  
 *source_expression*  
 (**VariantArray**) Espressione valutata nell'ambito corrente che specifica il set di nomi o chiavi da ricercare. Ad esempio per un parametro multivalore, `=Parameters!IDs.value`.  
  
 *destination_expression*  
 (**Variant**) Espressione valutata per ogni riga in un set di dati che specifica il nome o la chiave con cui stabilire la corrispondenza. Ad esempio: `=Fields!ID.Value`.  
  
 *result_expression*  
 (**Variant**) Espressione valutata per la riga nel set di dati in cui *source_expression* = *destination_expression*, e che specifica il valore da recuperare. Ad esempio: `=Fields!Name.Value`.  
  
 *set di dati*  
 Costante che specifica il nome di un set di dati nel report, ad esempio "Colori".  
  
## <a name="return"></a>Return  
 Restituisce **VariantArray**o **Nothing** se non viene rilevata alcuna corrispondenza.  
  
## <a name="remarks"></a>Osservazioni  
 Usare **Multilookup** per recuperare un set di valori da un set di dati per coppie nome/valore in ciascuna delle quali è presente una relazione uno-a-uno. **MultiLookup** è l'equivalente alla chiamata di **Lookup** per un set di nomi o chiavi. Per un parametro multivalore basato su identificatori di chiave primaria, ad esempio, è possibile utilizzare la funzione **Multilookup** in un'espressione in una casella di testo di una tabella per recuperare i valori associati da un set di dati non associato al parametro o alla tabella.  
  
 Tramite la funzione**Multilookup** vengono effettuate le operazioni seguenti:  
  
-   Valuta l'espressione di origine nell'ambito corrente e genera una matrice di oggetti variant.  
  
-   Per ogni oggetto nella matrice, chiama la [Funzione Lookup &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md) e aggiunge il risultato alla matrice restituita.  
  
-   Restituisce il set di risultati.  
  
 Per recuperare un singolo valore da un set di dati con coppie nome/valore per un nome specificato in cui è presente una relazione uno-a-uno, usare la [Funzione Lookup &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md). Per recuperare più valori da un set di dati con coppie nome/valore per un nome in cui è presente una relazione uno-a-molti, usare la [Funzione LookupSet &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md).  
  
 Si applicano le restrizioni seguenti:  
  
-   La funzione**Multilookup** viene valutata dopo l'applicazione di tutte le espressioni di filtro  
  
-   È supportato solo un livello di ricerca. Un'espressione di origine, destinazione o risultato non può includere un riferimento a una funzione di ricerca.  
  
-   Le espressioni di origine e di destinazione devono restituire lo stesso tipo di dati.  
  
-   Le espressioni di origine, di destinazione e di risultato non possono includere riferimenti a variabili di report o di gruppo.  
  
-   La funzione**Multilookup** non può essere utilizzata come espressione per gli elementi del report seguenti:  
  
    -   Stringhe di connessione dinamiche per un'origine dati.  
  
    -   Campi calcolati in un set di dati.  
  
    -   Parametri di query in un set di dati.  
  
    -   Filtri in un set di dati.  
  
    -   Parametri di report.  
  
    -   Proprietà Report.Language.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Esempio  
 Si supponga che un set di dati denominato "Category" contenga il campo CategoryList che è un campo con un elenco di identificatori di categoria separato da virgole, ad esempio, "2, 4, 2, 1".  
  
 Nel set di dati CategoryNames sono contenuti l'identificatore e il nome della categoria, come illustrato nella tabella seguente.  
  
|ID|Nome|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|Componenti|  
  
 Per cercare i nomi che corrispondono all'elenco di identificatori, utilizzare **Multilookup**. È necessario innanzitutto suddividere l'elenco in una matrice di stringhe, chiamare la funzione **Multilookup** per recuperare i nomi di categoria e concatenare i risultati in una stringa.  
  
 L'espressione seguente, se inserita in una casella di testo in un'area dati associata al set di dati Category, visualizza "Bikes, Components, Bikes, Accessories":  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>Esempio  
 Si supponga che un set di dati ProductColors contenga un campo dell'identificatore del colore ColorID e un campo del valore del colore Color, come illustrato nella tabella seguente.  
  
|ColorID|Colore|  
|-------------|-----------|  
|1|Rosso|  
|2|Blu|  
|3|Green|  
  
 Si supponga che il parametro multivalore *MyColors* non sia associato a un set di dati per i valori disponibili. I valori predefiniti per il parametro sono impostati su 2 e 3. L'espressione seguente, se inserita in una casella di testo all'interno di una tabella, consente di concatenare i valori selezionati per il parametro in un elenco delimitato da virgole e visualizza "Blue, Green".  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
