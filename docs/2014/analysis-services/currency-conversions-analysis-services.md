---
title: Conversioni di valuta (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple currency conversions
- monetary data [SQL Server]
- currency [Analysis Services]
- converting currency
- one-to-many currency conversions
- many-to-many currency conversions [Analysis Services]
- many-to-one currency conversions [Analysis Services]
ms.assetid: e03f491c-7df8-46a0-ade9-f2e55b68db85
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48bbb9eeacc1e3ba2bd31ef10b47b058f0f57239
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086544"
---
# <a name="currency-conversions-analysis-services"></a>Conversioni di valuta (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]** Solo multidimensionale  
  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa una serie di funzionalità, basate su script MDX (Multidimensional Expressions), che implementano il supporto per la conversione di valuta nei cubi che supportano più valute.  
  
## <a name="currency-conversion-terminology"></a>Terminologia relativa alla conversione di valuta  
 Di seguito sono elencati i termini relativi alla conversione di valuta usati in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Valuta pivot  
 La valuta in base a cui vengono immessi i tassi di cambio nel gruppo di misure di tipo Tasso.  
  
 Valuta locale  
 La valuta usata per l'archiviazione delle transazioni su cui sono basate le misure da convertire.  
  
 La valuta locale può essere identificata da uno degli identificatori seguenti:  
  
-   Un identificatore di valuta nella tabella dei fatti archiviata con la transazione, come nel caso di applicazioni per operazioni bancarie in cui la transazione stessa identifica la valuta usata per la transazione.  
  
-   Un identificatore di valuta associato a un attributo di una tabella delle dimensioni che viene quindi associata a una transazione nella tabella dei fatti. È il caso di applicazioni finanziarie, in cui la valuta usata per la transazione associata è identificata dall'ubicazione o da un altro identificatore, ad esempio una filiale.  
  
 Valuta report  
 La valuta in cui viene convertita la valuta pivot nelle transazioni.  
  
> [!NOTE]  
>  In molte conversioni di valuta molti-a-uno la valuta pivot e la valuta report corrispondono.  
  
 Dimensione di tipo Valuta  
 Una dimensione del database definita con le impostazioni seguenti:  
  
-   La proprietà `Type` della dimensione è impostata su Currency.  
  
-   La proprietà `Type` di un attributo della dimensione è impostata su CurrencyName.  
  
    > [!IMPORTANT]  
    >  I valori di questo attributo devono essere usati in tutte le colonne che devono includere un identificatore di valuta.  
  
 Gruppo di misure di tipo Tasso  
 Un gruppo di misure di un cubo definito con le impostazioni seguenti:  
  
-   Tra una dimensione di tipo Valuta e il gruppo di misure di tipo Tasso esiste una relazione tra dimensioni di tipo Regolare.  
  
-   Tra una dimensione temporale e il gruppo di misure di tipo Tasso esiste una relazione tra dimensioni di tipo Regolare.  
  
-   Facoltativamente, la proprietà `Type` è impostata su ExchangeRate. Sebbene nella Configurazione guidata funzionalità di Business Intelligence vengano usate relazioni con dimensioni di tipo Valuta e temporali per l'identificazione dei possibili gruppi di misure di tipo Tasso, l'impostazione della proprietà `Type` su ExchangeRate semplifica l'identificazione di tali gruppi nelle applicazioni client.  
  
-   Una o più misure, che rappresentano i tassi di cambio inclusi nel gruppo di misure di tipo Tasso.  
  
 Dimensione di tipo Valuta report  
 La dimensione, specificata dalla Configurazione guidata funzionalità di Business Intelligence dopo che è stata definita una conversione di valuta, contenente le valute report per la conversione. La dimensione di tipo Valuta report è basata su una query denominata, definita nella vista origine dati su cui è basata la dimensione di tipo Valuta associata al gruppo di misure di tipo Tasso, che deriva dalla tabella della dimensione principale della dimensione di tipo Valuta. La dimensione è definita con le impostazioni seguenti:  
  
-   La proprietà `Type` della dimensione è impostata su Currency.  
  
-   La proprietà `Type` dell'attributo chiave della dimensione è impostata su CurrencyName.  
  
-   La proprietà `Type` di un attributo della dimensione è impostata su CurrencyDestination e la colonna associata all'attributo contiene gli identificatori di valuta che rappresentano le valute report per la conversione.  
  
## <a name="defining-currency-conversions"></a>Definizione delle conversioni di valuta  
 La Configurazione guidata funzionalità di Business Intelligence consente di definire la funzionalità di conversione di valuta per un cubo. In alternativa, le conversioni di valuta possono essere definite in modo manuale tramite script MDX.  
  
### <a name="prerequisites"></a>Prerequisites  
 Per poter definire una conversione di valuta in un cubo tramite la Configurazione guidata funzionalità di Business Intelligence, è prima necessario definire almeno una dimensione di tipo Valuta, una dimensione temporale e un gruppo di misure di tipo Tasso. Quando si esegue la Configurazione guidata funzionalità di Business Intelligence, questi oggetti vengono usati per recuperare i dati e i metadati per la creazione della dimensione di tipo Valuta report e dello script MDX necessari per l'implementazione della funzionalità di conversione di valuta.  
  
### <a name="decisions"></a>Decisioni  
 Per consentire la creazione della dimensione di tipo Valuta report e dello script MDX per l'implementazione della funzionalità di conversione di valuta tramite la Configurazione guidata funzionalità di Business Intelligence, è prima necessario stabilire:  
  
-   Direzione del tasso di cambio  
  
-   Membri convertiti  
  
-   Tipo di conversione  
  
-   Valute locali  
  
-   Valute report  
  
### <a name="exchange-rate-directions"></a>Direzioni del tasso di cambio  
 Il gruppo di misure di tipo Tasso include misure che rappresentano i tassi di cambio tra le valute locali e la valuta pivot, denominata anche valuta aziendale. L'insieme di direzione del tasso di cambio e tipo di conversione determina l'operazione che lo script MDX generato dalla Configurazione guidata funzionalità di Business Intelligence esegue sulle misure da convertire. Nella tabella seguente vengono descritte le operazioni eseguite a seconda della direzione del tasso di cambio e del tipo di conversione selezionati tra le opzioni disponibili nella configurazione guidata.  
  
|||||  
|-|-|-|-|  
|Direzione del tasso di cambio|**Molti-a-uno**|**Uno-a-molti**|**Molti a molti**|  
|**n valuta pivot per 1 valuta di esempio**|Moltiplica la misura da convertire in base alla misura di tipo Tasso della valuta locale allo scopo di convertirla nella valuta pivot.|Divide la misura da convertire in base alla misura di tipo Tasso della valuta report allo scopo di convertirla nella valuta report.|Moltiplica la misura da convertire in base alla misura di tipo Tasso della valuta locale allo scopo di convertirla nella valuta pivot, quindi divide la misura convertita in base alla misura di tipo Tasso della valuta report allo scopo di convertirla nella valuta report.|  
|**n valuta di esempio per 1 valuta pivot**|Divide la misura da convertire in base alla misura di tipo Tasso della valuta locale allo scopo di convertirla nella valuta pivot.|Moltiplica la misura da convertire in base alla misura di tipo Tasso della valuta report allo scopo di convertirla nella valuta report.|Divide la misura da convertire in base alla misura di tipo Tasso della valuta locale allo scopo di convertirla nella valuta pivot, quindi moltiplica la misura convertita in base alla misura di tipo Tasso della valuta report allo scopo di convertirla nella valuta report.|  
  
 La direzione del tasso di cambio viene impostata nel passaggio **Impostazione opzioni di conversione valuta** della Configurazione guidata funzionalità di Business Intelligence. Per altre informazioni sull'impostazione della direzione di conversione, vedere [Impostazione opzioni di conversione valuta &#40;Configurazione guidata funzionalità di Business Intelligence&#41](set-currency-conversion-options-business-intelligence-wizard.md).  
  
### <a name="converted-members"></a>Membri convertiti  
 La Configurazione guidata funzionalità di Business Intelligence consente di specificare le misure del gruppo di misure di tipo Tasso che devono essere usate per la conversione di valori per:  
  
-   Misure di altri gruppi di misure.  
  
-   Membri della gerarchia di un attributo Conto in una dimensione del database.  
  
-   Tipi di conto usati dai membri della gerarchia di un attributo Conto in una dimensione del database.  
  
 Nella configurazione guidata queste informazioni vengono usate nello script MDX generato automaticamente per determinare l'ambito della conversione di valuta. Per altre informazioni sull'impostazione dei membri per le conversioni di valuta, vedere [Selezione membri &#40;Configurazione guidata funzionalità di Business Intelligence&#41;](select-members-business-intelligence-wizard.md).  
  
### <a name="conversion-types"></a>Tipi di conversione  
 La Configurazione guidata funzionalità di Business Intelligence supporta tre tipi di conversione di valuta:  
  
-   **Uno-a-molti**  
  
     Le transazioni vengono archiviate nella tabella dei fatti nella valuta pivot e quindi convertite in una o più valute report.  
  
     Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni vengono archiviate nella tabella dei fatti in questa valuta. Con questo tipo di conversione la valuta pivot delle transazioni viene convertita nelle valute report specificate. Di conseguenza le transazioni possono essere archiviate nella valuta pivot specificata e visualizzate sia in questa valuta che in una delle valute report specificate nella dimensione di tipo Valuta report definita per la conversione di valuta.  
  
-   **Molti-a-uno**  
  
     Le transazioni vengono archiviate nella tabella dei fatti nelle valute locali e quindi convertite nella valuta pivot. La valuta pivot corrisponde all'unica valuta report specificata nella dimensione di tipo Valuta report.  
  
     Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni possono venire archiviate nella tabella dei fatti in euro (EUR), dollari australiani (AUD) e peso messicani (MXN). Con questo tipo di conversione le valute locali specificate delle transazioni vengono convertite nella valuta pivot. Di conseguenza le transazioni possono essere archiviate nelle valute locali specificate e visualizzate nella valuta pivot, la quale è specificata nella dimensione di tipo Valuta report definita per la conversione di valuta.  
  
-   **Molti a molti**  
  
     Le transazioni vengono archiviate nella tabella dei fatti nelle valute locali. La funzionalità di conversione di valuta consente di convertire queste transazioni nella valuta pivot e quindi in una o più valute report.  
  
     Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni possono venire archiviate nella tabella dei fatti in euro (EUR), dollari australiani (AUD) e peso messicani (MXN). Con questo tipo di conversione le valute locali specificate delle transazioni vengono convertite nella valuta pivot, la quale viene quindi convertita nelle valute report specificate. Di conseguenza le transazioni possono essere archiviate nelle valute locali specificate e visualizzate sia nella valuta pivot specificata che in una delle valute report specificate nella dimensione di tipo Valuta report definita per la conversione di valuta.  
  
 Se si specifica il tipo di conversione, nella Configurazione guidata funzionalità di Business Intelligence vengono definite la query denominata e la struttura della dimensione della dimensione di tipo Valuta report, nonché la struttura dello script MDX definito per la conversione di valuta.  
  
### <a name="local-currencies"></a>Valute locali  
 Se si imposta il tipo di conversione molti-a-molti o molti-a-uno, è necessario specificare la modalità di identificazione delle valute locali in base alle quali lo script MDX generato da Configurazione guidata funzionalità di Business Intelligence esegue le conversioni di valuta. La valuta locale di una transazione della tabella dei fatti può essere identificata in uno dei modi seguenti:  
  
-   Nel gruppo di misure è inclusa una relazione tra dimensioni di tipo Regolare con la dimensione di tipo Valuta. Ad esempio, nel database di esempio [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel gruppo di misure Internet Sales è inclusa una relazione tra dimensioni di tipo Regolare con la dimensione di tipo Valuta. La tabella dei fatti per tale gruppo di misure include una colonna chiave esterna che fa riferimento agli identificatori di valuta della tabella della dimensione. In questo caso è possibile selezionare l'attributo dalla dimensione di tipo Valuta a cui fa riferimento il gruppo di misure per identificare la valuta locale per le transazioni della tabella dei fatti di tale gruppo di misure. Ciò si verifica in genere nelle applicazioni per transazioni bancarie in cui la valuta usata viene determinata dalla transazione stessa.  
  
-   Nel gruppo di misure è inclusa una relazione tra dimensioni di tipo Riferimento con la dimensione di tipo Valuta tramite un'altra dimensione che fa riferimento direttamente alla dimensione di tipo Valuta. Ad esempio, nel database di esempio [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , il gruppo di misure Financial Reporting dispone di una relazione con dimensioni di tipo Riferimento alla dimensione di tipo Valuta tramite la dimensione Organization. La tabella dei fatti per tale gruppo di misure include una colonna chiave esterna che fa riferimento ai membri della tabella della dimensione per la dimensione Organization. Questa tabella della dimensione include a sua volta una colonna chiave esterna che fa riferimento agli identificatori di valuta nella tabella della dimensione per la dimensione di tipo Valuta. Ciò si verifica in genere nella applicazioni per relazioni finanziarie in cui la valuta di una transazione viene determinata dall'ubicazione o filiale. In questo caso è possibile selezionare l'attributo che fa riferimento alla dimensione di tipo Valuta nella dimensione dell'entità aziendale.  
  
### <a name="reporting-currencies"></a>Valute report  
 Se si imposta il tipo di conversione molti-a-molti o uno-a-molti, è necessario specificare le valute report in base alle quali lo script MDX generato dalla Configurazione guidata funzionalità di Business Intelligence esegue le conversioni di valuta. È possibile specificare tutti i membri della dimensione di tipo Valuta correlati al gruppo di misure di tipo Tasso oppure selezionare singoli membri.  
  
 Nella Configurazione guidata funzionalità di Business Intelligence viene creata una dimensione di tipo Valuta report basata sulla query denominata. Quest'ultima è formulata in base alla tabella della dimensione per la dimensione di tipo Valuta usando le valute report selezionate.  
  
> [!NOTE]  
>  Se si imposta il tipo di conversione uno-a-molti, viene creata anche una dimensione di tipo Valuta report. La dimensione include un solo membro che rappresenta la valuta pivot, in quanto questa valuta è usata anche come valuta report per le conversioni di valuta uno-a-molti.  
  
 Per ogni conversione di valuta definita in un cubo viene definita una dimensione di tipo Valuta report distinta. Le dimensioni di tipo Valuta report possono essere rinominate. In questo caso tuttavia è necessario aggiornare anche lo script MDX generato per la conversione di valuta in modo che nei riferimenti alle dimensioni di tipo Valuta report del comando script sia usato il nome corretto.  
  
## <a name="defining-multiple-currency-conversions"></a>Definizione di più conversioni di valuta  
 La Configurazione guidata funzionalità di Business Intelligence consente di definire il numero di conversioni di valuta desiderato in base alle specifiche esigenze. È possibile sovrascrivere una conversione di valuta esistente o accodare una nuova conversione allo script MDX di un cubo. La definizione di più conversioni di valuta in un cubo offre una maggiore flessibilità nelle applicazioni di Business Intelligence con requisiti di report complessi, ad esempio in applicazioni per relazioni finanziarie che supportano più requisiti di conversione distinti per la gestione di report internazionali.  
  
### <a name="identifying-currency-conversions"></a>Identificazione delle conversioni di valuta  
 Nella Configurazione guidata funzionalità di Business Intelligence, per identificare le varie conversioni di valuta, i comandi script per la conversione di valuta vengono inseriti nei commenti seguenti:  
  
 `//<Currency conversion>`  
  
 `...`  
  
 `[MDX statements for the currency conversion]`  
  
 `...`  
  
 `//</Currency conversion>`  
  
 Se questi commenti vengono modificati o rimossi, la conversione di valuta non potrà essere rilevata automaticamente dalla configurazione guidata. È pertanto necessario non modificare mai questi commenti.  
  
 In questi commenti vengono inoltre archiviati i metadati di commenti, tra cui la data e l'ora di creazione, l'utente e il tipo di conversione. Anche questi commenti non devono essere modificati, in quanto i metadati vengono usati dalla Configurazione guidata funzionalità di Business Intelligence per la visualizzazione delle conversioni di valuta esistenti.  
  
 È possibile modificare i comandi script contenuti in una conversione di valuta in base alle specifiche esigenze. Se si sovrascrive la conversione di valuta, le modifiche andranno perdute.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services multidimensionale](globalization-scenarios-for-analysis-services-multiidimensional.md)  
  
  
