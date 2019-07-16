---
title: Concessione di autorizzazioni di lettura definizione per i metadati degli oggetti (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6cc110a773981a7592f8cdd06b3fd10b2d83144
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208827"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  L'autorizzazione per la lettura di una definizione dell'oggetto o dei metadati negli oggetti selezionati consente a un amministratore di concedere l'autorizzazione per la visualizzazione delle informazioni sull'oggetto, senza tuttavia concedere l'autorizzazione per la modifica della definizione dell'oggetto, per la modifica della struttura dell'oggetto o per la visualizzazione dei dati effettivi dell'oggetto. Le autorizzazioni**Lettura definizione** possono essere concesse a livello di database, origine dati, dimensione, struttura di data mining e modello di data mining. Se sono necessarie le autorizzazioni **Lettura definizione** per un cubo, abilitare l'opzione **Lettura definizione** per il database. Tenere presente che le autorizzazioni si sommano tra loro. Si supponga, ad esempio, uno scenario in cui un ruolo concede l'autorizzazione per la lettura dei metadati per un cubo, mentre un secondo ruolo concede allo stesso utente l'autorizzazione per la lettura dei metadati per una dimensione. Le autorizzazioni concesse dai due diversi ruoli si sommano, assegnando all'utente l'autorizzazione per la lettura sia dei metadati per il cubo che dei metadati per la dimensione inclusa nel database.  
  
> [!NOTE]  
>  La lettura dei metadati di un database rappresenta l'autorizzazione minima necessaria per la connessione a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Un utente che dispone dell'autorizzazione per la lettura dei metadati può inoltre usare il set di righe dello schema DISCOVER_XML_METADATA per eseguire una query sull'oggetto e visualizzarne i metadati. Per altre informazioni, vedere [Set di righe DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Impostare le autorizzazioni di lettura definizione per un database  
 Quando si concede l'autorizzazione per la lettura dei metadati del database, si concede anche l'autorizzazione per la lettura dei metadati di tutti gli oggetti all'interno del database.  
  
 È consigliabile includere l'autorizzazione **Lettura definizione** a livello di database quando si configurano i ruoli per un'elaborazione dedicata. L'autorizzazione **Lettura definizione** consente agli utenti non amministratori di visualizzare la gerarchia degli oggetti di un modello in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e di visualizzare i singoli oggetti per l'elaborazione successiva.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nella scheda **Generale** selezionare l'opzione **Lettura definizione** .  
  
3.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
4.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Impostare le autorizzazioni di lettura definizione per singoli oggetti  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], aprire la cartella **Database** , selezionare un database, espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nel riquadro **Generale** deselezionare l'autorizzazione del database per **Lettura definizione**. Questo passaggio rimuove l'ereditarietà delle autorizzazioni in modo tale da potere impostare le autorizzazioni per i singoli oggetti.  
  
3.  Selezionare l'oggetto per il quale specificare le proprietà **Lettura definizione** :  
  
    -   Nel riquadro **Origini dati** fare clic sulla casella di controllo **Lettura definizione** per l'origine dati. I membri del ruolo possono visualizzare la stringa di connessione all'origine dati, compresi il nome del server ed eventualmente il nome utente. Questa autorizzazione è disponibile nel caso in cui si desideri fornire le informazioni sulla stringa di connessione, senza tuttavia concedere l'autorizzazione per la modifica della stringa di connessione o per la visualizzazione delle definizioni di altri oggetti.  
  
    -   Nel riquadro **Dimensioni** fare clic sulla casella di controllo **Lettura definizione** per la dimensione. Gli analisti e sviluppatori esperti potrebbero avere l'esigenza di visualizzare la definizione senza l'autorizzazione a modificarla o di visualizzare le definizione di altri oggetti, quali dimensioni, oggetti del cubo o strutture e modelli di data mining.  
  
    -   Nel riquadro Strutture di data mining fare clic sulla casella di controllo **Lettura definizione** per le strutture o i modelli di data mining. L'autorizzazione **Lettura definizione** è obbligatoria per l'esplorazione del modello di dati. Per informazioni dettagliate, vedere [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md).  
  
4.  Nel riquadro **Appartenenza** immettere gli account utente e di gruppo di Windows che si connettono ad Analysis Services con questo ruolo.  
  
5.  Fare clic su **OK** per completare la creazione del ruolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere le autorizzazioni per il database &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
