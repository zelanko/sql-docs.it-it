---
title: Limiti della capacità di calcolo per edizione di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7a32b00ec6ad34095a17816406eb5516207fafa1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013019"
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>Limiti della capacità di calcolo per edizione di SQL Server
  In questo argomento si illustrano i limiti della capacità di calcolo per differenti edizioni di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e le differenze in ambienti fisici e virtualizzati con i processori con l'Hyper-Threading.  
  
 ![Mapping per il calcolo dei limiti della capacità](../../2014/getting-started/media/compute-capacity-limits.gif "Mapping per il calcolo dei limiti della capacità")  
  
 Nella tabella seguente vengono descritte le notazioni utilizzate nel diagramma sopra riportato:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0..1|Zero o uno|  
|1|Esattamente uno|  
|1..*|Uno o più|  
|0..*|Zero o più|  
|1..2|Uno o due|  
  
> [!IMPORTANT]
>  Per un'ulteriore elaborazione:  
> 
>  1.  Una macchina virtuale viene allocata per uno o più processori virtuali.  
> 2.  Uno o più processori virtuali sono allocati a esattamente una macchina virtuale.  
> 3.  Viene eseguito il mapping a zero o più processori logici di zero o un processore virtuale. Quando il mapping del processore virtuale al processore logico è:  
> 
>      -   Uno-a-zero, che rappresenta un processore logico non associato non utilizzato dai sistemi operativi guest.  
>     -   Uno a molti, che rappresenta un overcommit.  
>     -   Zero-a-molti, che rappresenta l'assenza di una macchina virtuale sul sistema host, pertanto non è utilizzato alcun processore logico dalle VM.  
> 4.  Viene eseguito il mapping di un socket a zero o a più core. Quando il mapping da socket a core è:  
> 
>      -   Uno-a-zero, che rappresenta un socket vuoto (alcun chip installato).  
>     -   Uno-a-uno, che rappresenta un chip singole-core installato nel socket (molto raro).  
>     -   Uno a molti, che rappresenta un multi-core installato nel socket (i valori tipici sono 2,4,8).  
> 5.  Viene eseguito il mapping di un core a uno o due processori logici. Quando il mapping del core al processore logico è:  
> 
>      -   Uno-a-uno, l'Hyper-Threading è disabilitato.  
>     -   Uno-a-due, l'Hyper-Threading è abilitato.  
  
 Le definizioni seguenti si riferiscono ai termini utilizzati in tutto questo argomento:  
  
-   Un thread o un processore logico è un motore di calcolo logico dalla prospettiva di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], del sistema operativo, di un'applicazione o un driver.  
  
-   Un core è un'unità del processore che può essere costituita da uno o più processori logici.  
  
-   Un processore fisico può essere costituito da uno o più core. Un processore fisico corrisponde a un pacchetto del processore o a un socket.  
  
 Sistemi con più processori fisici o sistemi con processori fisici che dispongono di più core e/o Hyper-thread consentono al sistema operativo di eseguire più attività simultaneamente. Ogni thread di esecuzione viene visualizzato come un processore logico. Ad esempio, se si dispone di un computer che dispone di due processori quad core con l'Hyper-Threading abilitato e due thread per core, si dispone di 16 processori logici: 2 processori x 4 core per processore x 2 thread per core. Vale la pena notare che:  
  
-   La capacità di calcolo di un processore logico da un solo thread di un core con l'Hyper-Threading è inferiore alla capacità di calcolo di un processore logico da quello stesso core con l'Hyper-Threading disabilitato.  
  
-   Tuttavia, la capacità di calcolo dei 2 processori logici nel core con l'Hyper-Threading è maggiore della capacità di calcolo dello stesso core con l'Hyper-Threading disabilitato.  
  
 Ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dispone di due limiti di capacità di calcolo:  
  
1.  Un numero massimo di socket (uguale al processore fisico o al socket o al pacchetto del processore).  
  
2.  Un numero massimo di core come riportato dal sistema operativo.  
  
 Questi limiti si applicano a una sola istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Rappresentano la capacità di calcolo massima che verrà utilizzata da una sola istanza. Non vincolano il server sul quale potrebbe essere distribuita l'istanza. Infatti la distribuzione di più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sullo stesso server fisico è un modo efficiente di utilizzare la capacità di calcolo di un server fisico con più socket e/o core dei limiti di capacità riportati di seguito.  
  
 Nella tabella seguente vengono specificati i limiti della capacità di calcolo per una sola istanza di ogni edizione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Edition|Capacità di calcolo massima utilizzata da una sola istanza ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|Capacità di calcolo massima utilizzata da una sola istanza (AS, RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition: licenze basate su Core<sup>1</sup>|Valore massimo del sistema operativo|Valore massimo del sistema operativo|  
|Developer|Valore massimo del sistema operativo|Valore massimo del sistema operativo|  
|Valutazione|Valore massimo del sistema operativo|Valore massimo del sistema operativo|  
|Business Intelligence|Limitato a meno di 4 socket o 16 core|Valore massimo del sistema operativo|  
|Standard|Limitato a meno di 4 socket o 16 core|Limitato a meno di 4 socket o 16 core|  
|Web|Limitato a meno di 4 socket o 16 core|Limitato a meno di 4 socket o 16 core|  
|Express|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|  
|Express with Tools|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|  
|Express with Advanced Services|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|  
  
 <sup>1</sup> la licenza basata su Enterprise Edition con server + licenza CAL (Client Access License) (non disponibile per nuovi contratti) è limitata a un massimo di 20 Core per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanza. Non sono previsti limiti nel modello di licenza server basato su core.  
  
 In un ambiente virtualizzato, il limite della capacità di calcolo è basato sul numero di processori logici non core, perché l'architettura del processore non è visibile alle applicazioni guest.  Ad esempio, un server con quattro socket popolati con processori quad-core e la capacità di abilitare due Hyper-Thread per core contiene 32 processori logici con l'Hyper-Threading abilitato ma solo 16 processori logici con l'Hyper-Threading disabilitato. È possibile eseguire il mapping di questi processori logici alle macchine virtuali sul server con il carico di calcolo delle macchine virtuali su quel processore logico di cui è stato eseguito il mapping in un thread di esecuzione nel processore fisico nel server host.  
  
 È necessario disabilitare l'Hyper-Threading quando le prestazioni per processore virtuale sono importanti. È possibile abilitare o disabilitare l'Hyper-Threading utilizzando una impostazione BIOS per il processore durante l'impostazione del BIOS, ma è in genere un'operazione con ambito server che avrà un impatto su tutti i carichi di lavoro in esecuzione sul server. In tale situazione potrebbe essere consigliabile dividere i carichi di lavoro che saranno in esecuzione negli ambienti virtualizzati da quelli che beneficeranno del miglioramento delle prestazioni dell'Hyper-Threading in un ambiente fisico del sistema operativo.  
  
## <a name="see-also"></a>Vedere anche  
 [Edizioni e componenti di SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Specifiche di capacità massima per SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [Guida introduttiva all'installazione di SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
