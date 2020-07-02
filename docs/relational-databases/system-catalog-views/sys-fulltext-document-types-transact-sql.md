---
title: sys. fulltext_document_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 454b1460b0f1db0da7298e640b7b4cf081bb90b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790542"
---
# <a name="sysfulltext_document_types-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce una riga per ogni tipo di documento disponibile per operazioni di indicizzazione full-text. Ogni riga rappresenta l'interfaccia IFilter registrata nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|Estensione di file del tipo di documento supportato.<br /><br /> Questo valore può essere utilizzato per identificare il filtro che verrà utilizzato durante l'indicizzazione full-text di colonne di tipo **varbinary (max)** o **Image**.|  
|**class_id**|**uniqueidentifier**|GUID della classe IFilter che supporta l'estensione di file.|  
|**path**|**nvarchar(260)**|Percorso della DLL dell'interfaccia IFilter. Il percorso è visibile solo ai membri del ruolo predefinito del server **serveradmin** .|  
|**version**|**sysname**|Versione della DLL dell'interfaccia IFilter.|  
|**Produttore**|**sysname**|Nome del produttore dell'interfaccia IFilter.<br /><br /> Nota: solo i documenti con il produttore [!INCLUDE[msCoName](../../includes/msconame-md.md)] sono supportati in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
