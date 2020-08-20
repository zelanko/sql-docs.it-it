---
description: Operatori (sintassi MDX)
title: Operatori (sintassi MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3d52751978dbe2973ecab9506094fad6a6f6c29a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471773"
---
# <a name="operators-mdx-syntax"></a>Operatori (sintassi MDX)


  Gli operatori disponibili nel linguaggio MDX (Multidimensional Expressions) consentono di eseguire le operazioni seguenti:  
  
-   Modificare i dati in modo permanente o temporaneo.  
  
-   Ricercare oggetti o valori che soddisfano una condizione specificata.  
  
-   Effettuare una scelta tra due valori o espressioni.  
  
-   Verificare l'esistenza di condizioni specifiche prima di iniziare o eseguire il commit di una transazione oppure prima di eseguire istruzioni specifiche.  
  
 MDX supporta gli operatori elencati nella tabella seguente:  
  
|Per eseguire questo tipo di operazione|Uso|  
|---------------------------------------|---------|  
|Assegnare un valore a una variabile oppure associare un alias a una colonna di un set di risultati.|[Operatori di assegnazione](../mdx/assignment-operators.md)|  
|Eseguire addizioni, sottrazioni, moltiplicazioni e divisioni.|[Operatori aritmetici](../mdx/arithmetic-operators.md)|  
|Stabilire se una condizione è vera, ad esempio AND, OR, NOT e XOR.|[Operatori bit per bit](../mdx/bitwise-operators.md)|  
|Confrontare un valore con un altro valore o un'espressione.|[Operatori di confronto](../mdx/comparison-operators.md)|  
|Combinare due stringhe in un'unica stringa in modo permanente o temporaneo.|[Operatori di concatenazione](../mdx/concatenation-operators.md)|  
|Combinare due espressioni set in un unico set in modo permanente o temporaneo.|[Operatori Set](../mdx/set-operators.md)|  
|Eseguire un'operazione su un operando.|[Operatori unari](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  Nelle query può eseguire operazioni qualsiasi utente in grado di visualizzare i dati del cubo da utilizzare con uno specifico operatore. Per modificare i dati è tuttavia necessario disporre delle autorizzazioni appropriate.  
  
 Quando si utilizzano più operatori, l'ordine in cui vengono valutati da MDX è molto importante. Per utilizzare alcuni operatori, inoltre, può essere necessario convertire i dati da un tipo di dati a un altro affinché gli operatori possano essere valutati.  
  
## <a name="evaluating-complex-expressions"></a>Valutazione di espressioni complesse  
 Quando si compila un'espressione è possibile utilizzare gli operatori per combinare diverse espressioni più piccole. In queste espressioni complesse, MDX valuta gli operatori in base alla definizione della precedenza degli operatori utilizzata da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Gli operatori con precedenza superiore vengono applicati prima di quelli con precedenza inferiore.  
  
### <a name="understanding-operator-precedence"></a>Informazioni sulla precedenza degli operatori  
 Nell'elenco seguente viene illustrata la precedenza degli operatori, dalla più alta alla più bassa. Gli operatori indicati sulla stessa riga hanno la stessa precedenza e vengono valutati da sinistra a destra, a meno che non siano presenti parentesi che impongono un ordine diverso:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, > , <  
  
-   NOT  
  
-   AND  
  
-   XOR  
  
-   OR  
  
 Per ulteriori informazioni sugli operatori in MDX, vedere Guida di riferimento agli operatori [mdx &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Determinazione dei risultati  
 Quando si combinano più espressioni semplici in modo da formare un'espressione complessa, il tipo di dati del valore risultante viene ottenuto combinando le regole degli operatori con le regole relative alla precedenza dei tipi di dati.  
  
 Se il risultato è un carattere o un valore Unicode, le regole di confronto verranno determinate combinando le regole degli operatori con le regole sulla precedenza delle regole di confronto. Per ulteriori informazioni sulle regole di confronto, vedere [lingue e regole di confronto &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services).  
  
 Sono previste inoltre regole per determinare precisione, scala e lunghezza del risultato in base alla precisione, alla scala e alla lunghezza delle varie espressioni semplici.  
  
## <a name="converting-data-types"></a>Conversione del tipo di dati  
 MDX converte implicitamente un oggetto in un tipo diverso se tale oggetto viene utilizzato in un'espressione che richiede un tipo diverso. Nella tabella seguente sono definite le regole di conversione per ogni oggetto.  
  
|Tipo originale|Tipo necessario|Conversione|  
|-------------------|-----------------|----------------|  
|Level|Set|\<level>. membri|  
|Gerarchia|Membro|\<hierarchy>. DefaultMember|  
|Membro|Tupla|(\<Member>)|  
|Tupla|Membro|\<tuple>. Item (0)|  
|Tupla|Scalare|\<tuple>. valore|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)   
 [Elementi della sintassi MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
