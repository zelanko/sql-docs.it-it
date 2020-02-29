---
title: Strumenti e applicazioni usati in Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a48b400196a77a9c59219bc28cdff496229ae7e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175560"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Strumenti e applicazioni usati in Analysis Services
  È importante trovare gli strumenti e le applicazioni necessari per la creazione di modelli di Analysis Services e la gestione dei database associati in un'istanza di Analysis Services.

## <a name="analysis-services-model-designers"></a>Strumenti di progettazione dei modelli di Analysis Services
 I modelli tabulari e multidimensionali vengono creati dai modelli di progetto in una soluzione compilata all'interno della shell di Visual Studio. Il modello di progetto fornisce gli strumenti di progettazione per la creazione di modelli, cubi, dimensioni e ruoli che costituiscono una soluzione di Analysis Services.

### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>Download di SQL Server Data Tools per Business Intelligence (SSDT-BI)
 
  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] per Business Intelligence (SSDT-BI), precedentemente noto come Business Intelligence Development Studio (BIDS), viene utilizzato per creare i modelli di Analysis Services, i report di Reporting Services e i pacchetti di Integration Services. È possibile scaricare SSDT-BI dai percorsi seguenti:

-   [Scaricare SSDT-BI per Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [Download di SSDT-BI per Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 Se si dispone di una versione precedente di SSDT-BI o BIDS installata nel computer, la versione più recente viene installata side-by-side alla versione precedente. La versione più recente e quella precedente degli strumenti di progettazione vengono in genere eseguite su una sola workstation in modo da poter modificare progetti e soluzioni legati a versioni specifiche del server.

> [!NOTE]
>  Sono disponibili vari siti di download per le versioni di SSDT di Visual Studio 2012 e Visual Studio 2013. La maggior parte non include i modelli di progetto BI. Tramite i collegamenti sopra indicati è possibile scaricare la versione corretta. Si noterà che è presente la versione corretta di SSDT-BI se viene visualizzata la cartella dei modelli di progetto di business intelligence. Questa cartella contiene i modelli di progetto per Analysis Services, Reporting Services e Integration Services. A seconda della modalità di installazione di SSDT-BI, potrebbe essere visualizzato anche un modello di progetto aggiuntivo per i database di SQL Server.

 ![Nuovi modelli di progetto in SSDT](media/ssdt-biprojects.png "Nuovi modelli di progetto in SSDT")

## <a name="administrative-tools"></a>Strumenti di amministrazione

### <a name="sql-server-management-studio"></a>SQL Server Management Studio
 Management Studio è lo strumento di amministrazione principale per tutte le funzionalità di SQL Server, compreso Analysis Services. SQL Server Management Studio è un componente facoltativo. Se non viene visualizzato con le altre applicazioni di SQL Server nella pagina App in Windows Server 2012, eseguire l'installazione di SQL Server per aggiungerlo all'installazione.

### <a name="sql-server-profiler"></a>SQL Server Profiler
 Sebbene sia ufficialmente deprecato, SQL Server Profiler consente di monitorare facilmente connessioni, esecuzione di query MDX e altre operazioni del server. SQL Server Profiler viene installato per impostazione predefinita. È possibile trovarlo con le applicazioni di SQL Server in App in Windows Server 2012.

### <a name="powershell"></a>PowerShell
 È possibile usare i comandi PowerShell per eseguire molte attività amministrative. Per ulteriori informazioni, vedere [Analysis Services PowerShell](analysis-services-powershell.md) .

### <a name="community-and-third-party-tools"></a>Strumenti della community e di terze parti
 Controllare la [pagina codeplex di Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) per esempi di codice della community. I [Forum](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) possono essere utili per cercare consigli per strumenti di terze parti che supportano Analysis Services.
