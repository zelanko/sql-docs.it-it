---
description: Identificatori (MDX)
title: Identificatori (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fe8494558f7026355cb25e1415f9269fbeb1bed3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387497"
---
# <a name="identifiers-mdx"></a>Identificatori (MDX)


  Un identificatore è il nome di un oggetto Analysis Services. Ogni oggetto può e deve avere un identificatore. inclusi cubi, dimensioni, gerarchie, livelli, membri e così via. L'identificatore di un oggetto consente di fare riferimento a tale oggetto nelle istruzioni MDX (Multidimensional Expressions).  
  
 A seconda del nome attribuito all'oggetto, l'identificatore può essere regolare o delimitato.  
  
> [!NOTE]  
>  Sia gli identificatori regolari che quelli delimitati devono contenere da 1 a 100 caratteri.  
  
## <a name="using-regular-identifiers"></a>Utilizzo di identificatori regolari  
 Un identificatore regolare è un nome di oggetto che rispetta le seguenti regole di formattazione per gli identificatori regolari. Gli identificatori regolari possono essere utilizzati con e senza delimitatori.  
  
### <a name="formatting-rules-for-regular-identifiers"></a>Regole di formattazione per gli identificatori regolari  
  
1.  Il primo carattere deve essere uno dei seguenti:  
  
    -   Una lettera definita dallo standard Unicode 2,0. ovvero i caratteri dell'alfabeto latino a-z e A-Z e i caratteri di altre lingue.  
  
    -   Il carattere di sottolineatura (_).  
  
2.  I caratteri successivi possono essere:  
  
    -   Lettere definite nello standard Unicode 2,0.  
  
    -   Numeri decimali inclusi nell'alfabeto Latino di base o in altri alfabeti nazionali.  
  
    -   Il carattere di sottolineatura (_).  
  
3.  L'identificatore non deve coincidere con una parola chiave riservata di MDX. In MDX per le parole chiave riservate non viene fatta distinzione tra maiuscole e minuscole. Per ulteriori informazioni, vedere [parole chiave riservate &#40;sintassi MDX&#41;](../mdx/reserved-keywords-mdx-syntax.md).  
  
4.  Non sono consentiti spazi incorporati o caratteri speciali.  
  
### <a name="examples-of-regular-identifiers"></a>Esempi di identificatori regolari  
 Nell'istruzione MDX seguente gli identificatori, `Measures`, `Product` e `Style`, sono conformi alle regole di formattazione per gli identificatori regolari. Per gli identificatori regolari non sono necessari delimitatori.  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 Sebbene non sia richiesto, con gli identificatori regolari è comunque possibile utilizzare delimitatori. Nell'istruzione MDX seguente gli identificatori regolari `Measures`, `Product` e `Style` sono stati correttamente delimitati tramite parentesi quadre.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>Utilizzo di identificatori delimitati  
 Gli identificatori non conformi alle regole di formattazione per gli identificatori regolari devono essere sempre delimitati da parentesi quadre ([]).  
  
> [!NOTE]  
>  I delimitatori vengono utilizzati solo con gli identificatori e non possono essere utilizzati per le parole chiave, indipendentemente dal fatto che siano o meno contrassegnate come riservate in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 È necessario utilizzare identificatori delimitati nelle situazioni seguenti:  
  
-   Quando il nome di un oggetto o parte di esso include parole riservate.  
  
     È consigliabile non utilizzare parole chiave riservate come nomi di oggetto. I database aggiornati da versioni precedenti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] possono contenere identificatori che includono parole non riservate nella versione precedente, ma ora sono riservate. Finché non sarà possibile modificare gli identificatori per tali oggetti, sarà necessario farvi riferimento tramite identificatori delimitati.  
  
-   Quando il nome di un oggetto include caratteri non elencati come identificatori qualificati.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] consente di utilizzare qualsiasi carattere della tabella codici corrente negli identificatori delimitati. L'utilizzo indiscriminato di caratteri speciali nei nomi degli oggetti potrebbe tuttavia rendere gli script e le istruzioni MDX difficili da leggere e gestire.  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>Regole di formattazione per gli identificatori delimitati  
 Il corpo di un identificatore può includere qualsiasi combinazione di caratteri della tabella codici corrente, inclusi i caratteri di delimitazione stessi. Se il corpo di un identificatore delimitato contiene caratteri di delimitazione, sarà necessaria una gestione particolare:  
  
-   Se il corpo dell'identificatore contiene solo una parentesi quadra aperta ([), non saranno necessarie operazioni di gestione aggiuntive.  
  
-   Se il corpo dell'identificatore contiene una parentesi quadra chiusa (]), sarà necessario specificare due parentesi quadre chiuse (]]).  
  
### <a name="examples-of-delimited-identifiers"></a>Esempi di identificatori delimitati  
 Nell'istruzione MDX ipotetica seguente `Sales Volume`, `Sales Cube` e `select` sono identificatori delimitati:  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 Nell'esempio successivo viene utilizzato un oggetto di nome `Total Profit [Domestic]`. Per farvi riferimento, è necessario utilizzare l'identificatore delimitato seguente:  
  
 `[Total Profit [Domestic]]]`  
  
 Si noti che la parentesi quadra aperta prima di `Domestic` non deve essere modificata per creare l'identificatore delimitato. La parentesi quadra chiusa dopo `Domestic`, invece, deve essere sostituita da due parentesi quadre chiuse.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Identificatori delimitati composti da più parti  
 Quando si utilizzano nomi di oggetti qualificati può essere necessario delimitare più di uno degli identificatori che compongono il nome dell'oggetto. Nel codice seguente, ad esempio, l'identificatore Front Brakes deve essere delimitato.  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 Nell'esempio precedente è stato delimitato anche l'identificatore Measures per illustrare la delimitazione di più di un identificatore.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento al linguaggio MDX &#40;&#41;MDX ](../mdx/mdx-language-reference-mdx.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)   
 [Elementi della sintassi MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
