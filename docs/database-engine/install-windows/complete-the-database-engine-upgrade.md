---
title: Completare l'aggiornamento al motore di database | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 4fe57da44076bd33c585d4ab9986cf373e311f8e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794985"
---
# <a name="complete-the-database-engine-upgrade"></a>Completare l'aggiornamento al motore di database

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dopo aver completato l'aggiornamento a SQL Server, potrebbe essere necessario effettuare una serie di passaggi aggiuntivi. tra cui:  
  
Al termine dell'aggiornamento del [!INCLUDE[ssDE](../../includes/ssde-md.md)], completare le operazioni seguenti:  
  
- **Backup dei database:** creare un backup completo di ogni database.  

- **Abilitare le nuove funzionalità:** in SQL Server 2016 e SQL Server 2017 alcune modifiche vengono abilitate solo dopo aver modificato il livello DATABASE_COMPATIBILITY di un database impostando il livello 130 o superiore.  Per altre informazioni e per il flusso di lavoro consigliato, vedere [Modificare la modalità di compatibilità del database e usare l'archivio query](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Se il database contiene tabelle ottimizzate per la memoria create in SQL Server 2014, vedere [Statistiche per tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).
  
- **Integration Services:**  
  
     Eseguire la migrazione di pacchetti di Integration Services nel formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per altre informazioni, vedere [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
- **Reporting Services:** per l'aggiornamento con nuova installazione, ripristinare le chiavi di crittografia di Reporting Services. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- **Master Data Services:**  aggiornare lo schema del database MDS e creare l'applicazione Web di SQL Server 2017. Per altre informazioni, vedere [Aggiornare Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
- **Data Quality Services:** aggiornare lo schema del database DQS e verificarne l'aggiornamento. Per altre informazioni, vedere [Aggiornare Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
- **Ricerca full-text:** Ripopolare cataloghi full-text per garantire la coerenza semantica nei risultati delle query. Per altre informazioni sugli indici full-text, vedere [Popolamento degli indici full-text](../../relational-databases/search/populate-full-text-indexes.md).  
  
