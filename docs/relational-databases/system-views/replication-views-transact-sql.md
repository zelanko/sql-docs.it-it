---
title: Viste della replica (Transact-SQL) | Microsoft Docs
description: Le viste di replica contengono informazioni utilizzate dalla replica in SQL Server. Le viste semplificano l'accesso ai dati nelle tabelle di sistema di replica.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: ae0c1245bdf9ff7fe1d1eb712745cbc15d2479af
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807934"
---
# <a name="replication-views-transact-sql"></a>Viste della replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Queste viste contengono informazioni utilizzate dalla replica in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le visualizzazioni consentono un accesso più semplice ai dati nelle [tabelle del sistema di replica](../../relational-databases/system-tables/replication-tables-transact-sql.md). Le viste vengono create in un database utente quando questo viene abilitato come database di pubblicazione o sottoscrizione. Tutti gli oggetti di replica vengono rimossi da un database utente quando questo viene rimosso dalla topologia di replica. Il metodo preferito per accedere ai metadati di replica consiste nell'utilizzare [le stored procedure di replica](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
> [!IMPORTANT]  
>  Gli utenti non devono modificare direttamente le viste di sistema.  
  
## <a name="replication-views"></a>Viste della replica  
 Di seguito è riportato un elenco delle viste di sistema utilizzate dalla replica, raggruppate per database.  
  
### <a name="replication-views-in-the-msdb-database"></a>Viste della replica nel database msdb  
  
|||  
|-|-|  
|[MSdatatype_mappings &#40;&#41;Transact-SQL](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[sysdatatypemappings &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>Viste della replica nel database di distribuzione  
  
|||  
|-|-|  
|[IHextendedArticleView &#40;&#41;Transact-SQL](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40;vista di sistema&#41; &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[Vista IHextendedSubscriptionView &#40;&#41;Transact-SQL](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40;&#41;Transact-SQL](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications &#40;System View&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[MSdistribution_status &#40;&#41;Transact-SQL](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions &#40;System View&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40;vista di sistema&#41; &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>Viste della replica nel database di pubblicazione  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;&#41;Transact-SQL](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>Viste della replica nel database di sottoscrizione  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;&#41;Transact-SQL](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
