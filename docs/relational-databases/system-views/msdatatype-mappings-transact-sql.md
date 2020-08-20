---
description: MSdatatype_mappings (Transact-SQL)
title: MSdatatype_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: f67f313d177b5ef22e6cb97b9ab25d5281c860e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463844"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La visualizzazione **MSdatatype_mappings** esegue il mapping dei tipi di dati SQL Server ai tipi di dati utilizzati da sistemi di gestione di database non SQL Server (DBMS). Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|È il nome del sistema DBMS. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> **MSSQLSERVER**: la destinazione è un database SQL Server.<br />**Oracle**: la destinazione è un database Oracle.<br />**DB2**: la destinazione è un database IBM DB2.<br />**Sybase**: la destinazione è un database Sybase.|  
|**sql_type**|**nvarchar(128)**|Tipo di dati di SQL Server.|  
|**dest_type**|**nvarchar(128)**|Nome del tipo di dati non SQL Server.|  
|**dest_prec**|**bigint**|Precisione del tipo di dati non SQL Server.|  
|**dest_create_params**|**int**|Solo per uso interno.|  
|**dest_nullable**|**bit**|Indica se il tipo di dati non SQL Server supporta valori NULL.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Specificare i mapping dei tipi di dati per un server di pubblicazione Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
