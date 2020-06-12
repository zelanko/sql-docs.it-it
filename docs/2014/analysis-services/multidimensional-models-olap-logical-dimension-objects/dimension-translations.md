---
title: Traduzioni delle dimensioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6f31773ad871ef7e3fc8f99d57e7a9099335b899
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545157"
---
# <a name="dimension-translations"></a>Traduzioni delle dimensioni
  Una traduzione è un semplice meccanismo che consente di modificare la lingua delle etichette e delle didascalie visualizzate. Ogni traduzione è definita come una coppia di valori: una stringa con il testo tradotto e un numero con l'ID della lingua. Le traduzioni sono disponibili per tutti gli oggetti in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Nel caso delle dimensioni è possibile tradurre anche i valori di attributo. L'applicazione client è responsabile della ricerca dell'impostazione della lingua definita dall'utente e del passaggio alla visualizzazione di tutte le didascalie e le etichette nella lingua in questione. Un oggetto può disporre di un numero illimitato di traduzioni.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Translation> semplice è composto dal numero ID della lingua e dalla didascalia tradotta. Il numero ID della lingua è un valore `Integer` con l'ID della lingua. La didascalia tradotta è il testo tradotto.  
  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una conversione della dimensione è una rappresentazione specifica della lingua del nome di una dimensione, del nome di un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetto o di uno dei relativi membri, ad esempio una didascalia, un membro o un livello di gerarchia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]supporta inoltre le traduzioni di oggetti cubo.  
  
 Le traduzioni offrono supporto server per applicazioni client in grado di supportare più lingue. I cubi e le relative dimensioni spesso vengono visualizzati da utenti di paesi diversi. La possibilità di tradurre vari elementi di un cubo e le relative dimensioni in un'altra lingua consente a tali utenti di visualizzare e comprendere il cubo. Un utente aziendale in Francia, ad esempio, può accedere a un cubo da una workstation in cui vengono utilizzate le impostazioni locali francesi e visualizzare i valori delle proprietà dell'oggetto in francese. Tuttavia, un utente aziendale in Germania che accede allo stesso cubo da una workstation in cui vengono utilizzate le impostazioni locali tedesche visualizzerà gli stessi valori delle proprietà dell'oggetto in tedesco.  
  
 Le informazioni sulle regole di confronto e sulla lingua per il computer client sono archiviate in forma di identificatore delle impostazioni locali (LCID). Al momento della connessione, il client passa l'identificatore delle impostazioni locali all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. che utilizza tale valore per determinare il set di traduzioni in cui restituire i metadati relativi agli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se un oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non contiene la traduzione specificata, per restituire il contenuto al client viene utilizzata la lingua predefinita.  
  
## <a name="see-also"></a>Vedere anche  
 [Traduzioni di cubi](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Traduzioni &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
