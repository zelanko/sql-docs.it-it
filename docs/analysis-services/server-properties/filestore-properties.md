---
title: FILESTORE-proprietà di Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0319006e3ca6d69416746d802c20164da309b188
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071978"
---
# <a name="filestore-properties"></a>FileStore - proprietà
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta il `filestore` le proprietà del server elencate nelle tabelle seguenti. Si tratta di proprietà avanzate, che vanno modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Si applica a:** Modalità server multidimensionale e tabulare  
  
## <a name="properties"></a>Proprietà  
 **MemoryLimit**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryLimitMin**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PercentScanPerPrice**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PerformanceTrace**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RandomFileAccessMode**  
 Proprietà booleana che indica se l'accesso ai file del database e ai file memorizzati nella cache viene eseguito nella modalità di accesso file causale. Questa proprietà è disattivata per impostazione predefinita. Per impostazione predefinita, il server non imposta il flag di accesso file causale quando si apre i file di dati di partizione per l'accesso in lettura.  
  
 Nei sistemi di fascia alta, in particolare quelli che dispongono di grandi risorse di memoria e più nodi NUMA, l'utilizzo dell'accesso ai file causale può essere vantaggioso. In modalità di accesso casuale, Windows consente di ignorare le operazioni di mapping di pagina che leggono i dati dal disco nella cache del file system, abbassando pertanto la contesa sulla cache.  
  
 Sarà necessario eseguire test di confronto per determinare se le prestazioni di esecuzione delle query vengono migliorate a seguito della modifica di questa proprietà. Per le procedure consigliate su come eseguire test di confronto, inclusi la cancellazione della cache e il modo di evitare errori comuni, vedere la pagina relativa alla [Guida operativa di SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539). Per altre informazioni sui compromessi di utilizzo di questa proprietà, vedere [ http://support.microsoft.com/kb/2549369 ](http://support.microsoft.com/kb/2549369).  
  
 Per visualizzare o modificare questa proprietà in Management Studio, abilitare l'elenco delle proprietà avanzate nella pagina delle proprietà del server. Per cambiare la proprietà, è anche possibile utilizzare il file msmdsrv.ini. Dopo aver impostato questa proprietà, si consiglia di riavviare il server; in caso contrario, l'accesso ai file già aperti continuerà a essere eseguito nella modalità precedente.  
  
 **UnbufferedThreshold**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="memory-model-category"></a>Categoria Memory Model  
 **MemoryModel\Tax**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryModel\Income**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryModel\MaximumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryModel\MinimumBalance**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryModel\InitialBonus**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
