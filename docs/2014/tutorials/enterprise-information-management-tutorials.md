---
title: Esercitazioni sulla gestione di informazioni aziendali | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 8745dc80-193d-4de0-9f17-ba648ab1e81c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9e40202ef0230fbbdddd1c596e5dc41b4d44a0fe
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373993"
---
# <a name="enterprise-information-management-tutorials"></a>Esercitazioni sulla gestione di informazioni aziendali
  In questa sezione sono contenute esercitazioni per gestire le informazioni in un'organizzazione utilizzando le tecnologie di gestione di informazioni aziendali (EIM, Enterprise Information Management) disponibili in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. La tecnologia EIM offre soluzioni che consentono alle organizzazioni di considerare attendibili la credibilità e la coerenza dei dati in modo che possano prendere decisioni aziendali critiche. In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] sono disponibili le seguenti tecnologie che consentono l'implementazione di soluzioni EIM nell'organizzazione.  
  
-   SQL Server Integration Services (SSIS). SSIS offre una piattaforma potente e flessibile per l'integrazione di dati da diverse origini in una soluzione di estrazione, trasformazione e caricamento (ETL, Extract, Transform and Loading) completa che supporta flussi di lavoro aziendali, un data warehouse o la gestione dei dati master.  
  
-   SQL Server Data Quality Services (DQS). DQS consente la pulizia, la corrispondenza, la standardizzare e l'arricchimento dei dati, pertanto è possibile garantire informazioni attendibili per le funzionalità di Business Intelligence, un data warehouse e carichi di lavoro di elaborazione delle transazioni.  
  
-   SQL Server Master Data Services (MDS). MDS fornisce un hub centrale di dati mediante il quale viene garantita l'integrità costante delle informazioni e la coerenza costante dei dati nelle diverse applicazioni.  
  
 [Enterprise Information Management con SSIS, MDS e DQS insieme &#91;esercitazione&#93;](../../2014/tutorials/enterprise-information-management-using-ssis-mds-and-dqs-together-[tutorial].md)  
 In questa esercitazione viene illustrato come utilizzare insieme SSIS, MDS e DQS per implementare una soluzione EIM di esempio. Innanzitutto, DQS viene utilizzato per creare una Knowledge Base con le informazioni sui dati fornitore (metadati), per pulire i dati in un file di Excel rispetto alla Knowledge Base e per far corrispondere i dati in modo da identificare e rimuovere i relativi duplicati. Successivamente, viene utilizzato il componente aggiuntivo MDS per Excel per caricare i dati puliti e corrispondenti in MDS. Infine, l'intero processo viene automatizzato mediante una soluzione SSIS.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle informazioni aziendali - Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=270871)  
  
  
