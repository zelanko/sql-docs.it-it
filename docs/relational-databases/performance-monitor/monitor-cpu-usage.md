---
title: Monitorare l'uso della CPU | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], CPU usage
- tuning databases [SQL Server], CPU usage
- processors [SQL Server], monitoring usage
- database performance [SQL Server], CPU usage
- monitoring CPU usage [SQL Server]
- server performance [SQL Server], CPU usage
- database monitoring [SQL Server], CPU usage
- monitoring [SQL Server], CPU usage
- processors [SQL Server]
- CPU [SQL Server], monitoring
- monitoring server performance [SQL Server], CPU usage
ms.assetid: 2a02a3b6-07b2-4ad0-8a24-670414d19812
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: eb73d1b82d1a58a756c2ec6287429cee88315fd7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68091028"
---
# <a name="monitor-cpu-usage"></a>Monitorare l'utilizzo della CPU
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È opportuno monitorare periodicamente un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per verificare che i valori di utilizzo della CPU rientrino nei normali intervalli. Se la frequenza di utilizzo della CPU è costantemente elevata può essere necessario eseguire un aggiornamento della CPU o aggiungere più processori. Una valore costantemente elevato di utilizzo della CPU può inoltre indicare la presenza di un'applicazione non progettata o ottimizzata correttamente. L'ottimizzazione dell'applicazione potrebbe ridurre l'utilizzo della CPU.  
  
 Una soluzione efficiente per determinare l'utilizzo della CPU consiste nell'usare il contatore **Processore:% Tempo processore** in Monitoraggio di sistema. Questo contatore consente di monitorare la quantità di tempo utilizzata dalla CPU per l'esecuzione di un thread non inattivo. Se il valore relativo a tale stato è incluso tra l'80% e il 90%, può essere necessario eseguire un aggiornamento della CPU o aggiungere ulteriori processori. Nel caso dei sistemi multiprocessore, è necessario monitorare un'istanza del contatore per ogni processore. Il valore rappresenta il tempo totale di un processore specifico. Per determinare la media di tutti i processori, usare il contatore **Sistema: % Tempo totale processore** .  
  
 Facoltativamente, per monitorare l'utilizzo del processore è inoltre possibile utilizzare i contatori seguenti:  
  
-   **Processore: % Tempo privilegiato**  
  
     Indica la percentuale di tempo richiesta dal processore per l'esecuzione dei comandi kernel di Microsoft Windows, ad esempio l'elaborazione delle richieste di I/O di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se il valore di questo contatore è costantemente elevato e anche i contatori **Disco fisico** presentano valori elevati, valutare la possibilità di installare un sottosistema di disco più veloce o più efficiente.  
  
    > [!NOTE]  
    >  I diversi tipi di controller del disco e driver utilizzano quantità diverse di tempo di elaborazione del kernel. I controller e i driver efficienti richiedono meno tempo privilegiato, lasciando una maggior quantità di tempo di elaborazione disponibile per le applicazioni utente, migliorando di conseguenza il throughput generale.  
  
-   **Processore: % Tempo utente**  
  
     Indica la percentuale di tempo richiesta dal processore per l'esecuzione dei processi utente, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Sistema: Lunghezza coda processore**  
  
     Indica il numero di thread in attesa di elaborazione. Se i thread di un processo richiedono un numero di cicli del processore maggiore di quello disponibile, si verifica un collo di bottiglia a livello del processore. Se una quantità notevole di processi tenta di utilizzare il tempo del processore, può essere necessario installare un processore più veloce o, nel caso di sistemi multiprocessore, aggiungere un processore.  
  
 Quando si analizza l'utilizzo del processore, è necessario tenere presente il tipo di attività eseguita dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue numerosi calcoli, ad esempio query che riguardano aggregazioni o query gestite in memoria che non richiedono I/O su disco, è possibile che venga utilizzato il 100% del tempo del processore. In tal caso, se le prestazioni delle altre applicazioni peggiorano, provare a modificare il carico di lavoro, ad esempio dedicando il computer all'esecuzione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I valori di utilizzo prossimi al 100%, sintomo dell'elaborazione di numerose richieste client, possono indicare la presenza di processi in coda in attesa del tempo del processore che causano un collo di bottiglia. Risolvere il problema aggiungendo processori più veloci.  
  
  
