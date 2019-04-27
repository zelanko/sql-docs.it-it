---
title: Finestra di dialogo Proprietà Analysis Server (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e9bcb19e10417c24b30b5ee6346d6d6a19d4bbcb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636780"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>Finestra di dialogo Proprietà computer Analysis Server (Analysis Services)
  Usare la finestra di dialogo **Proprietà computer Analysis Server** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per definire le impostazioni generali, di sicurezza e di lingua e regole di confronto per un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per visualizzare la finestra di dialogo **Proprietà computer Analysis Server**, è possibile fare clic con il pulsante destro del mouse su un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora oggetti** e scegliere **Proprietà** dal menu di scelta rapida. Nella finestra di dialogo **Proprietà computer Analysis Server** sono incluse le proprietà seguenti.  
  
## <a name="information-properties"></a>Proprietà delle informazioni  
 Utilizzare questa pagina per visualizzare la modalità server, la versione e il livello di compatibilità. Ogni istanza viene installata in modalità server tabulare o multidimensionale con la possibilità di caricare modelli tabulari o multidimensionali. Se è necessario supportare entrambe le modalità, installare due istanze.  
  
 **Livello di compatibilità supportato** equivale al `DefaultCompatibilityLevel` proprietà in AMO. È di sola lettura in base alla modalità di distribuzione del server specificata durante l'installazione. Il server verifica tale proprietà durante l'esecuzione delle operazioni che variano in base alla modalità server o alla versione, ad esempio durante il ripristino di un backup di un database tabulare in un'istanza del server tabulare. Non confonderla con la modalità di compatibilità del database dei modelli tabulari o multidimensionali che hanno nomi e valori simili. I valori validi per questa proprietà del server includono:  
  
-   **1100** è il livello di compatibilità predefinito per una modalità di distribuzione 0, per la modalità multimediale e di data mining  
  
-   **1103** è il livello di compatibilità predefinito per le modalità di distribuzione 1 o 2, per le installazioni che supportano la modalità tabulare o per [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)].  
  
 Il server restituisce questo valore quando un client che supporta lo spazio dei nomi richiede DISCOVER_XML_METADATA. Per altre informazioni, vedere [Set di righe DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="general-properties"></a>Proprietà generali  
 Utilizzare questa pagina per impostare le proprietà generali di base e avanzate, ad esempio i percorsi delle cartelle e le impostazioni di rete, relative a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Nella pagina delle proprietà del server vengono visualizzate solo le proprietà che più probabilmente vengono modificate da un amministratore, ad esempio le proprietà della memoria e del pool di thread utilizzate per ottimizzare il server per alcune configurazioni. Nell'elenco seguente vengono forniti i collegamenti ai principali gruppi di proprietà:  
  
-   [Proprietà generali](server-properties/general-properties.md)  
  
-   [Proprietà di data mining](server-properties/data-mining-properties.md)  
  
-   [Proprietà di funzionalità](server-properties/feature-properties.md)  
  
-   [Proprietà della cache dei file](server-properties/filestore-properties.md)  
  
-   [Proprietà di Gestione blocchi](server-properties/lock-manager-properties.md)  
  
-   [Proprietà dei log](server-properties/log-properties.md)  
  
-   [Proprietà della memoria](server-properties/memory-properties.md)  
  
-   [Proprietà di rete](server-properties/network-properties.md)  
  
-   [Proprietà OLAP](server-properties/olap-properties.md)  
  
-   [Proprietà di sicurezza](server-properties/security-properties.md)  
  
-   [Proprietà dei pool di thread](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>Proprietà di lingua e regole di confronto  
 Utilizzare questa pagina per impostare le opzioni di lingua e regole di confronto predefinite per un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nell'elenco seguente viene fornita una breve descrizione di ogni opzione. Per descrizioni più dettagliate, vedere [Lingue e regole di confronto &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md).  
  
-   L'opzione**Binario** viene utilizzata per ordinare e confrontare i dati in base agli schemi di bit definiti per ogni carattere. Il tipo di ordinamento binario prevede la distinzione tra maiuscole e minuscole, ovvero i caratteri minuscoli precedono quelli maiuscoli, e la distinzione tra caratteri accentati e non accentati. Si tratta del tipo di ordinamento più rapido.  
  
     Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] segue le regole di ordinamento e confronto definite nei dizionari relativi alla lingua o all'alfabeto associato.  
  
    > [!NOTE]  
    >  La selezione di questa opzione comporta la disabilitazione delle opzioni **Distinzione maiuscole/minuscole**, **Distinzione caratteri accentati/non accentati**, **Distinzione Kana**e **Distinzione larghezza** .  
  
-   L'opzione**Binario 2** viene utilizzata per ordinare e confrontare i dati Unicode in base agli schemi di bit definiti per ogni carattere. Il tipo di ordinamento binario prevede la distinzione tra maiuscole e minuscole, ovvero i caratteri minuscoli precedono quelli maiuscoli, e la distinzione tra caratteri accentati e non accentati. Si tratta del tipo di ordinamento più rapido.  
  
-   L'opzione**Distinzione maiuscole/minuscole** viene usata per ordinare e confrontare i dati in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra lettere maiuscole e minuscole.  
  
     Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali le versioni maiuscole e minuscole non accentate delle lettere. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] indica se le lettere minuscole debbano essere ordinate più o versione successiva in relazione a lettere maiuscole di lettere quando **distinzione maiuscole/minuscole** non è selezionata.  
  
-   L'opzione**Distinzione caratteri accentati/non accentati** viene usata per ordinare e confrontare i dati in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra lettere accentate e non accentate. Il carattere 'a' non viene ad esempio considerato uguale ad 'à'.  
  
     Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali le versioni accentate e non accentate delle lettere.  
  
-   **Distinzione Kana e distinzione** viene usato per e confrontare i dati in base alle regole del dizionario specificate per la lingua associata o l'alfabeto, nonché per distinguere tra i due tipi di caratteri kana giapponesi: Hiragana e Katakana.  
  
     Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguale i caratteri Hiragana e Katakana.  
  
-   L'opzione**Distinzione larghezza** viene usata per eseguire l'ordinamento e il confronto in base alle regole del dizionario specificate per la lingua o l'alfabeto associato, nonché per distinguere tra la rappresentazione a un byte, ovvero a metà larghezza, e la rappresentazione a due byte, ovvero a larghezza intera, dello stesso carattere.  
  
     Se questa opzione non è selezionata, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera uguali la rappresentazione a un byte e la rappresentazione a due byte dello stesso carattere.  
  
## <a name="security-properties"></a>Proprietà di sicurezza  
 Utilizzare questa pagina per specificare gli account utente e di gruppo di Windows appartenenti al ruolo di amministratore del server per un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . L'appartenenza a questo ruolo concede le autorizzazioni necessarie per effettuare attività a livello di intero server, ad esempio la creazione o l'elaborazione di un database, la modifica delle proprietà del server, l'aggiunta o la rimozione di altri membri di questo ruolo oppure l'avvio di una traccia. Visualizzare [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md) per informazioni dettagliate.  
  
## <a name="see-also"></a>Vedere anche  
 [Determinare la modalità server di un'istanza di Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Configurare le proprietà del Server in Analysis Services](server-properties/server-properties-in-analysis-services.md)   
 [Metodologie di autenticazione supportate da Analysis Services](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Ruoli e autorizzazioni &#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
