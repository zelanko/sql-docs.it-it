---
title: Opzioni degli articoli per la replica di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 692ff343154ae53d53cce4bf385e7e1e6350bb03
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897177"
---
# <a name="article-options-for-merge-replication"></a>Opzioni degli articoli per la replica di tipo merge
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Sono disponibili diverse opzioni per gli articoli di tabella di merge che consentono di adattare il comportamento della replica alle esigenze delle applicazioni. La replica di tipo merge consente di eseguire le operazioni seguenti:  
  
-   Utilizzare filtri di riga, join e di colonna. L'applicazione di filtri agli articoli di una tabella consente di creare partizioni di dati da pubblicare. Per altre informazioni, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Specificare se le modifiche del Sottoscrittore vengono caricate nel server di Pubblicazione. Per le applicazioni in cui è necessario che alcuni o tutti i dati siano di sola lettura nel Sottoscrittore, gli articoli di solo download sono vantaggiosi in termini di prestazioni. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Specificare che le eliminazioni di uno o più articoli non devono essere rilevate dai trigger di replica e dalle tabelle di sistema. Questa opzione può essere utile in molti scenari applicativi, inclusi quelli in cui vengono utilizzate eliminazioni batch che non richiedono una replica. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con il rilevamento condizionale delle eliminazioni](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Specificare l'ordine di elaborazione degli articoli per garantire che corrisponda a quello richiesto dall'applicazione. Per altre informazioni, vedere [Specify merge replication options](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Specificare le opzioni per la replica di tipo merge).  
  
-   Specificare che i set di record correlati devono essere elaborati come unità. Per impostazione predefinita, la replica di tipo merge elabora le modifiche nelle tabelle procedendo riga per riga. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
-   Utilizzare il rilevamento e la risoluzione dei conflitti per i casi in cui è possibile che gli stessi dati vengano modificati in più nodi di una topologia. Per altre informazioni, vedere [Rilevare e risolvere i conflitti tra repliche di tipo merge](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
-   Specificare le opzioni di schema, ad esempio se i vincoli e i trigger vengono copiati nel Sottoscrittore. Per altre informazioni, vedere [Specificare le opzioni dello schema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Utilizzare un gestore della logica di business in grado di rispondere a molte condizioni durante la sincronizzazione, ad esempio modifiche dei dati, conflitti ed errori. Per altre informazioni, vedere [Eseguire logiche di business durante la sincronizzazione di tipo merge](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
