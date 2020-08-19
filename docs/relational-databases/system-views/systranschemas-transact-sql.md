---
description: systranschemas (Transact-SQL)
title: systranschemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f034b802eca4a3349b69067d10280b886ffb22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446518"
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **systranschemas** viene utilizzata per tenere traccia delle modifiche dello schema negli articoli pubblicati nelle pubblicazioni transazionali e snapshot. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|Identificatore dell'articolo di tabella nel quale è stata apportata la modifica dello schema.|  
|**StartLsn**|**binary**|Valore LSN all'inizio della modifica dello schema.|  
|**endlsn**|**binary**|Valore LSN alla fine della modifica dello schema.|  
|**TypeId**|**int**|Tipo di modifica dello schema.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
