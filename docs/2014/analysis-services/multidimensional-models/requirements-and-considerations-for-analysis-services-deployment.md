---
title: Considerazioni per l'analisi e i requisiti di distribuzione dei servizi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6759c38aa519979bdf05ba8848aaccbb89f37a94
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376923"
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Requisiti e considerazioni per la distribuzione di Analysis Services
  Le prestazioni e la disponibilità di una soluzione dipendono da molti fattori, tra cui le funzionalità dell'hardware sottostante, la topologia della distribuzione server, le caratteristiche della soluzione (ad esempio, con partizioni distribuite in più server o usando l'archiviazione ROLAP per la quale è richiesto l'accesso diretto al motore relazionale), i contratti di servizio e la complessità del modello di dati.  
  
## <a name="memory-and-processor-requirements"></a>Requisiti relativi a memoria e processore  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è necessaria una quantità maggiore di risorse di memoria e processore nei casi seguenti:  
  
-   In caso di elaborazione di cubi di grandi dimensioni o complessi. Questi cubi richiedono maggiori risorse di memoria e processore rispetto ai cubi di piccole dimensioni o semplici.  
  
-   In caso di aumento del numero di cubi in un unico database.  
  
-   In caso di aumento del numero di database in un'unica istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   In caso di aumento del numero di istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un unico computer.  
  
