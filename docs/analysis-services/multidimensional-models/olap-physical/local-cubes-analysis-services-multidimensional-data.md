---
title: Cubi locali (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bf47347967dcc4344ee71ee131951923df47713
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020216"
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Cubi locali (Analysis Services - Dati multidimensionali)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Per creare, aggiornare o eliminare cubi locali, è necessario scrivere ed eseguire uno script ASSL o un programma AMO.  
  
 I cubi locali e i modelli di data mining locali consentono di eseguire analisi in una workstation client disconnessa dalla rete. Un'applicazione client può ad esempio chiamare il provider OLE DB per OLAP 9.0 (MSOLAP.3), il quale carica il motore dei cubi locali per creare cubi locali ed eseguire query su di essi, come illustrato nella figura seguente:  
  
 ![Architettura client per i cubi locali e modelli](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "architettura Client per modelli e cubi locali")  
  
 Il motore dei cubi locali viene inoltre caricato da ADMOD.NET e dalla libreria AMO (Analysis Management Objects) durante l'interazione con cubi locali. A un file di cubo locale può accedere un unico processo, poiché il motore dei cubi locali blocca un file di cubo locale in modo esclusivo quando stabilisce una connessione con esso. Durante uno stesso processo, sono consentite fino a cinque connessioni simultanee.  
  
 Un file con estensione cub può contenere più cubi o modelli di data mining. Le query eseguite su modelli di data mining e cubi locali vengono gestite dal motore dei cubi locali e non necessitano di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  L'utilizzo di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] per la gestione di cubi locali non è supportato.  
  
## <a name="local-cubes"></a>Cubi locali  
 Un cubo locale può essere creato e popolato da un cubo esistente in un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] istanza o da un'origine dati relazionale.  
  
|Origine dei dati per il cubo locale|Metodo di creazione|  
|------------------------------------|---------------------|  
|Cubo basato su server|È possibile usare l'istruzione CREATE GLOBAL CUBE oppure un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] script Scripting Language (ASSL) per creare e popolare un cubo da un cubo basato su server. Per altre informazioni, vedere [istruzione CREATE GLOBAL CUBE &#40;MDX&#41; ](../../../mdx/mdx-data-definition-create-global-cube.md) oppure [Analysis Services Scripting Language &#40;ASSL per XMLA&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).|  
|Origine dei dati relazionale|Per creare e popolare un cubo da un database relazionale OLE DB è possibile utilizzare uno script ASSL. Per creare un cubo locale tramite ASSL, è sufficiente connettersi a un file di cubo locale con estensione cub ed eseguire lo script ASSL così come in caso di esecuzione di uno script ASSL su un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per creare un cubo sul server. Per altre informazioni, vedere [Guida di riferimento ad Analysis Services Scripting Language &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).|  
  
 Utilizzare l'istruzione REFRESH CUBE per ricompilare un cubo locale e aggiornarne i dati. Per altre informazioni, vedere [REFRESH CUBE Statement &#40;MDX&#41;](../../../mdx/mdx-data-definition-refresh-cube.md).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>Cubi locali creati da cubi basati su server  
 In caso di creazione di cubi locali a partire da cubi basati su server, si applicano le considerazioni seguenti:  
  
-   Non sono supportate misure Distinct Count.  
  
-   Quando si aggiunge una misura, è inoltre necessario includere almeno una dimensione correlata alla misura aggiunta. Per altre informazioni sulle relazioni tra dimensioni per i gruppi di misure, vedere [relazioni di tipo](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
-   Quando si aggiunge una gerarchia padre-figlio, i relativi livelli e filtri vengono ignorati e viene inclusa l'intera gerarchia padre-figlio.  
  
-   Non vengono create proprietà dei membri.  
  
-   Quando si include una misura semiadditiva, non sono consentite sezioni nella dimensione di tipo Conti o temporale.  
  
-   Le dimensioni di riferimento vengono sempre materializzate.  
  
-   Se si include una dimensione molti-a-molti, è necessario rispettare le regole seguenti:  
  
    -   Non è possibile sezionare la dimensione molti-a-molti.  
  
    -   È necessario aggiungere una misura dal gruppo di misure intermedio.  
  
    -   Non è possibile sezionare dimensioni comuni ai due gruppi di misure coinvolti nella relazione molti-a-molti.  
  
-   Nel cubo locale verranno inclusi soltanto i membri calcolati, i set denominati e le assegnazioni basati su misure e dimensioni aggiunte al cubo locale. I membri calcolati, i set denominati e le assegnazioni non validi verranno automaticamente esclusi.  
  
### <a name="security"></a>Sicurezza  
 Affinché un utente di creare un cubo locale da un cubo sul server, è necessario concedergli **drill-through e cubo locale** le autorizzazioni per il cubo sul server. Per altre informazioni, vedere [concedere le autorizzazioni del cubo o modello &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 I cubi locali non sono protetti tramite ruoli come i cubi sul server. Qualsiasi utente con accesso a livello di file per un file di cubo locale può eseguire query sui cubi in esso contenuti. È possibile usare la **Password di crittografia** proprietà di connessione in un file di cubo locale per impostare una password nel file di cubo locale. Con l'impostazione di una password per un file di cubo locale, tutte le successive connessioni a tale file dovranno utilizzare la password per eseguire query sul file.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione CREATE GLOBAL CUBE &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [REFRESH CUBE Statement &#40;MDX&#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  
