---
title: Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e03e55451c2340b5f0773e2873127c3551a82aab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074901"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti (Analysis Services)
  L'autorizzazione per la lettura di una definizione dell'oggetto o dei metadati negli oggetti selezionati consente a un amministratore di concedere l'autorizzazione per la visualizzazione delle informazioni sull'oggetto, senza tuttavia concedere l'autorizzazione per la modifica della definizione dell'oggetto, per la modifica della struttura dell'oggetto o per la visualizzazione dei dati effettivi dell'oggetto. `Read Definition`le autorizzazioni possono essere concesse a livello di database, origine dati, dimensione, struttura di data mining e modello di data mining. Se sono necessarie `Read Definition` autorizzazioni per un cubo, è necessario abilitare `Read Definition` per il database. Tenere presente che le autorizzazioni sono additive. Si supponga, ad esempio, uno scenario in cui un ruolo concede l'autorizzazione per la lettura dei metadati per un cubo, mentre un secondo ruolo concede allo stesso utente l'autorizzazione per la lettura dei metadati per una dimensione. Le autorizzazioni concesse dai due diversi ruoli si sommano, assegnando all'utente l'autorizzazione per la lettura sia dei metadati per il cubo che dei metadati per la dimensione inclusa nel database.  
  
> [!NOTE]  
>  La lettura dei metadati di un database rappresenta l'autorizzazione minima necessaria per la connessione a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Un utente che dispone dell'autorizzazione per la lettura dei metadati può inoltre usare il set di righe dello schema DISCOVER_XML_METADATA per eseguire una query sull'oggetto e visualizzarne i metadati. Per altre informazioni, vedere [Set di righe DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Impostare le autorizzazioni di lettura definizione per un database  
 Quando si concede l'autorizzazione per la lettura dei metadati del database, si concede anche l'autorizzazione per la lettura dei metadati di tutti gli oggetti all'interno del database.  
  
 È consigliabile includere l'autorizzazione a `Read Definition` livello di database ogni volta che si configurano i ruoli per l'elaborazione dedicata. La `Read Definition` possibilità di consentire a non amministratori di visualizzare la gerarchia di oggetti [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] di un modello in e di spostarsi tra i singoli oggetti per l'elaborazione successiva.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di, espandere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **ruoli** per il database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nella scheda **generale** selezionare l' `Read Definition` opzione.  
  
3.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
4.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Impostare le autorizzazioni di lettura definizione per singoli oggetti  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], aprire la cartella **Database** , selezionare un database, espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nel riquadro **generale** deselezionare l'autorizzazione del database per `Read Definition`. Questo passaggio rimuove l'ereditarietà delle autorizzazioni in modo tale da potere impostare le autorizzazioni per i singoli oggetti.  
  
3.  Selezionare l'oggetto per cui si specificano `Read Definition` le proprietà:  
  
    -   Nel riquadro **origini dati** fare clic sulla `Read Definition` casella di controllo relativa a tale origine dati. I membri del ruolo possono visualizzare la stringa di connessione all'origine dati, compresi il nome del server ed eventualmente il nome utente. Questa autorizzazione è disponibile nel caso in cui si desideri fornire le informazioni sulla stringa di connessione, senza tuttavia concedere l'autorizzazione per la modifica della stringa di connessione o per la visualizzazione delle definizioni di altri oggetti.  
  
    -   Nel riquadro **dimensioni** fare clic sulla casella `Read Definition` di controllo relativa alla dimensione. Gli analisti e sviluppatori esperti potrebbero avere l'esigenza di visualizzare la definizione senza l'autorizzazione a modificarla o di visualizzare le definizione di altri oggetti, quali dimensioni, oggetti del cubo o strutture e modelli di data mining.  
  
    -   Nel riquadro strutture di data mining fare clic `Read Definition` sulla casella di controllo per data mining strutture o modelli. `Read Definition`è necessario per esplorare il modello di dati. Per informazioni dettagliate, vedere [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md).  
  
4.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
5.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere autorizzazioni per il database &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
