---
title: Opzioni degli articoli per la replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 42076200732500a58bce7010dd23e6f90c737317
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904594"
---
# <a name="article-options-for-transactional-replication"></a>Opzioni degli articoli per la replica transazionale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sono disponibili svariate opzioni per gli articoli delle repliche transazionali. La replica transazionale consente infatti di eseguire le operazioni seguenti:  
  
-   Specificare le modalità di propagazione delle modifiche dal server di pubblicazione ai Sottoscrittori. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
-   Specificare che l'esecuzione di una stored procedure deve essere replicata. Ciò risulta utile per la replica dei risultati di stored procedure orientate alla manutenzione che influiscono su ingenti quantità di dati. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Specificare le opzioni di schema, ad esempio se i vincoli e i trigger vengono copiati nel Sottoscrittore. Per altre informazioni, vedere [Specificare le opzioni dello schema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Utilizzare i filtri di righe e di colonne. L'applicazione di filtri agli articoli di una tabella consente di creare partizioni di dati da pubblicare. Per altre informazioni, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
