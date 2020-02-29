---
title: Aggiornare lo schema in una vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data source views [Analysis Services], schema updates
- refreshing data source views
- data source views [Analysis Services], refreshing
ms.assetid: 634b0504-1437-43e7-8ac7-3248ac7989a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d11ac65a565df23332f24eef8a3e4ddb4e476a5
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175710"
---
# <a name="refresh-the-schema-in-a-data-source-view-analysis-services"></a>Aggiornare lo schema in una vista origine dati (Analysis Services)
  Dopo la definizione di una vista origine dati in un database o un progetto di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , è possibile che lo schema di un'origine dati sottostante venga modificato. Tali modifiche non vengono automaticamente rilevate o aggiornate in un progetto di sviluppo. Inoltre, se è stato distribuito il progetto in un server, verranno rilevati errori di elaborazione qualora non sia più possibile la connessione di Analysis Services all'origine dati esterna.

 Per aggiornare la vista origine dati in modo che corrisponda all'origine dati esterna, è possibile aggiornare la vista origine dati in Business Intelligence Development Studio (BIDS). L'aggiornamento della vista origine dati consente di rilevare le modifiche apportate alle origini dati esterne su cui è basata la vista origine dati, nonché di compilare un elenco di modifiche in cui vengono enumerate le aggiunte o le eliminazioni nell'origine dati esterna. È possibile applicare quindi il set di modifiche alla vista origine dati che verrà riallineata all'origine dati sottostante. Si noti che sono spesso necessarie operazioni aggiuntive per aggiornare ulteriormente i cubi e le dimensioni nel progetto in cui viene utilizzata la vista origine dati.

 Questo argomento include le sezioni seguenti:

 [Modifiche supportate nell'aggiornamento](#bkmk_changlist)

 [Aggiornare una vista origine dati in SQL Server Data Tools](#bkmk_DSVrefresh)

##  <a name="bkmk_changlist"></a>Modifiche supportate nell'aggiornamento
 Nell'aggiornamento della vista origine dati sono incluse le azioni seguenti:

-   Eliminazione di tabelle, colonne e relazioni

-   Aggiunta di colonne e relazioni, applicate a tabelle già incluse nella vista origine dati

-   Aggiunta di nuovi vincoli univoci. Se nella vista origine dati esiste una chiave primaria logica per una tabella e viene aggiunta una chiave fisica alla tabella nell'origine dati, la chiave logica verrà rimossa e sostituita dalla chiave fisica.

 L'aggiornamento non implica mai l'aggiunta di nuove tabelle a una vista origine dati. Se si desidera aggiungere una nuova tabella, è necessario effettuare tale operazione manualmente. Per altre informazioni, vedere [Aggiunta o rimozione di tabelle o viste in una vista origine dati &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md).

##  <a name="bkmk_DSVrefresh"></a>Aggiornare una vista origine dati in SQL Server Data Tools
 Per aggiornare una vista origine dati, fare doppio clic su di essa in Esplora soluzioni di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e quindi fare clic sul pulsante Aggiorna vista origine dati o scegliere **Aggiorna** dal menu Vista origine dati.

 Durante l'aggiornamento, in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] vengono eseguite query su tutte le origini dati relazionali sottostanti per determinare se sono state apportate modifiche nelle tabelle o nelle viste incluse nella vista origine dati. Se è possibile stabilire connessioni a tutte le origini dati sottostanti e sono state apportate modifiche, queste verranno visualizzate nella finestra di dialogo **Aggiorna vista origine dati** .

 ![Finestra di dialogo Aggiorna vista origine dati](../media/ssas-olapdsv-refresh.gif "Finestra di dialogo Aggiorna vista origine dati")

 Nella finestra di dialogo vengono elencati tabelle, colonne, vincoli e relazioni che verranno eliminati o aggiunti nella vista origine dati. Inoltre, nel report viene elencato un calcolo o una query denominata che non è possibile preparare correttamente. Gli oggetti interessati vengono elencati in una visualizzazione albero contenente le colonne e le relazioni nidificate nelle tabelle e il tipo di modifica (eliminazione o aggiunta) indicata per ogni oggetto. Le icone di oggetti della vista origine dati standard indicano il tipo di oggetto interessato.

 L'aggiornamento è basato esclusivamente sui nomi degli oggetti sottostanti. Se pertanto un oggetto sottostante viene rinominato nell'origine dei dati, Progettazione vista origine dati considera l'oggetto rinominato come due operazioni separate, un'eliminazione e un'aggiunta. In tal caso, potrebbe essere necessario raggiungere manualmente l'oggetto rinominato nella vista origine dati, nonché ricreare le relazioni o le chiavi primarie logiche.

> [!IMPORTANT]
>  Se è stata rinominata una tabella in un'origine dei dati, è possibile usare il comando **Sostituisci tabella** per sostituire la tabella con quella rinominata prima di aggiornare la vista origine dati. Per altre informazioni, vedere [Sostituire una tabella o una query denominata in una vista origine dati &#40;Analysis Services&#41;](replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md).

 Dopo aver esaminato il report, è possibile accettare le modifiche oppure annullare l'aggiornamento e rifiutare così qualsiasi modifica. Tutte le modifiche devono essere accettate o rifiutate insieme. Non è possibile scegliere elementi singoli nell'elenco. È inoltre possibile salvare un report delle modifiche.

## <a name="see-also"></a>Vedere anche
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)


