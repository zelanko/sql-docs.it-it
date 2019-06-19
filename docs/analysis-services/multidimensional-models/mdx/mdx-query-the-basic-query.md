---
title: La Query MDX di base (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61975b6b24cda25454d10eb1eeb5b452cad0f1ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025550"
---
# <a name="mdx-query---the-basic-query"></a>Query MDX - Query di base
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  La query MDX (Multidimensional Expressions) di base è la query utilizzata più di frequente: l'istruzione SELECT in MDX. Se si conosce la sintassi dell'istruzione MDX SELECT, si sa creare una semplice query tramite questa istruzione e si capisce perché in un'istruzione SELECT è necessario specificare un set di risultati, si avrà la padronanza dell'utilizzo di MDX per l'esecuzione di query in dati multidimensionali.  
  
## <a name="specifying-a-result-set"></a>Impostazione di un set di risultati  
 In MDX l'istruzione SELECT specifica un set di risultati contenente un subset dei dati multidimensionali di un cubo che sono stati restituiti. Per specificare un set di risultati, una query MDX deve contenere le informazioni seguenti:  
  
-   Numero di assi che devono essere inclusi nel set di risultati. In una query MDX è possibile specificare un massimo di 128 assi.  
  
-   Set di membri o tuple da includere in ogni asse della query MDX.  
  
-   Il nome del cubo che definisce il contesto della query MDX.  
  
-   Set di membri o tuple da includere nell'asse di sezionamento. Per altre informazioni sugli assi di sezionamento e della query, vedere [Restrizione della query con gli assi della query e di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md).  
  
 Per identificare gli assi della query, il cubo su cui verrà eseguita la query e l'asse di sezionamento, l'istruzione MDX deve utilizzare le clausole seguenti:  
  
-   Clausola SELECT che determina gli assi della query di un'istruzione MDX SELECT. Per altre informazioni sulla formulazione degli assi della query in una clausola SELECT, vedere [Impostazione del contenuto di un asse della query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   Clausola FROM che determina il cubo su cui eseguire la query. Per altre informazioni sulla clausola FROM, vedere [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
-   Clausola WHERE facoltativa che determina i membri o le tuple da utilizzare nell'asse di sezionamento per limitare i dati restituiti. Per altre informazioni sulla formulazione di un asse di sezionamento in una clausola WHERE, vedere [Impostazione del contenuto di un asse di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
> [!NOTE]  
>  Per altre informazioni sulle varie clausole dell'istruzione SELECT, vedere [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="select-statement-syntax"></a>Sintassi dell'istruzione SELECT  
 La sintassi seguente illustra un'istruzione SELECT di base in cui sono specificate le clausole SELECT, FROM e WHERE:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 L'istruzione MDX SELECT supporta sintassi facoltativa, ad esempio la parola chiave WITH, l'utilizzo di funzioni MDX per la creazione di membri calcolati per l'inclusione di un asse o un asse di sezionamento e la restituzione dei valori di proprietà di celle specifiche come parte della query. Per altre informazioni sull'istruzione MDX SELECT, vedere [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>Confronto tra la sintassi dell'istruzione MDX SELECT e SQL  
 Il formato della sintassi di un'istruzione MDX SELECT è simile alla sintassi SQL. Sussistono tuttavia diverse differenze essenziali:  
  
-   La sintassi MDX separa i set racchiudendo le tuple o i membri tra parentesi graffe, ovvero tra i caratteri { e }. Per altre informazioni sulla sintassi per membri, tuple e set, vedere [Uso di membri, tuple e set &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
-   Le query MDX possono includere 0, 1, 2 e fino a 128 assi della query nell'istruzione SELECT. Ciascun asse si comporta esattamente allo stesso modo, a differenza di SQL in cui sussistono differenze significative tra il comportamento delle righe e il comportamento delle colonne di una query.  
  
-   In modo analogo a una query SQL, la clausola FROM indica l'origine dei dati per la query MDX. La clausola FROM di MDX tuttavia è limitata a un solo cubo. Le informazioni di altri cubi possono essere recuperate per singoli valori tramite la funzione LookupCube.  
  
-   La clausola WHERE descrive l'asse di sezionamento in una query MDX e opera come un asse aggiuntivo invisibile nella query, sezionando i valori visualizzati nelle celle nel set di risultati. Diversamente dalla clausola SQL WHERE, questa clausola non influisce direttamente su quanto visualizzato nell'asse delle righe della query. La funzionalità della clausola SQL WHERE è disponibile tramite altre funzioni MDX, ad esempio la funzione FILTER.  
  
## <a name="select-statement-example"></a>Esempio di istruzione SELECT  
 Nell'esempio seguente viene illustrata una query MDX di base in cui è utilizzata l'istruzione SELECT. Questa query restituisce un set di risultati contenente le vendite e le imposte relative agli anni 2002 e 2003 per le aree di vendita della zona sudoccidentale.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Nell'esempio la query definisce le informazioni del set di risultati seguenti:  
  
-   La clausola SELECT imposta le assi della query come membri Sales Amount e Tax Amount della dimensione Measures e i membri 2002 e 2003 della dimensione Date.  
  
-   La clausola FROM indica che l'origine dei dati è il cubo Adventure Works.  
  
-   La clausola WHERE definisce l'asse di sezionamento come membro Southwest della dimensione Sales Territory.  
  
 Si noti che nella query di esempio sono utilizzati anche gli alias di asse COLUMNS e ROWS. In alternativa è possibile specificare la posizione ordinale degli assi. Nell'esempio seguente viene illustrata la stessa query MDX in cui è tuttavia specificata la posizione ordinale dei vari assi:  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Per esempi più dettagliati, vedere [Impostazione del contenuto di un asse della query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)e [Impostazione del contenuto di un asse di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
