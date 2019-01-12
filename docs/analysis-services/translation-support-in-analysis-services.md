---
title: Supporto delle traduzioni in Analysis Services | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd727b56649ce9ffc237575b0311db256ec9b2fc
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2019
ms.locfileid: "54184927"
---
# <a name="translation-support-in-analysis-services"></a>Supporto delle traduzioni in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] modelli di dati, è possibile incorporare più traduzioni di una didascalia o una descrizione per fornire stringhe specifiche delle impostazioni cultura in base all'identificatore delle impostazioni locali (LCID). Per i modelli multidimensionali, è possibile aggiungere traduzioni per il nome del database, gli oggetti cubo e gli oggetti dimensione del database. Per i modelli tabulari, è possibile tradurre le descrizioni e le didascalie di tabella e colonna.  
  
 La definizione di una traduzione crea i metadati e la didascalia tradotta all'interno del modello, ma per eseguire il rendering delle stringhe localizzate in un'applicazione client, è necessario impostare la proprietà **Language** per l'oggetto o passare un parametro **Culture** o **Locale Identifier** nella stringa di connessione, ad esempio impostando `LocaleIdentifier=1036` per restituire le stringhe in francese.  
  
 Pensare di usare **Locale Identifier** se si vuole supportare più traduzioni simultanee dello stesso oggetto in lingue diverse. L'impostazione della proprietà **Language** funziona, ma influisce anche sull'elaborazione e l'esecuzione di query comportando conseguenze impreviste. È preferibile scegliere di impostare il parametro **Locale Identifier** in quanto viene usato solo per restituire le stringhe tradotte.  
  
 Una traduzione è costituita da un identificatore delle impostazioni locali (LCID), una didascalia tradotta per l'oggetto (ad esempio, il nome di una dimensione o di un attributo), e facoltativamente un'associazione a una colonna che fornisce i valori dei dati nella lingua di destinazione. È possibile avere più traduzioni, ma è possibile usarne solo una per ogni connessione specifica. In teoria, non vi sono limiti al numero di traduzioni che è possibile incorporare nel modello, ma ogni traduzione aggiunge complessità al test e tutte le traduzioni devono condividere le stesse regole di confronto, pertanto quando si progetta la soluzione tenere presenti questi vincoli normali.  
  
> [!TIP]  
>  È possibile utilizzare le applicazioni client quali Excel, SQL Server Management Studio e SQL Server Profiler per restituire le stringhe tradotte. Per informazioni dettagliate, vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>Come aggiungere metadati tradotti al modello in Analysis Services  
 Per istruzioni dettagliate, usare questi collegamenti:  
  
-   [Traduzioni nei modelli tabulari](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [Traduzioni nei modelli multidimensionali](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [Impostare o modificare le regole di confronto delle colonne](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
