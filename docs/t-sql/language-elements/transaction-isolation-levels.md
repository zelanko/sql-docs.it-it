---
description: Livelli di isolamento delle transazioni
title: Livelli di isolamento delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
ms.openlocfilehash: f9c3d400f67f42f206c9b6924f3d2ea90445d023
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467558"
---
# <a name="transaction-isolation-levels"></a>Livelli di isolamento delle transazioni
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non garantisce che gli hint di blocco verranno rispettati nelle query che accedono ai metadati tramite viste del catalogo, viste di compatibilità, viste degli schemi delle informazioni e funzioni predefinite di creazione di metadati.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rispetta internamente solo il livello di isolamento READ COMMITTED per l'accesso ai metadati. Se una transazione utilizza, ad esempio, un livello di isolamento SERIALIZABLE e nella transazione viene eseguito un tentativo di accedere ai metadati utilizzando le viste del catalogo o le funzioni predefinite di creazione di metadati, le query verranno eseguite fino a quando non vengono completate come READ COMMITTED. Nel livello di isolamento dello snapshot, tuttavia, l'accesso ai metadati potrebbe non riuscire a causa di operazioni DDL simultanee. Questo comportamento si verifica perché ai metadati non viene applicato il controllo delle versioni. Per questo motivo, l'accesso agli elementi indicati di seguito nel livello di isolamento dello snapshot potrebbe non riuscire:  
  
-   Viste del catalogo  
  
-   Viste di compatibilità  
  
-   Viste degli schemi delle informazioni  
  
-   Funzioni predefinite di creazione dei metadati  
  
-   Gruppo di stored procedure **sp_help**  
  
-   Stored procedure del catalogo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Viste e funzioni a gestione dinamica  
  
 Per altre informazioni sui livelli di isolamento, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 Nella tabella seguente è incluso un riepilogo sull'accesso ai metadati in livelli di isolamento diversi.  
  
|Livello di isolamento|Funzionalità supportata|Rispettato|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|No|Rispetto non garantito|  
|READ COMMITTED|Sì|Sì|  
|REPEATABLE READ|No|No|  
|SNAPSHOT ISOLATION|No|No|  
|SERIALIZABLE|No|No|  
  
  
