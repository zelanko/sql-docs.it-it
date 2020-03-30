---
title: Tipi di dati nelle espressioni di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], data types
- data types [Integration Services], expressions
ms.assetid: c296ad10-4080-4988-8c2c-2c250f7a1884
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e2c8c8f77fd0643c503f5b817b050ff64529751
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297542"
---
# <a name="integration-services-data-types-in-expressions"></a>Tipi di dati nelle espressioni di Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'analizzatore di espressioni usa i tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La prima volta che i dati entrano nel flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] il motore del flusso di dati converte i dati di tutte le colonne in un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , mentre i dati delle colonne utilizzate da un'espressione hanno già un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Le espressioni utilizzate nelle trasformazioni Suddivisione condizionale e Colonna derivata possono fare riferimento alle colonne perché fanno parte di un flusso di dati che include dati di colonna.  
  
## <a name="variables"></a>variables  
 Nelle espressioni è possibile utilizzare anche variabili. Le variabili hanno tipo di dati Variant e, prima di valutare l'espressione, l'analizzatore di espressioni converte il tipo di dati di una variabile da un sottotipo Variant a un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per le variabili è possibile usare solo un subset dei tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per una variabile non è ad esempio possibile utilizzare un tipo di dati BLOB (Binary Large Object).  
  
 Per altre informazioni sui tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e sul mapping dei tipi di dati Variant ai tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="literals"></a>Valori letterali  
 Le espressioni possono includere anche stringhe, valori booleani e valori letterali numerici. Per altre informazioni sulla conversione di valori letterali numerici in tipi di dati numerici di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Valori letterali &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md).  
  
## <a name="strings"></a>Stringhe  
 È possibile usare DT_STR o DT_WSTR come tipo restituito di un'espressione. All'interno di un'espressione, però, è supportato solo DT_WSTR, mentre i valori DT_STR vengono convertiti in valori DT_WSTR. Questo comportamento ha diverse implicazioni quando si scrive un'espressione.  
  
-   All'interno di un'espressione usare NULL(DT_WSTR, ...) anziché NULL(DT_STR, ...). Per altre informazioni su questa funzione, vedere [NULL &#40;espressione SSIS&#41;](../../integration-services/expressions/null-ssis-expression.md).  
  
-   All'interno di un'espressione si può usare solo la funzione CAST per eseguire il cast di un valore al tipo DT_STR alla radice dell'espressione, ovvero quando viene restituito il risultato finale dell'espressione. Altrimenti usare il tipo DT_WSTR all'interno di un'espressione.  
  
 Osservare le espressioni nello screenshot seguente.  
  
 ![Tipi di dati stringa nelle espressioni SSIS](../../integration-services/expressions/media/stringsinssisexpressions.png "Tipi di dati stringa nelle espressioni SSIS")  
  
1.  La prima espressione viene eseguita senza errori perché la funzione NULL(DT_STR, ...) si trova al livello radice dell'espressione.  
  
2.  La seconda espressione viene eseguita senza errori perché usa NULL(DT_WSTR, ...).  
  
3.  La terza espressione genera un errore perché usa NULL(DT_STR, ...) all'interno dell'espressione.  
  
4.  La quarta espressione viene eseguita senza errori perché esegue il cast del risultato di NULL(DT_STR, ...) all'interno dell'espressione.  
  
     L'analizzatore di espressioni gestisce questo cast in modo intelligente ed esegue il cast a DT_WSTR, non a DT_STR, perché riconosce che l'operazione non è al livello radice dell'espressione.  
  
 Gli esempi seguenti illustrano gli effetti del cast.  
  
 ![Cast di stringhe nelle espressioni SSIS](../../integration-services/expressions/media/stringsinssisexpressions2.png "Cast di stringhe nelle espressioni SSIS")  
  
1.  Nella prima espressione il cast non è al livello radice dell'espressione. L'analizzatore di espressioni gestisce questo cast in modo intelligente ed esegue il cast a DT_WSTR, non a DT_STR. L'espressione restituisce DT_WSTR.  
  
2.  Nella seconda espressione il cast è al livello radice dell'espressione. L'espressione restituisce DT_STR.  
  
## <a name="implicit-data-conversion"></a>Conversione dati implicita  
 La conversione implicita di un tipo di dati si verifica quando l'analizzatore di espressioni converte automaticamente i dati da un tipo a un altro. Se ad esempio un valore **smallint** viene confrontato con un valore **int**, il valore **smallint** verrà implicitamente convertito in un valore **int** prima dell'esecuzione del confronto.  
  
 L'analizzatore di espressioni non è in grado di eseguire una conversione implicita dei dati se gli argomenti e gli operandi hanno tipi di dati incompatibili. Inoltre, l'analizzatore di espressioni non è in grado di convertire implicitamente alcun valore in un valore booleano. Gli argomenti e gli operandi devono essere invece convertiti esplicitamente utilizzando l'operatore cast. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Nella figura seguente viene illustrato il tipo di risultato delle conversioni implicite delle operazioni BINARY. L'intersezione di colonna e riga in questa tabella è il tipo di risultato di un'operazione binaria con operandi di tipo sinistra (Da) e destra (A).  
  
 ![Conversione implicita tra tipi di dati](../../integration-services/expressions/media/mw-dts-impl-conver-02.gif "Conversione implicita tra tipi di dati")  
  
 L'intersezione tra un valore intero con segno e un valore intero senza segno è un valore intero con segno potenzialmente maggiore di entrambi gli argomenti.  
  
 Gli operatori confrontano stringhe, date, valori booleani e altri tipi di dati. Prima che un operatore confronti due valori, l'analizzatore di espressioni esegue alcune conversioni implicite. L'analizzatore di espressioni converte sempre i valori letterali stringa nel tipo di dati DT_WSTR e i valori letterali booleani nel tipo di dati DT_BOOL. L'analizzatore di espressioni interpreta come stringhe tutti i valori racchiusi tra virgolette. I valori letterali numerici vengono convertiti in uno dei tipi di dati numeric di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!NOTE]  
>  I valori booleani sono valori logici, non numeri. Benché possano essere visualizzati come numeri in alcuni ambienti, i valori booleani non vengono archiviati come numeri e i vari linguaggi di programmazione, così come i metodi di .NET Framework, li rappresentano come valori numerici in modi diversi.  
>   
>  Le funzioni di conversione disponibili in Visual Basic, ad esempio, convertono **True** in -1, mentre il metodo **System.Convert.ToInt32** di .NET Framework converte **True** in +1. Il linguaggio delle espressioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] converte **True** in -1.  
>   
>  Per evitare errori o risultati imprevisti, è consigliabile non scrivere codice basato su particolari valori numerici per **True** e **False**. Quando possibile, è consigliabile limitare l'utilizzo delle variabili booleane ai valori logici per i quali sono progettate.  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [== &#40;uguale&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/equal-ssis-expression.md)  
  
