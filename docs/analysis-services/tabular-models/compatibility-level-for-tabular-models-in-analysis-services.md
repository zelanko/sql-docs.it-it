---
title: Livello di compatibilità per i modelli tabulari in Analysis Services | Microsoft Docs
ms.date: 05/14/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 45ea2e048a7ea7ae7d041614d62a280ee3698131
ms.sourcegitcommit: 4cb96c291529e9bdf0a95fb3610b350583eb36d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65709119"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Livello di compatibilità per i modelli tabulari di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Il *livello di compatibilità* fa riferimento ai comportamenti specifici di ogni versione nel motore di Analysis Services. Ad esempio, DirectQuery e i metadati degli oggetti tabulari hanno implementazioni diverse a seconda del livello di compatibilità. In generale, è consigliabile scegliere il livello di compatibilità più recente supportato dal server.

  **Il livello di compatibilità supportato più recente è 1400** 
  
Le funzionalità principali nel livello di compatibilità 1400 includono:

*  Nuova infrastruttura per la connettività dei dati e l'importazione in modelli tabulari con il supporto per APIs TOM e degli script TMSL. In questo modo il supporto per origini dati aggiuntive, ad esempio archiviazione Blob di Azure. Dati aggiuntivi origini saranno inclusi in futuro gli aggiornamenti.
*  Trasformazione dei dati e le funzionalità di mashup dei dati usando recupera dati ed espressioni M in SSDT.
*  Le misure ora supportano una proprietà di righe di dettaglio con un'espressione DAX, l'abilitazione di strumenti di Business Intelligence, ad esempio Microsoft Excel il drill-down per i dati dettagliati da un report aggregato. Ad esempio, quando gli utenti finali visualizzano le vendite totali per un'area e il mese, è possibile visualizzare i dettagli degli ordini associati. 
*  Sicurezza a livello di oggetto per i nomi di tabelle e colonne, oltre ai dati in esse contenute.
*  Supporto avanzato per le gerarchie incomplete.
*  Monitoraggio delle prestazioni e miglioramenti.

  
## <a name="supported-compatibility-levels-by-version"></a>Livelli di compatibilità supportato dalla versione
  
|||  
|-|-|- 
|**Livello di compatibilità**|**Versione del server**| 
|1470|SQL Server 2019 (CTP 2.3 e versioni successive) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\* i livelli di compatibilità 1100 e 1103 sono deprecati in SQL Server 2017.
  
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
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità di un database multidimensionale](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Creare un nuovo progetto di modello tabulare](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
