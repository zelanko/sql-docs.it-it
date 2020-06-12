---
title: Dimensioni abilitate per la scrittura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
author: minewiskan
ms.author: owend
ms.openlocfilehash: f8f0f1c959d44b4d3e133e5676e9aca9365a628d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545093"
---
# <a name="write-enabled-dimensions"></a>Dimensioni abilitate per la scrittura
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 I dati di una dimensione sono in genere di sola lettura. In determinati scenari, tuttavia, può rivelarsi utile abilitare una dimensione per la scrittura. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , l'abilitazione per la scrittura di una dimensione consente agli utenti aziendali di modificare il contenuto della dimensione e di visualizzare l'effetto immediato delle modifiche sulle gerarchie della dimensione. È possibile abilitare per la scrittura qualsiasi dimensione basata su una singola tabella. In una dimensione abilitata per la scrittura, gli amministratori e gli utenti aziendali possono modificare, spostare, aggiungere ed eliminare membri all'interno della dimensione. Tali operazioni di aggiornamento vengono definite collettivamente come *writeback della dimensione*.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta il writeback della dimensione in tutti gli attributi della dimensione e in qualsiasi membro di una dimensione che sia possibile modificare. Per una partizione o un cubo abilitato per la scrittura, gli aggiornamenti vengono archiviati in una tabella writeback separata dalle tabelle di origine del cubo. Per una dimensione abilitata per la scrittura, tuttavia, le modifiche vengono registrate direttamente nella tabella della dimensione. Inoltre, se la dimensione abilitata per la scrittura è inclusa in un cubo con più partizioni in cui alcune o tutte le origini dei dati contengono copie della tabella della dimensione, durante un processo di writeback verrà aggiornata solo la tabella della dimensione originale.  
  
 Le dimensioni e i cubi abilitati per la scrittura hanno caratteristiche diverse ma complementari. Una dimensione abilitata per la scrittura consente agli utenti aziendali di aggiornare i membri, mentre un cubo abilitato per la scrittura consente loro di aggiornare i valori delle celle. Sebbene queste due caratteristiche siano complementari, non è necessario utilizzarle in combinazione. Per l'esecuzione del writeback della dimensione non è necessario che una dimensione venga inclusa in un cubo. Una dimensione abilitata per la scrittura può anche essere inclusa in un cubo non abilitato per la scrittura. Le procedure utilizzate per abilitare per la scrittura le dimensioni e i cubi e per gestirne la sicurezza sono diverse.  
  
 Al writeback della dimensione vengono applicate le restrizioni seguenti:  
  
-   Quando si crea un nuovo membro, è necessario includere ogni attributo di una dimensione. Non è possibile inserire un membro senza specificare un valore per l'attributo chiave della dimensione. La creazione di membri è pertanto soggetta a tutti i vincoli, ad esempio valori di chiave non Null, definiti nella tabella della dimensione.  
  
-   Il writeback della dimensione è supportato solo per gli schemi star. In altre parole, una dimensione deve essere basata su un'unica tabella della dimensione correlata direttamente a una tabella dei fatti. Dopo avere abilitato per la scrittura una dimensione, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] questi requisiti vengono convalidati quando si esegue la distribuzione a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente o quando si compila un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 È possibile modificare o eliminare qualsiasi membro esistente di una dimensione writeback. Quando un membro viene eliminato, l'eliminazione viene propagata a tutti i membri figlio. In una dimensione Customer contenente gli attributi CountryRegion, Province, City e Customer, l'eliminazione di un paese/regione provocherebbe, ad esempio, l'eliminazione di tutte le province e città e di tutti i clienti appartenenti al paese/regione eliminato. Se un paese/regione include una sola provincia, eliminando tale provincia verrebbe eliminato anche il paese/regione.  
  
 I membri di una dimensione writeback possono essere spostati solo all'interno dello stesso livello. Una città, ad esempio, può essere spostata al livello City in un diverso paese/regione o provincia, ma non può essere spostata al livello Province o CountryRegion. In una gerarchia padre-figlio tutti i membri sono membri foglia e pertanto un membro può essere spostato in qualsiasi livello ad esclusione del livello `(All)`.  
  
 Se un membro di una gerarchia padre-figlio viene eliminato, i figli del membro vengono spostati nell'elemento padre del membro. Nel membro eliminato sono necessarie le autorizzazioni di aggiornamento per la tabella relazionale, mentre nei membri spostati non è richiesta alcuna autorizzazione. Quando tramite un'applicazione viene spostato un membro in una gerarchia padre-figlio, nell'operazione UPDATE è possibile specificare se i discendenti del membro devono essere spostati con il membro oppure spostati nell'elemento padre del membro. Per eliminare in modo ricorsivo un membro in una gerarchia padre-figlio, è necessario che l'utente disponga delle autorizzazioni di aggiornamento per la tabella relazionale sia per il membro che per tutti i relativi discendenti.  
  
> [!NOTE]  
>  Gli aggiornamenti all'attributo padre in una gerarchia padre-figlio non devono includere aggiornamenti ad altre proprietà o altri attributi.  
  
 Tutte le modifiche a una dimensione provocano la modifica della struttura della dimensione. Ogni modifica a una dimensione viene considerata come transazione singola, che necessita di elaborazione incrementale per l'aggiornamento della struttura della dimensione. Le dimensioni abilitate per la scrittura hanno gli stessi requisiti di elaborazione delle altre dimensioni.  
  
> [!NOTE]  
>  Il writeback della dimensione non è supportato dalle dimensioni collegate.  
  
## <a name="security"></a>Sicurezza  
 Gli unici utenti aziendali autorizzati ad aggiornare una dimensione abilitata per la scrittura sono quelli inclusi nei ruoli del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a cui sono state concesse le autorizzazioni di lettura/scrittura nella dimensione. Per ogni ruolo, è possibile impostare i membri che possono o meno essere aggiornati. Affinché gli utenti aziendali possano aggiornare le dimensioni abilitate per la scrittura, è necessario che le applicazioni client utilizzate supportino questa funzionalità. Per tali utenti, è necessario che la dimensione abilitata per la scrittura sia inclusa in un cubo elaborato dopo l'ultima modifica della dimensione. Per altre informazioni, vedere [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
 Gli utenti e i gruppi inclusi nel ruolo Administrators possono aggiornare i membri degli attributi di una dimensione abilitata per la scrittura, anche se la dimensione non è inclusa in un cubo.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà delle dimensioni del database](database-dimension-properties.md)   
 [Partizioni abilitate per la scrittura](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
