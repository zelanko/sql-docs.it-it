---
title: Funzionalità di Integration Services supportate dalle edizioni di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 08a38e8a907c32a2614b3bda07a3153141b127d5
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893819"
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Funzionalità di Integration Services supportate dalle edizioni di SQL Server

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Questo argomento illustra i dettagli delle funzionalità di SQL Server Integration Services (SSIS) supportate dalle diverse edizioni di [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].  

Per le funzionalità supportate dalle edizioni Developer ed Evaluation, vedere le funzionalità elencate per SQL Server Enterprise Edition nelle tabelle seguenti.
  
Per le note sulla versione più recenti e informazioni sulle novità, vedere gli articoli seguenti:
-   [Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Novità di Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Novità di Integration Services in SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**Per provare SQL Server 2016**    

SQL Server Evaluation Edition è disponibile per un periodo di valutazione di 180 giorni.  
    
> [![Download da Evaluation Center](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Scaricare SQL Server 2016 da Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a> Nuove funzionalità di Integration Services in SQL Server 2017
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Scale Out Master|Sì|||||
|Scale Out Worker|Sì|Sì <sup>1</sup>|TBD|TBD|TBD|
|Supporto per Microsoft Dynamics AX e Microsoft Dynamics CRM nei componenti OData <sup>2</sup>|Sì|Sì||||

<sup>1</sup> Se si eseguono i pacchetti che richiedono funzionalità solo Enterprise in Scale Out, anche gli Scale Out Worker devono essere eseguiti in istanze di SQL Server Enterprise.

<sup>2</sup> Questa funzionalità è supportata anche in SQL Server 2016 con Service Pack 1.

## <a name="IEWiz"></a> Importazione/Esportazione guidata SQL Server

|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Importazione/Esportazione guidata SQL Server|Sì|Sì|Sì|Sì|Sì|  

## <a name="IS"></a> Integration Services  
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Connettori origine dati incorporati|Sì|Sì|||| 
|Attività e trasformazioni predefinite|Sì|Sì||||  
|Origine e destinazione ODBC |Sì|Sì|||| 
|Attività e connettori di origine dati di Azure|Sì|Sì||||  
|Connettori e attività Hadoop/HDFS|Sì|Sì||||  
|Strumenti di profiling dei dati di base|Sì|Sì|||| 

## <a name="ISAA"></a> Integration Services - Origini e destinazioni avanzate  
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Origine e destinazione Oracle a prestazioni elevate di Attunity|Sì|||||  
|Origine e destinazione Teradata a prestazioni elevate di Attunity|Sì|||||  
|Origine e destinazione SAP BW|Sì|||||  
|Destinazione Training modello di data mining|Sì|||||  
|Destinazione elaborazione dimensione|Sì|||||  
|Destinazione elaborazione partizione|Sì|||||  
  
## <a name="ISAT"></a> Integration Services - Attività e trasformazioni avanzate  
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Componenti Change Data Capture di Attunity <sup>1</sup>|Sì|||||  
|Trasformazione di query di data mining|Sì|||||  
|Trasformazioni Raggruppamento fuzzy e Ricerca fuzzy|Sì|||||  
|Trasformazioni Estrazione termini e Ricerca termini|Sì|||||  

<sup>1</sup> I componenti Change Data Capture di Attunity richiedono Enterprise Edition. Change Data Capture Service e Change Data Capture Designer, tuttavia, non richiedono Enterprise Edition. È possibile usarli in un computer in cui SSIS non è installato.
