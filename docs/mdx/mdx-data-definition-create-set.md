---
title: Istruzione CREATE SET (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f8d522f7832a280aa8b280bbe912640b566974a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893747"
---
# <a name="mdx-data-definition---create-set"></a>Definizione dei dati MDX - CREATE SET


  Crea un set denominato con ambito sessione per il cubo corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome del cubo.  
  
 *Set_Name*  
 Espressione stringa valida che specifica il nome del set denominato che viene creato.  
  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Property_Name*  
 Stringa valida che fornisce il nome di una proprietà del set.  
  
 *Property_Value*  
 Espressione scalare valida che definisce il valore della proprietà del set.  
  
## <a name="remarks"></a>Osservazioni  
 Un set denominato è un set di membri di dimensioni, o un'espressione che definisce un set, che è possibile creare per un riutilizzo successivo. Un set denominato, ad esempio, consente di definire un set di membri di dimensioni costituito dal set dei primi dieci punti vendita per fatturato. Questo set può essere definito in modo statico o tramite una funzione come il [conteggio dei conteggi](../mdx/topcount-mdx.md). Il set denominato potrà quindi essere utilizzato ogni volta che sarà necessario recuperare il set dei primi 10 punti vendita.  
  
 L'istruzione CREATE SET crea un set denominato che rimane disponibile per tutta la sessione e può pertanto essere utilizzato in più query durante la sessione. Per ulteriori informazioni, vedere [creazione di membri calcolati con ambito sessione &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members).  
  
 È inoltre possibile definire un set denominato da utilizzare in un'unica query. Per definire un set di questo tipo, utilizzare la clausola WITH nell'istruzione SELECT. Per ulteriori informazioni sulla clausola WITH, vedere [creazione di set denominati con ambito Query &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets).  
  
 La clausola *set_expression* può contenere qualsiasi funzione che supporta la sintassi MDX. L'ambito dei set creati con l'istruzione CREATE SET che non specificano la clausola SESSION è sessione. Utilizzare la clausola WITH per creare un set con l'ambito query.  
  
 Specificando un cubo diverso dal cubo connesso viene generato un errore. Pertanto, per identificare il cubo corrente è consigliabile usare CURRENTCUBE anziché il nome di un cubo.  
  
## <a name="scope"></a>Scope  
 Un set definito dall'utente può trovarsi all'interno di uno degli ambiti elencati nella tabella seguente.  
  
 Ambito delle query  
 La visibilità e la durata del set sono limitate alla query. Il set è definito in un'unica query. L'ambito query prevale sull'ambito sessione. Per ulteriori informazioni, vedere [creazione di set denominati con ambito Query &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets).  
  
 Ambito sessione  
 La visibilità e la durata del set sono limitate alla sessione in cui è stato creato. (La durata è inferiore alla durata della sessione se nel set viene eseguita un'istruzione DROP SET). L'istruzione CREATE SET crea un set con ambito sessione. Utilizzare la clausola WITH per creare un set con l'ambito query.  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un set denominato Core Products. Mediante la query SELECT viene quindi illustrata la chiamata del set appena creato. Affinché possa essere eseguita la query SELECT, è necessario che sia stata innanzitutto eseguita l'istruzione CREATE SET. Non possono essere eseguite nello stesso batch.  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>Valutazione del set  
 La valutazione del set può essere definita in diversi modi: può essere definita per essere eseguita solo una volta alla creazione del set oppure per essere eseguita ogni volta che il set viene utilizzato.  
  
 STATIC  
 Indica che il set viene valutato solo al momento della valutazione dell'istruzione CREATE SET.  
  
 DYNAMIC  
 Indica che il set deve essere valutato tutte le volte che viene utilizzato in una query.  
  
## <a name="set-visibility"></a>Visibilità set  
 Il set può essere o meno visibile agli altri utenti che eseguono la query sul cubo.  
  
 HIDDEN  
 Specifica che il set non è visibile agli utenti che eseguono una query sul cubo.  
  
## <a name="standard-properties"></a>Proprietà standard  
 Ogni set presenta un set di proprietà predefinite. Quando un'applicazione client è connessa a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], le proprietà predefinite sono supportate o disponibili per essere supportate, in quanto l'amministratore sceglie.  
  
|Identificatore proprietà|Significato|  
|-------------------------|-------------|  
|CAPTION|Una stringa che l'applicazione client utilizza come didascalia per il set.|  
|DISPLAY_FOLDER|Una stringa che identifica il percorso della cartella di visualizzazione che l'applicazione client utilizza per mostrare il set. Il separatore di livello delle cartelle è definito dall'applicazione client. Per gli strumenti e i client forniti [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]da, la barra\\rovesciata () è il separatore di livello. Per fornire più cartelle di visualizzazione per un set definito, utilizzare un punto e virgola (;) per separare le cartelle.|  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione DROP SET &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
