---
title: Interoperabilità e coesistenza (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5552780cdc4a2f4e3faf39b9111882fcf4ffdd63
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380119"
---
# <a name="interoperability-and-coexistence-integration-services"></a>Interoperabilità e coesistenza (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) può coesistere in modalità affiancata con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services.  
  
## <a name="features-and-differences"></a>Funzionalità e differenze  
 Nella tabella seguente sono riportate alcune delle differenze esistenti tra la versione corrente e le versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Funzionalità|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|Ambiente di sviluppo|[SQL Server 2014 Data Tools - Business Intelligence per Visual Studio 2012 CTP 2](https://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools - Business Intelligence per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools per Visual Studio 2010](https://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools - Business Intelligence per Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|Ambiente di gestione|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|Tabella di sistema principale in msdb per l'archivio di pacchetti|sysssispackages|sysssispackages|sysssispackages|  
|Utilità del prompt dei comandi principale per i pacchetti in esecuzione|**dtexec** (dtexec.exe), versione 2014|**dtexec** (dtexec.exe), versione 2012|**dtexec** (dtexec.exe), versione 2008|  
|Cartella radice del file system predefinita|C:\Programmi\Microsoft SQL Server\120\DTS|C:\Programmi\Microsoft SQL Server\110\DTS|C:\Programmi\Microsoft SQL Server\100\DTS|  
|Chiave del Registro di sistema radice predefinita|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>Problemi di compatibilità di installazioni side-by-side  
 Quando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services è installato in modalità affiancata con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services, è possibile eseguire le attività seguenti:  
  
-   **Progettare pacchetti in SQL Server Data Tools**. È possibile usare gli strumenti seguenti per sviluppare e gestire i pacchetti in base alle versioni corrispondenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Utilizzare la versione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] di Business Intelligence Development Studio per sviluppare e gestire pacchetti basati su [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)].  
  
    -   Utilizzare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per sviluppare e gestire pacchetti basati su [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
    -   Utilizzare la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per sviluppare e gestire pacchetti basati su [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   **Caricare ed eseguire pacchetti**. È possibile caricare ed eseguire pacchetti sviluppati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], nella versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando si aggiunge il pacchetto a un progetto esistente, il pacchetto viene aggiornato in modo permanente al formato usato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services. Quando si apre il file del pacchetto in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], il pacchetto viene aggiornato temporaneamente al formato usato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services. Se si salva la modifica al pacchetto, quest'ultimo viene aggiornato in modo permanente. Dopo il salvataggio nel formato usato da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services, non è più possibile aprire i pacchetti nelle versioni [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] corrispondenti di Business Intelligence Development Studio e non è possibile eseguirli usando gli strumenti di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services corrispondenti.  
  
-   **Gestire i pacchetti in SQL Server Management Studio**. Non è possibile connettersi a un'istanza della versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dalla versione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Non è possibile connettersi a un'istanza della versione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dalla versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. È possibile utilizzare la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per gestire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archiviati in un'istanza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. È necessario modificare il file di configurazione del servizio per aggiungere l'istanza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] all'elenco dei percorsi gestiti dal servizio. Per altre informazioni, vedere [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Archiviare i pacchetti in SQL Server**. È possibile archiviare i pacchetti nei database seguenti.  
  
    |Formato pacchetto|Database|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services|database msdb di un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services|database msdb di un'istanza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services|database msdb di un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     In un'istanza della versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è possibile importare pacchetti da un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o da un'istanza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ma non è possibile esportare pacchetti in un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o in un'istanza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     In un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]non è possibile importare pacchetti da né esportare pacchetti in un'istanza della versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   **Eseguire i pacchetti**. È possibile eseguire i pacchetti di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services usando la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del servizio **dtexec** o di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Ogni volta che tramite uno strumento di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services si carica un pacchetto sviluppato in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], lo strumento converte temporaneamente, in memoria, il pacchetto nel formato pacchetto usato da [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] . Se il pacchetto di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] presenta problemi che impediscono la conversione, lo strumento di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services non è in grado di eseguire il pacchetto fino a quando tali problemi non vengono risolti. Per altre informazioni, vedere [Upgrade Integration Services Packages](upgrade-integration-services-packages.md).  
  
  
