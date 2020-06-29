---
title: Trasformazione DQS Cleansing | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6df48dd9d90802b5694dcc6b7f73a65aee46b5e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430688"
---
# <a name="dqs-cleansing-transformation"></a>Trasformazione DQS Cleansing
  La trasformazione DQS Cleansing utilizza Data Quality Services (DQS) per correggere i dati da un'origine dati connessa, applicando le regole approvate create per l'origine dati connessa o un'origine dati simile. Per ulteriori informazioni sulle regole di correzione dei dati, vedere [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Per ulteriori informazioni su DQS, vedere [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Per determinare se è necessario correggere i dati, la trasformazione DQS Cleansing elabora i dati da una colonna di input quando le condizioni seguenti sono vere:  
  
-   La colonna è selezionata per la correzione dei dati.  
  
-   Il tipo di dati della colonna è supportato per la correzione dei dati.  
  
-   È stato eseguito il mapping della colonna a un dominio con un tipo di dati compatibile.  
  
 La trasformazione include inoltre un output degli errori da configurare per gestire gli errori a livello di riga. Per configurare l'output degli errori, utilizzare **Editor trasformazione DQS Cleansing**.  
  
 È possibile includere [Fuzzy Grouping Transformation](fuzzy-grouping-transformation.md) nel flusso di dati per identificare righe di dati che probabilmente sono duplicati.  
  
## <a name="data-quality-projects-and-values"></a>Progetti Data Quality e valori  
 Quando si elaborano i dati con la trasformazione DQS Cleansing, viene creato un progetto di pulizia nel server Data Quality. È possibile utilizzare il client Data Quality per gestire il progetto. Inoltre, è possibile utilizzare il client Data Quality per importare i valori del progetto in un dominio di una Knowledge Base in DQS. È possibile importare i valori solo in un dominio (o dominio collegato) configurato per l'utilizzo dalla trasformazione DQS Cleansing.  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Aprire progetti di Integration Services in Data Quality Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importare i valori di un progetto di pulizia in un dominio](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Applicare le regole relative alla qualità dei dati all'origine dati](apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Gestire &#40;aprire, sbloccare, rinominare ed eliminare&#41; un progetto Data Quality](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   Articolo relativo alla [pulizia dei dati complessi utilizzando domini compositi](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)su social.technet.microsoft.com.  
  
  
