---
title: Livello di compatibilità per i modelli tabulari in Analysis Services | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19c69aa1a1ab27e7498d3c9d6a0d52c25b9f0020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826826"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Livello di compatibilità per i modelli tabulari di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Il *livello di compatibilità* fa riferimento alle funzionalità avanzate di funzioni e funzionalità in entrambi il motore di Analysis Services e nei metadati di modello tabulare. In generale, è consigliabile scegliere il livello di compatibilità più recente supportato dal server. 

  **Il livello di compatibilità supportato più recente è 1400** 
  
Le funzionalità principali nel livello di compatibilità 1400 includono:

*  Nuova infrastruttura per la connettività dei dati e l'importazione in modelli tabulari con il supporto per APIs TOM e degli script TMSL. In questo modo il supporto per origini dati aggiuntive, ad esempio archiviazione Blob di Azure. Dati aggiuntivi origini saranno inclusi in futuro gli aggiornamenti.
*  Trasformazione dei dati e le funzionalità di mashup di dati usando recupera dati ed espressioni M in SQL Server Data Tools (SSDT).
*  Misura ora il supporto degli strumenti, ad esempio Microsoft Excel drill down per una proprietà di righe di dettaglio con un'espressione DAX, attivazione della BI in dettaglio i dati da un report aggregato. Ad esempio, quando gli utenti visualizzano le vendite totali per un'area e il mese, è possibile visualizzare i dettagli degli ordini associati. 
*  Sicurezza a livello di oggetto per i nomi di tabelle e colonne, oltre ai dati in esse contenute.
*  Supporto avanzato per le gerarchie incomplete.
*  Monitoraggio delle prestazioni e miglioramenti.

  
## <a name="supported-compatibility-levels-by-version"></a>Livelli di compatibilità supportato dalla versione
  
Livelli di compatibilità inferiori sono supportati con le versioni precedenti per la compatibilità. 

|||  
|-|-|- 
|**Livello di compatibilità**|**Versione del server**| 
|1470|SQL Server 2019 (CTP 2.3 e versioni successive) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\* i livelli di compatibilità 1100 e 1103 sono deprecati in SQL Server 2017 e versioni successive.
  
## <a name="set-compatibility-level"></a>Impostare il livello di compatibilità 
 Quando si crea un nuovo progetto di modello tabulare in SQL Server Data Tools (SSDT), è possibile specificare il livello di compatibilità sul **progettazione di modelli tabulari** finestra di dialogo. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Se si seleziona il **non visualizzare più questo messaggio** opzione, tutti i progetti successivi verranno utilizzato il livello di compatibilità specificato come valore predefinito. È possibile modificare il livello di compatibilità predefinito in SSDT in **Strumenti** > **Opzioni**.  
  
 Per aggiornare un progetto di modello tabulare in SSDT, impostare il **livello di compatibilità** proprietà nel modello **proprietà** finestra. Tenere presente, l'aggiornamento del livello di compatibilità è irreversibile.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Controllare il livello di compatibilità per un database in SSMS  
 In SSMS, fare clic sul nome del database > **delle proprietà** > **a livello di compatibilità**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Controllare il livello di compatibilità supportato per un server in SSMS  
 In SSMS fare clic con il pulsante destro del mouse sul nome del server > **Proprietà** > **Livello di compatibilità supportato**.  

 Questa proprietà specifica il massimo livello di compatibilità di un database che verrà eseguito nel server. Il livello di compatibilità supportato è di sola lettura e non può essere modificato.
 
> [!NOTE]  
>  In SSMS, quando si è connessi a un server di SQL Server Analysis Services, server Azure Analysis Services o dell'area di lavoro di Power BI Premium, la proprietà a livello di compatibilità supportato mostrerà 1200. Questo è un problema noto e verrà risolto in un SQL Server Management Studio prossimi aggiornamenti. Quando è stato risolto, questa proprietà indicherà il massimo livello di compatibilità supportato. 
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità di un database multidimensionale](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Creare un nuovo progetto di modello tabulare](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
