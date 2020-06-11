---
title: Creare una dimensione generando una tabella non temporale nell'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 66ac0c2a120e0981ce23c794b97427121ae5eb23
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536783"
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>Creare una dimensione generando una tabella non temporale nell'origine dati
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile utilizzare la creazione guidata dimensione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare una dimensione senza utilizzare un'origine dati esistente. A questo scopo, selezionare l'opzione **Genera una tabella diversa dalla tabella dei tempi nell'origine dati** della pagina **Seleziona metodo di creazione** della procedura guidata. Per creare una nuova tabella della dimensione nell'origine dati sottostanti è necessario disporre delle autorizzazioni per creare oggetti nell'origine dati sottostanti. In caso di definizione di una dimensione senza una vista origine dati predefinita, è possibile sia definire la dimensione da zero sia definirla in base a un modello di dimensione.  
  
 Creazione guidata dimensione offre modelli di dimensione in base ai quali è possibile compilare un tipo di dimensione comune. È possibile scegliere tra i tipi di dimensione seguenti:  
  
-   Account  
  
-   Customer  
  
-   Data  
  
-   department  
  
-   Destination Currency  
  
-   Employee  
  
-   Area geografica  
  
-   Internet Sales Order Details  
  
-   Organization  
  
-   Prodotto  
  
-   Promotion  
  
-   Reseller Sales Order Details  
  
-   Rivenditore  
  
-   Sales Channel  
  
-   Sales Reason  
  
-   Sales Summary Order Details  
  
-   Territorio vendita  
  
-   Scenario  
  
-   Source Currency  
  
 Tutti i modelli standard supportano gli attributi che è possibile includere nella dimensione. È inoltre possibile aggiungere file di modelli personalizzati per le dimensioni che vengono comunemente utilizzate. I modelli di dimensione sono disponibili nella cartella seguente:  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 È possibile utilizzare Progettazione dimensioni al termine della Creazione guidata dimensione per aggiungere, rimuovere e configurare attributi e gerarchie nella dimensione.  
  
 Quando si crea una dimensione non temporale senza utilizzare un'origine dati, Creazione guidata dimensione descrive i passaggi per specificare il tipo di dimensione ed identifica l’attributo chiave e le dimensioni a modifica lenta.  
  
## <a name="specify-dimension-type"></a>Impostazione del tipo di dimensione  
 Nella pagina **Impostazione tipo di dimensione** della Creazione guidata dimensione è possibile specificare il tipo di dimensione. Se si sta compilando la dimensione basata su un modello, il tipo di dimensione viene definito automaticamente. In questa pagina è inoltre possibile selezionare gli attributi standard del tipo di dimensione specificato, se disponibili.  
  
 Se è stato selezionato un modello che corrisponde a un tipo di dimensione, questa pagina viene popolata con le opzioni di quel tipo di dimensione. Se non è stato selezionato un modello o se non esiste un tipo di dimensione corrispondente, il tipo di dimensione predefinito è **Regolare**. Se non è già stato selezionato un tipo di dimensione, scegliere il tipo più appropriato per la dimensione da creare. Se nell'elenco **Tipo di dimensione**non è disponibile alcun tipo appropriato, selezionare **Regolare**.  
  
 Quando si seleziona un tipo di dimensione, durante la procedura guidata in **Attributi dimensione**vengono elencati i tipi di attributi che possono essere applicati alla dimensione. Per selezionare un tipo di attributo, spuntare la casella di controllo **Includi** accanto al tipo di attributo e inserire il nome dell'attributo in **Attributo dimensione**. Il nome predefinito è lo stesso visualizzato in **Tipo di attributo**.  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>Identificazione di attributi chiave e dimensioni modificabili  
 Nella pagina **Impostazione chiave e tipo della dimensione** selezionare l'attributo da impostare come attributo chiave della dimensione. L'attributo chiave generalmente corrisponde alla colonna chiave primaria nella tabella principale della dimensione e indicizza i membri foglia della dimensione.  
  
 Se è stato selezionato un modello, nel quale viene poi definito un attributo chiave, tale attributo sarà l'attributo chiave predefinito. Se è stato selezionato un modello, ma in esso non è stato definito un attributo chiave, il primo attributo dell’elenco sarà l'attributo chiave predefinito. L'elenco contiene tutti gli attributi selezionati nella pagina **Impostazione tipo di dimensione** . Nella pagina **Impostazione tipo di dimensione** è possibile selezionare uno degli attributi selezionati come attributo chiave della dimensione. Se non è stato selezionato alcun attributo, verrà creato automaticamente un attributo chiave il cui nome verrà determinato concatenando il nome e l'"ID" della dimensione.  
  
 Definire infine se la dimensione è una dimensione modificabile. I membri di una dimensione modificabile possono spostarsi, nel tempo, in posizioni diverse all'interno della gerarchia. Durante la procedura guidata vengono generate colonne aggiuntive e vengono creati attributi che corrispondono a queste colonne. Queste colonne permettono agli utenti di consultare la dimensione in tale modalità come fattore nella modifica. Tutti i pacchetti creati successivamente con Generazione guidata schema gestiscono chiavi surrogate basate sulle caratteristiche della dimensione a modifica lenta.  
  
 Selezionando la casella di controllo **Dimensione modificabile** , la Creazione guidata dimensione definisce gli attributi indicati nella seguente tabella:  
  
|Attributo|Type|  
|---------------|----------|  
|ID originale dimensione a modifica lenta|SCDOriginalID|  
|Data fine dimensione a modifica lenta|SCDEndDate|  
|Data inizio dimensione a modifica lenta|SCDStartDate|  
|Stato dimensione a modifica lenta|SCDStatus|  
  
 La casella di controllo **Dimensione modificabile** viene selezionata per impostazione predefinita se si usa un modello per il quale sono stati definiti questi attributi di dimensione a modifica lenta. Se si deseleziona la casella di controllo, gli attributi della dimensione a modifica lenta vengono rimossi dalla dimensione.  
  
 È possibile utilizzare Progettazione dimensioni per configurare le proprietà di una dimensione a modifica lenta.  
  
## <a name="completing-the-dimension-wizard"></a>Completamento di Creazione guidata dimensione  
 Nella pagina **Completamento procedura guidata** assegnare un nome alla nuova dimensione e quindi verificarne la struttura. Selezionare la casella di controllo **Genera schema adesso** per avviare Generazione guidata schema dopo avere fatto clic su **Fine**. Nella maggior parte dei casi non è necessario selezionare questa casella di controllo quando si pianifica la creazione di oggetti aggiuntivi. Se non si seleziona questa casella di controllo, è possibile utilizzare Progettazione dimensioni per generare lo schema in un secondo momento.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una dimensione temporale generando una tabella dei tempi](create-a-time-dimension-by-generating-a-time-table.md)   
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)  
  
  
