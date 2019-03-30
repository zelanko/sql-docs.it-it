---
title: Scenari di globalizzazione per Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9af9e0eaf06fca60da515a16e7e6830dcb8462d
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658325"
---
# <a name="globalization-scenarios-for-analysis-services"></a>Scenari di globalizzazione per Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] archivia e gestisce dati e metadati multilingue per i modelli di dati tabulari e multidimensionali. L'archiviazione dei dati è in formato Unicode (UTF-16) nei set di caratteri che usano la codifica Unicode. Se in un modello di dati si caricano dati ANSI, i caratteri vengono archiviati usando elementi di codice Unicode equivalenti.  
  
 Le implicazioni del supporto Unicode consentono a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di archiviare i dati in una qualsiasi lingua supportata dai sistemi operativi client e server Windows, permettendo la lettura, la scrittura, l'ordinamento e il confronto dei dati in qualsiasi set di caratteri usato in un computer Windows. Le applicazioni client BI che utilizzano i dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] possono rappresentare i dati nella lingua scelta dall'utente, supponendo che i dati esistano in tale lingua nel modello.  
  
 Il supporto della lingua può avere diversi significati a seconda degli utenti. L'elenco seguente risponde ad alcune domande comuni relative al modo in cui Analysis Services supporta le lingue.  
  
-   I dati, come già indicato, vengono archiviati in un qualsiasi set di caratteri con codifica Unicode presente in un sistema operativo client Windows.  
  
-   I metadati, ad esempio i nomi degli oggetti, possono essere tradotti. Anche se il supporto varia in base al tipo di modello, i modelli multidimensionali e tabulari supportano l'aggiunta di stringhe tradotte all'interno del modello. È possibile definire più traduzioni e quindi usare un identificatore delle impostazioni locali per stabilire quale traduzione viene restituita al client. Per altre informazioni, vedere la sezione [Funzionalità](#bkmk_features) di seguito  
  
-   Gli errori, gli avvisi e i messaggi informativi restituiti dal motore di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (msmdsrv) sono localizzati in 43 lingue supportate da Office e Office 365. Per ricevere i messaggi in una lingua specifica non è necessaria alcuna configurazione. Le impostazioni locali dell'applicazione client determinano quali stringhe vengono restituite.  
  
-   I file di configurazione (msmdsrv.ini) e PowerShell per AMO sono disponibili solo in lingua inglese.  
  
-   I file di log conterranno un insieme di messaggi localizzati e in lingua inglese, supponendo che sia stato installato un Language Pack nel server Windows in cui viene eseguito Analysis Services.  
  
-   La documentazione e gli strumenti, ad esempio [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], sono tradotti nelle lingue seguenti: cinese semplificato, cinese tradizionale, francese, tedesco, italiano, giapponese, coreano, portoghese (Brasile), russo e spagnolo. Le impostazioni cultura vengono specificate durante l'installazione.  
  
 Per i modelli multidimensionali, Analysis Services consente di impostare la lingua, le regole di confronto e le traduzioni in modo indipendente in tutta la gerarchia di oggetti.  Per i modelli tabulari, è possibile aggiungere solo le traduzioni: lingua e regole di confronto vengono ereditate dal sistema operativo host.  
  
 Gli scenari abilitati tramite le funzionalità di globalizzazione di Analysis Services includono:  
  
-   Un unico modello di dati fornisce più didascalie tradotte in modo che i nomi dei campi e i valori vengono visualizzati nella lingua scelta dall'utente. Per le società che operano in paesi bilingue come Canada, Belgio o Svizzera, il supporto di più lingue nelle applicazioni client e server è un requisito di codifica standard. Questo scenario viene abilitato tramite traduzioni e conversioni di valuta. Per altre informazioni e collegamenti, vedere la sezione [Funzionalità](#bkmk_features) di seguito.  
  
-   Gli ambienti di sviluppo e di produzione sono posizionati geograficamente in diversi paesi. È sempre più comune sviluppare una soluzione in un paese e quindi distribuirla in un altro. È essenziale sapere impostare le proprietà della lingua e delle regole di confronto se occorre preparare una soluzione sviluppata in una lingua, per distribuirla in un server che usa un altro Language Pack. L'impostazione di queste proprietà consente di eseguire l'override delle impostazioni predefinite ereditate che vengono recuperate dal sistema host originale. Per altre informazioni, vedere la sezione [Lingue e regole di confronto &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md) per informazioni dettagliate sull'impostazione delle proprietà.  
  
##  <a name="bkmk_features"></a> Funzionalità per la creazione di una soluzione multilingue globalizzata  
 A livello di client, le applicazioni globalizzate che usano o gestiscono dati multidimensionali di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] possono usare le funzionalità multilingue e multiculturali di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 È possibile recuperare i dati e i metadati dagli oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in cui le traduzioni sono state definite automaticamente fornendo un identificatore delle impostazioni locali quando si esegue la connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Vedere [Suggerimenti e procedure consigliate per la globalizzazione &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) per le procedure di progettazione e codifica che consentono di evitare i problemi correlati ai dati multilingue.  
  
||||  
|-|-|-|  
|**Funzionalità**|**Tabella**|**Multidimensionale**|  
|[Lingue e regole di confronto &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)|Ereditata dal sistema operativo.|Ereditata, ma con possibilità di sostituire la lingua e le regole di confronto per gli oggetti principali nella gerarchia del modello.|  
|Ambito del supporto di traduzione|Didascalie e descrizioni.|È possibile creare traduzioni per nomi di oggetti, didascalie, identificatori e descrizioni, anche in qualsiasi alfabeto e lingua Unicode. Ciò vale anche quando gli strumenti e l'ambiente sono in un'altra lingua. Ad esempio, in un ambiente di sviluppo che usa la lingua inglese e le regole di confronto in caratteri latini in tutto lo stack, è possibile includere nel modello un oggetto che usa caratteri cirillici nel nome.|  
|Implementazione del supporto di traduzione|È possibile usare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per generare file di traduzione da completare e quindi importare nuovamente nel modello.<br /><br /> Per informazioni dettagliate, vedere [Traduzioni in modelli tabulari &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md).|È possibile usare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per definire le traduzioni per la didascalia, la descrizione e i tipi di account per cubi, misure, dimensioni e attributi.<br /><br /> Per altre informazioni, vedere [Translations in Multidimensional Models &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md) [Traduzioni nei modelli multidimensionali &#40;Analysis Services&#41;]. Una lezione su come usare questa funzionalità disponibili [lezione 9: Definizione di prospettive e traduzioni](../analysis-services/lesson-9-defining-perspectives-and-translations.md) del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esercitazione.|  
|Conversione di valuta|Non disponibile.|La conversione di valuta viene eseguita tramite script MDX specializzati che convertono le misure contenenti dati di valuta. È possibile usare la Configurazione guidata funzionalità di Business Intelligence in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] per generare uno script MDX che utilizzi una combinazione di dati e metadati di dimensioni, attributi e gruppi di misure per la conversione di misure contenenti dati di valuta. Vedere [Conversioni di valuta &#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto delle traduzioni in Analysis Services](../analysis-services/translation-support-in-analysis-services.md)   
 [Internazionalizzazione per le applicazioni di Windows](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Globalizzazione](/globalization/)   
 [Scrittura di app di Windows Store con progettazione adattiva basata sulle impostazioni locali](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [Sviluppo di app di Windows universali con C# e XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