-   In caso di aumento del numero di utenti che accedono contemporaneamente alle risorse di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Il numero di risorse in termini di memoria e processore disponibili per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] varia a seconda dell'edizione di SQL Server, del sistema operativo, della capacità hardware e se si usano processori virtuali o fisici. Per altre informazioni, vedere i collegamenti seguenti:  
  
 [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [Limiti della capacità di calcolo per edizione di SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
 [Specifiche di capacità massima &#40;Analysis Services&#41;](olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>Requisiti relativi allo spazio su disco  
 Per i diversi aspetti dell'installazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e le diverse attività correlate all'elaborazione degli oggetti sono necessarie quantità di spazio su disco differenti. Nell'elenco seguente vengono descritti questi requisiti.  
  
 Cubi  
 I cubi che includono tabelle dei fatti di grandi dimensioni richiedono una quantità maggiore di spazio su disco rispetto a quelli contenenti tabelle dei fatti di piccole dimensioni. Analogamente, sebbene in proporzioni minori, i cubi che includono un numero elevato di dimensioni grandi richiedono una maggiore quantità di spazio su disco rispetto ai cubi che contengono un numero minore di membri della dimensione. In genere, un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] richiede approssimativamente il 20% dello spazio su disco necessario per gli stessi dati archiviati nel database relazionale sottostante.  
  
 Aggregations  
 Le aggregazioni richiedono ulteriore spazio proporzionale alle aggregazioni aggiunto, il più le aggregazioni sono disponibili, è necessario più spazio. Se si evita la creazione di aggregazioni non necessarie, lo spazio su disco aggiuntivo necessario per le aggregazioni non supera in genere il 10% circa della dimensione dei dati archiviati nel database relazionale sottostante.  
  
 Data Mining  
 Per impostazione predefinita, le strutture di data mining memorizzano nella cache il set di dati in cui viene eseguito il training. Per rimuovere dal disco i dati presenti nella cache, è possibile usare l'opzione di elaborazione **Elaborazione struttura pulita** nell'oggetto struttura di data mining. Per altre informazioni, vedere [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Elaborazione di oggetti  
 Durante l'elaborazione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivia le copie degli oggetti in fase di elaborazione nella transazione di elaborazione sul disco fino al termine del processo. Al termine dell'elaborazione, le copie elaborate degli oggetti sostituiscono gli oggetti originali. È pertanto necessario verificare che vi sia spazio su disco aggiuntivo sufficiente per una seconda copia di ogni oggetto da elaborare. Se, ad esempio, si desidera elaborare un intero cubo in un'unica transazione, è necessario disporre di spazio su disco sufficiente per l'archiviazione di una seconda copia dell'intero cubo.  
  
##  <a name="BKMK_Availability"></a> Considerazioni sulla disponibilità  
 In un ambiente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un cubo o un modello di data mining potrebbe non essere disponibile per l'esecuzione di query a causa di un problema hardware o software. Un cubo potrebbe inoltre non essere disponibile in quanto necessita di essere elaborato.  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>Metodi per garantire la disponibilità in caso di problemi hardware o software  
 I componenti hardware o software possono presentare problemi per vari motivi. Per garantire la disponibilità dell'installazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non è tuttavia sufficiente risolvere questi problemi, ma è anche necessario offrire risorse alternative che consentano all'utente di continuare a usare un sistema in caso di errore. Spesso per offrire le risorse alternative necessarie a mantenere la disponibilità in caso di problema hardware o software vengono usati server di clustering o di bilanciamento del carico.  
  
 Per offrire un'alternativa in caso di problema hardware o software, valutare l'opportunità di distribuire [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un cluster di failover. In un cluster di failover se nel nodo primario si verifica un errore per qualsiasi motivo oppure se è necessario riavviare tale nodo, le funzionalità di clustering di failover di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows consentono di eseguire il failover a un nodo secondario. Dopo il failover, che avviene in modo molto rapido, quando gli utenti eseguono query accedono all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel nodo secondario. Per altre informazioni sui cluster di failover, vedere [tecnologie di Windows Server:  I cluster di failover](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx).  
  
 Un'altra soluzione utile per risolvere i problemi di disponibilità consiste nel distribuire il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in due o più server di produzione. Sarà quindi possibile usare la funzionalità di bilanciamento del carico di rete dei server Windows per combinare i server di produzione in un unico cluster. In un cluster con bilanciamento carico di rete, se un server non è disponibile a causa di problemi hardware o software, tramite il servizio di bilanciamento carico di rete le query degli utenti vengono indirizzate ai server ancora disponibili.  
  
### <a name="providing-availability-while-processing-structural-changes"></a>Metodi per garantire la disponibilità durante l'elaborazione di modifiche strutturali  
 Determinate modifiche apportate a un cubo possono rendere i l cubo non disponibile fino al termine dell'elaborazione. Se, ad esempio, si apportano modifiche strutturali a una dimensione in un cubo, non è sufficiente rielaborare la dimensione, ma è necessario elaborare anche ogni cubo che usano la dimensione modificata. Durante l'elaborazione di tali cubi, gli utenti non possono eseguire query su di essi né sui modelli di data mining basati su un cubo contenente una dimensione modificata.  
  
 Per offrire la disponibilità durante l'elaborazione di modifiche strutturali che potrebbero riguardare uno o più cubi in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , valutare l'opportunità di usare un server dell'area di gestione temporanea e la Sincronizzazione guidata database. Questa funzionalità consente di aggiornare i dati e i metadati in un server dell'area di gestione temporanea e quindi di eseguire una sincronizzazione online del server di produzione e del server dell'area di gestione temporanea. Per altre informazioni, vedere [Sincronizzare database di Analysis Services](synchronize-analysis-services-databases.md).  
  
 Per elaborare in modo trasparente gli aggiornamenti incrementali ai dati di origine, abilitare il caching attivo. Tramite il caching attivo i cubi vengono aggiornati con i nuovi dati di origine senza che sia necessaria l'elaborazione manuale e senza influire sulla disponibilità dei cubi. Per altre informazioni, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
##  <a name="BKMK_Scalability"></a> Considerazioni sulla scalabilità  
 La presenza di più istanze di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nello stesso computer può causare problemi di prestazioni. Per risolvere questi problemi, un'opzione consiste nell'aumentare le risorse di memoria, processore e disco nel server. Potrebbe inoltre essere necessario distribuire le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in più computer.  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>Distribuzione di Analysis Services in più computer  
 È possibile distribuire un'installazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in più computer in diversi modi. Le opzioni disponibili sono descritte nell'elenco seguente.  
  
-   Se vi sono più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un unico computer, è possibile spostare una o più istanze in un altro computer.  
  
-   Se vi sono più database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un unico computer, è possibile spostare uno o più database nella relativa istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un computer diverso.  
  
-   Se uno o più database relazionali forniscono dati a un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile spostare questi database in un computer diverso. Prima di spostare i database, valutare la velocità di rete e la larghezza di banda tra il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e i database sottostanti. Se la rete è lenta o sovraccarica, lo spostamento dei database sottostanti in un computer diverso influirà negativamente sulle prestazioni di elaborazione.  
  
-   Se l'elaborazione interessa le prestazioni delle query, ma non è possibile elaborare durante i periodi di carico di query è ridotto, è consigliabile spostare le attività di elaborazione in un server di gestione temporanea e quindi eseguire una sincronizzazione online del server di produzione e il server di gestione temporanea. Per altre informazioni, vedere [Sincronizzare database di Analysis Services](synchronize-analysis-services-databases.md). È inoltre possibile distribuire le attività di elaborazione tra più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite partizioni remote. Per l'elaborazione delle partizioni remote vengono usate risorse di memoria e processore nel server remoto anziché nel computer locale. Per altre informazioni sulla gestione delle partizioni remote, vedere [Creare e gestire una partizione remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md).  
  
-   Se le prestazioni di esecuzione delle query non sono soddisfacenti, ma non è possibile aumentare le risorse di memoria e processore nel server locale, valutare l'opportunità di distribuire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in due o più server di produzione. Sarà quindi possibile usare la funzionalità di bilanciamento del carico di rete per combinare i server in un unico cluster. In un cluster con bilanciamento carico di rete, le query vengono automaticamente distribuite tra tutti i server del cluster.  
  
  
