---
title: Gestione dei pacchetti in esecuzione a livello di programmazione| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2ffaeac67c91c520ba657b96afc97898328a8299
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422638"
---
# <a name="managing-running-packages-programmatically"></a>Gestione dei pacchetti in esecuzione a livello di programmazione
  Quando si utilizzano i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a livello di programmazione, può essere necessario determinare quali sono attualmente in esecuzione. La classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> dello spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> fornisce metodi e classi per soddisfare questi requisiti.  
  
 Per altre informazioni sul monitoraggio dei pacchetti, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](../service/package-management-ssis-service.md).  
  
 Tutti i metodi descritti in questo argomento richiedono un riferimento all'assembly `Microsoft.SqlServer.ManagedDTS`. Dopo aver aggiunto il riferimento in un nuovo progetto, importare lo spazio dei nomi <xref:Microsoft.SqlServer.Dts.Runtime> con un'istruzione `using` o `Imports`.  
  
> [!IMPORTANT]  
>  I metodi della classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> per l'utilizzo dell'archivio pacchetti SSIS supportano solo ".", localhost o il nome del server locale. Non è possibile utilizzare "(local)".  
  
## <a name="determining-which-packages-are-currently-running"></a>Identificazione dei pacchetti in esecuzione  
 Per determinare quali pacchetti sono attualmente in esecuzione in un server specificato, chiamare il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Il metodo restituisce una raccolta <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> di oggetti <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Gli amministratori vedono tutti i pacchetti attualmente in esecuzione nel computer, mentre gli altri utenti vedono solo quelli che hanno avviato.  
  
## <a name="working-with-running-packages"></a>Utilizzo dei pacchetti in esecuzione  
 Dopo aver determinato quali pacchetti sono attualmente in esecuzione, è possibile recuperare le relative informazioni e richiedere l'arresto di un pacchetto.  
  
### <a name="getting-information-about-a-running-package"></a>Recupero di informazioni su un pacchetto in esecuzione  
 Mentre si scorre la raccolta <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages>, è possibile utilizzare le proprietà dell'oggetto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> per individuare un pacchetto o per ottenere ulteriori informazioni sui pacchetti in esecuzione:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Arresto di un pacchetto in esecuzione  
 È possibile chiamare il metodo <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> di un oggetto <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> per richiedere l'arresto del pacchetto. È possibile che si verifichi un ritardo tra il momento in cui viene emessa una richiesta di arresto e il momento dell'arresto effettivo del pacchetto.  
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione pacchetti &#40;servizio SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerazione dei pacchetti disponibili a livello di codice](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
