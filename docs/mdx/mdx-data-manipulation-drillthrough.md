---
description: Manipolazione dei dati MDX - DRILLTHROUGH
title: Istruzione drill-through (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee68e6cbb22bc817d478490315ab88ccb87e4ad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387040"
---
# <a name="mdx-data-manipulation---drillthrough"></a>Manipolazione dei dati MDX - DRILLTHROUGH


  Recupera le righe di tabella sottostanti utilizzate per creare una cella specificata in un cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Unsigned_Integer*  
 Valore integer positivo.  
  
 *Istruzione SELECT MDX*  
 Qualsiasi istruzione SELECT di espressione MDX (Multidimensional Expression) valida.  
  
 *Set_of_Attributes_and_Measures*  
 Elenco delimitato da virgole di misure e attributi della dimensione.  
  
## <a name="remarks"></a>Osservazioni  
 Il drill-through è un'operazione con cui un utente finale seleziona una singola cella di un cubo e recupera un set di risultati dai dati di origine di tale cella allo scopo di ottenere informazioni più dettagliate. Per impostazione predefinita, il set di risultati di un drill-through è derivato dalle righe di tabella che sono state valutate per calcolare il valore della cella del cubo selezionata. Per il drill-through da parte degli utenti finali, è necessario che le relative applicazioni client supportino tale funzionalità. In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] i risultati vengono recuperati direttamente dall'archiviazione MOLAP, a meno che non vengano eseguite query su partizioni o dimensioni ROLAP.  
  
> [!IMPORTANT]  
>  La sicurezza relativa al drill-through è basata sulle opzioni di sicurezza generali definite per il cubo. Se un utente non può ottenere alcuni dati tramite MDX, all'utente verranno applicate dal drill-through le stesse restrizioni.  
  
 La cella interessata è specificata da un'istruzione MDX. Il valore specificato dall'argomento **MaxRows** indica il numero massimo di righe che devono essere restituite dal set di righe risultante.  
  
 Per impostazione predefinita, il numero massimo di righe restituite è 10.000. Ciò significa che se si lascia **MaxRows** non specificato, si otterranno 10.000 righe o meno. Se questo valore è troppo basso per lo scenario in uso, è possibile impostare **MaxRows** su un numero maggiore, ad esempio `MAXROWS 20000` . Se il valore è troppo basso, è possibile aumentare il valore predefinito modificando la proprietà del server **OLAP\Query\DefaultDrillthroughMaxRows** . Per ulteriori informazioni sulla modifica di questa proprietà, vedere [proprietà del server in Analysis Services](https://docs.microsoft.com/analysis-services/server-properties/server-properties-in-analysis-services).  
  
 Se non diversamente specificato, le colonne restituite includono tutti gli attributi di granularità per tutte le dimensioni correlate al gruppo di misure della misura specificata, tranne le dimensioni molti-a-molti. Le dimensioni del cubo sono precedute da $ per consentire la distinzione tra dimensioni e gruppi di misure. La clausola **return** viene utilizzata per specificare le colonne restituite dalla query drill-through. Le funzioni seguenti possono essere applicate a un singolo attributo o misura mediante la clausola **return** .  
  
 Name(attribute_name)  
 Restituisce il nome del membro dell'attributo specificato.  
  
 UniqueName(attribute_name)  
 Restituisce il nome univoco del membro dell'attributo specificato.  
  
 Key(attribute_name[, N])  
 Restituisce la chiave del membro dell'attributo specificato. N specifica la colonna nella chiave composta (se disponibile). Il valore predefinito di N è 1.  
  
 Caption(attribute_name)  
 Restituisce la didascalia del membro dell'attributo specificato.  
  
 MemberValue(attribute_name)  
 Restituisce il valore del membro dell'attributo specificato.  
  
 CustomRollup(attribute_name)  
 Restituisce l'espressione di rollup personalizzato del membro dell'attributo specificato.  
  
 CustomRollupProperties(attribute_name)  
 Restituisce le proprietà di rollup personalizzato del membro dell'attributo specificato.  
  
 UnaryOperator(attribute_name)  
 Restituisce l'operatore unario del membro dell'attributo specificato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene specificata la cella del mese di luglio 2007 per la misura dell'importo delle vendite dei rivenditori (misura predefinita) per il paese Australia. La clausola RETURN specifica la restituzione della data di ogni vendita, del nome del modello di prodotto, del nome del dipendente, dell'importo delle vendite, delle imposte e dei valori di costo dei prodotti sottostanti questa cella.  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di manipolazione dei dati MDX &#40;&#41;MDX ](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
