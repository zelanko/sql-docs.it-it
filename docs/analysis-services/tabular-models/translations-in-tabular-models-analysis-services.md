---
title: Traduzioni nei modelli tabulari (Analysis Services) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ddd49ce6d3edc3f1e2f72a3fe7f5ab61621eef62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162379"
---
# <a name="translations-in-tabular-models-analysis-services"></a>Traduzioni in modelli tabulari (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Aggiunge il supporto di stringa di traduzione per i modelli tabulari. Un singolo oggetto nel modello può avere più traduzioni di un nome o di una descrizione, rendendo possibile supportare versioni multilingue all'interno della definizione di modello.  
  
 Le stringhe tradotte valgono esclusivamente per i metadati dell'oggetto (nomi e descrizioni di tabelle e colonne) che vengono visualizzati in uno strumento client come un elenco di tabella pivot di Excel.  Per usare le stringhe tradotte, la connessione client specifica le impostazioni cultura. Nella funzionalità **Analisi in Excel** è possibile scegliere la lingua da un elenco a discesa. Per altri strumenti, potrebbe essere necessario specificare le impostazioni cultura nella stringa di connessione.  
  
 Questa funzionalità non è usata per caricare i dati tradotti in un modello. Se si desidera caricare i valori dei dati tradotti, è necessario sviluppare una strategia di elaborazione che includa l'estrazione di stringhe tradotte da un'origine di dati che le fornisce.  
  
 Un tipico flusso di lavoro per l'aggiunta di metadati tradotti è simile al seguente:  
  
-   Generare un file di traduzione vuoto JSON che contenga segnaposti per ogni stringa tradotta  
  
-   Aggiungere le traduzioni delle stringhe per il file JSON  
  
-   Reimportare le traduzioni nel modello  
  
-   Creare, elaborare o distribuire il modello  
  
-   Connettersi al modello usando un'applicazione client che consenta un LCID sulla stringa di connessione  
  
## <a name="create-an-empty-translation-file"></a>Creazione di un file di traduzione vuoto  
 Usare [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] per aggiungere le traduzioni.  
  
1.  Fare clic su **Modello** > **Traduzioni** > **Gestisci traduzioni**.  
  
2.  Selezionare le lingue per cui vengono fornite le traduzioni, quindi fare clic su **Aggiungi**.  
  
3.  Scegliere una o più lingue dall'elenco, a seconda di come si desidera importare le stringhe in un secondo momento.  
  
     Il file di traduzione può includere più lingue, ma la gestione delle traduzione può risultare più semplice se si crea un file di traduzione per ogni lingua. Il file di traduzione che viene adesso creato, verrà interamente importato in un secondo momento. Per differenziare le opzioni di importazione in base alla lingua, ciascuna lingua deve trovarsi nel relativo file.  
  