-   [\!= &#40;diverso da&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/unequal-ssis-expression.md)  
  
-   [&#62; &#40;maggiore di&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)  
  
-   [&#60; &#40;minore di&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/less-than-ssis-expression.md)  
  
-   [&#62;= &#40;maggiore o uguale a&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)  
  
-   [&#60;= &#40;minore o uguale a&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)  
  
 Una funzione che utilizza un singolo argomento restituisce un risultato con lo stesso tipo di dati dell'argomento, con le eccezioni seguenti:  
  
-   Le funzioni DAY, MONTH e YEAR accettano un valore date e restituiscono un Integer (DT_I4).  
  
-   La funzione ISNULL accetta un'espressione con qualsiasi tipo di dati [!INCLUDE[ssIS](../../includes/ssis-md.md)] e restituisce un valore booleano (DT_BOOL).  
  
-   Le funzioni SQUARE e SQRT accettano un'espressione numerica e restituiscono un valore numerico non integrale (DT_R8).  
  
 Se gli argomenti sono dello stesso tipo, anche il risultato sarà di tale tipo. L'unica eccezione è costituita dal risultato di un'operazione binaria su due valori con tipo di dati DT_DECIMAL, che restituisce un risultato con tipo di dati DT_NUMERIC.  
  
## <a name="requirements-for-data-used-in-expressions"></a>Requisiti per i dati utilizzati nelle espressioni  
 L'analizzatore di espressioni supporta tutti i tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A seconda dell'operazione o della funzione, operandi e argomenti possono tuttavia richiedere tipi di dati specifici. L'analizzatore di espressioni impone i seguenti requisiti sul tipo di dati per i dati utilizzati nelle espressioni:  
  
-   Gli operandi usati nelle operazioni **logiche** devono restituire valori booleani. Ad esempio, ColumnA > 1&&ColumnB < 2.  
  
-   Gli operandi usati nelle operazioni **matematiche** devono restituire valori numerici. Ad esempio, 23,75 * 4.  
  
-   Gli operandi utilizzati nelle operazioni di confronto, ad esempio operazioni logiche e di uguaglianza, devono restituire tipi di dati compatibili.  
  
     Ad esempio, in una delle espressioni nell'esempio seguente viene utilizzato il tipo di dati DT_DBTIMESTAMPOFFSET:  
  
     `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30" != (DT_DBDATE)"1999-10-12"`  
  
     Il sistema converte l'espressione `(DT_DBDATE)"1999-10-12"`nel tipo di dati DT_DBTIMESTAMPOFFSET. L'esempio restituisce TRUE in quanto l'espressione convertita diventa "1999-10-12 00:00:00.000 +00:00", diverso dal valore dell'altra espressione, `(DT_DBTIMESTAMPOFFSET,3) "1999-10-11 20:34:52.123 -3:30"`.  
  
-   Gli argomenti passati a funzioni matematiche devono restituire tipi di dati numeric. A seconda della funzione o dell'operazione può essere necessario un tipo di dati numeric specifico. La funzione HEX richiede ad esempio un intero con o senza segno.  
  
-   Gli argomenti passati alle funzioni per i valori stringa devono restituire il tipo di dati character DT_STR o DT_WSTR. Ad esempio, UPPER("flower"). Alcune funzioni per i valori stringa, ad esempio SUBSTRING, richiedono argomenti Integer aggiuntivi che indicano la posizione iniziale e la lunghezza della stringa.  
  
-   Gli argomenti passati alle funzioni di data e ora devono restituire una data valida. Ad esempio, DAY(GETDATE()). Funzioni quali DATEADD richiedono un argomento Integer aggiuntivo che indica il numero di giorni che la funzione deve aggiungere alla data specificata.  
  
 Nelle operazioni che combinano un Integer a 8 byte senza segno e un Integer con segno è necessario un cast esplicito per identificare il formato del risultato. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 I risultati di molte operazioni e funzioni hanno un tipo di dati predeterminato, che può essere il tipo di dati dell'argomento o il tipo di dati a cui l'analizzatore di espressioni esegue il cast del risultato. Il risultato di un operatore OR logico (||), ad esempio, è sempre un valore booleano, mentre il risultato della funzione ABS è il tipo di dati numeric dell'argomento e il risultato di una moltiplicazione è il più piccolo tipo di dati numeric in grado di contenere il risultato senza causare una perdita di dati. Per altre informazioni sui tipi di dati dei risultati, vedere [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) e [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Usare un'espressione in un componente flusso di dati](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=746575)sul sito Web pragmaticworks.com  
  
-   Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com  
  
  
