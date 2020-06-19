---
title: Applicare le regole relative alla qualità dei dati all'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 442516495ce4a384a7f2d61ffe469a976269dbb3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84913811"
---
# <a name="apply-data-quality-rules-to-data-source"></a>Applicazione delle regole relative alla qualità dei dati all'origine dati
  È possibile utilizzare Data Quality Services (DQS) per correggere i dati nel flusso di dati del pacchetto connettendo la trasformazione DQS Cleansing all'origine dati. Per altre informazioni su DQS, vedere [Concetti di Data Quality Services](../../../data-quality-services/data-quality-services-concepts.md). Per altre informazioni sulla trasformazione, vedere [Trasformazione DQS Cleansing](dqs-cleansing-transformation.md).  
  
 Quando si elaborano i dati con la trasformazione DQS Cleansing, viene creato un progetto Data Quality nel server Data Quality. È possibile utilizzare il client Data Quality per gestire il progetto. Per altre informazioni, vedere [Gestire un progetto Data Quality &#40;apertura, sblocco, ridenominazione ed eliminazione&#41;](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Per correggere i dati nel flusso di dati  
  
1.  Creare un pacchetto.  
  
2.  Aggiungere e configurare la trasformazione DQS Cleansing. Per altre informazioni, vedere [Finestra di dialogo Editor trasformazione DQS Cleansing](../../dqs-cleansing-transformation-editor-dialog-box.md).  
  
3.  Connettere la trasformazione DQS Cleansing a un'origine dati.  
  
  