4.  Fare clic su **Esporta file lingua**.  Specificare un nome e un percorso file.  
  
 ![ssas-tabular-translate-export](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-tabular-translate-export")  
  
## <a name="add-translations"></a>Aggiunta di traduzioni  
 Un file di traduzione JSON vuoto include metadati per le traduzioni in una lingua specifica. I segnaposti di traduzione per i nomi e le descrizioni degli oggetti vengono specificati nella sezione **Culture** alla fine della definizione del modello. È possibile aggiungere traduzioni per quanto segue:  
  
|||  
|-|-|  
|translatedCaption|Titolo della tabella o della colonna visualizzato in qualsiasi applicazione client che supporta visualizzazioni di un modello tabulare.|  
|translatedDescription|Meno frequente delle didascalie, una descrizione viene visualizzata come informazione sul modello in uno strumento di modellazione come SSDT.|  
  
 Non eliminare eventuali metadati non specificati dal file.  Dovrebbero corrispondere al file su cui si basano. È sufficiente aggiungere le stringhe desiderate, quindi salvare il file.  
  
 Anche se può sembrare un elemento da modificare, la sezione  **referenceCulture** contiene i metadati nelle impostazioni cultura predefinite del modello. Eventuali modifiche apportate alla sezione **referenceCulture** non verranno lette durante l'importazione e verranno ignorate.  
  
 Nell'esempio seguente vengono visualizzate le didascalie tradotte e la descrizione per le tabelle **DimProduct** e **DimCustomer** .  
  
 ![ssas-tabular-translate-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-tabular-translate-json")  
  
> [!TIP]  
>  È possibile usare qualsiasi editor di JSON per aprire il file, ma è consigliabile l'editor JSON in Visual Studio in modo da poter usare il comando Visualizza codice in Esplora soluzioni per visualizzare la definizione di modello tabulare in SSDT. Per disporre dell'editor JSON, è necessaria un' [installazione della versione completa di Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx). L'edizione gratuita Community include l'editor JSON.  
  
## <a name="import-a-translation-file"></a>Importazione di un file di traduzione  
 Le stringhe di traduzione che vengono importate diventano parte permanente della definizione del modello. Dopo aver importato le stringhe, non esistono più riferimenti al file di traduzione.  
  
1.  Fare clic su **Modello** > **Traduzioni** > **Importa traduzioni**.  
  
2.  Individuare il file di traduzione, quindi fare clic su **Apri**.  
  
3.  Facoltativamente, specificare le opzioni di importazione.  
  
    |||  
    |-|-|  
    |Sovrascrivi le traduzioni esistenti|Sostituisce tutte le didascalie o le descrizioni esistenti della stessa lingua del file che viene importato.|  
    |Ignora oggetti non validi|Specifica se le discrepanze dei metadati devono essere ignorate o contrassegnate come errore.|  
    |Registra i risultati dell'importazione in un file di log|I file di log vengono salvati nella cartella di progetto per impostazione predefinita. Il percorso esatto del file viene fornito al termine dell'importazione. Il nome di file di log è SSDT_Translations_Log_\<timestamp >.|  
    |Esegui il backup delle traduzioni in un file JSON prima dell'importazione|Esegue il backup di una traduzione esistente che corrisponde alle impostazioni cultura delle stringhe importate.  Se le impostazioni cultura importate non sono presenti nel modello, il backup sarà vuoto.<br /><br /> Se è necessario ripristinare questo file in un secondo momento, è possibile sostituire il contenuto di model.bim con questo file JSON.|  
  
4.  Fare clic su **Importa**.  
  
5.  Facoltativamente, se è stato generato un file di log o un backup, è possibile trovare i file nella cartella del progetto (ad esempio, C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW).  
  
6.  Per verificare l'importazione, attenersi alla seguente procedura:  
  
    -   Fare clic con il pulsante destro del mouse sul file **model.bim** in Esplora soluzioni e scegliere **Visualizza codice**. Fare clic su **Sì** per chiudere la visualizzazione di progettazione e riaprire **model.bim** nella visualizzazione codice.  Se è installata una versione completa di Visual Studio, ad esempio la Community Edition gratuita, il file viene aperto nell'editor JSON incorporato.  
  
    -   Cercare **Impostazioni cultura** o una specifica stringa tradotta per verificare se le stringhe previste sono effettivamente presenti.  
  
## <a name="connect-using-a-locale-identifier"></a>Connessione tramite un identificatore delle impostazioni locali  
 In questa sezione viene descritto un approccio per la convalida delle stringhe corrette restituite dal modello.  
  
1.  In Excel connettersi al modello tabulare. Arrivati a questo passaggio si presuppone che il modello sia stato distribuito. Se il modello esiste solo nell'area di lavoro, distribuirlo in un'istanza di Analysis Services per completare il controllo di convalida.  
  
     In alternativa, è possibile usare la funzionalità **Analizza in Excel** per la connessione al modello  
  
2.  Nella finestra di dialogo di connessione di Excel, scegliere le impostazioni cultura per cui le traduzioni delle stringhe esistono nel modello. Excel rileva le impostazioni cultura definite nel modello e popola di conseguenza l'elenco a discesa.  
  
     ![ssas-tabular-translations-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-tabular-translations-excel")  
  
     Dopo aver creato una tabella pivot, dovrebbero essere visualizzati i nomi della colonna e della tabella tradotti.  
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità per i modelli tabulari in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Scenari di globalizzazione per Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Modello](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
