---
description: Tabelle Integration Services (Transact-SQL)
title: Tabelle di Integration Services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 05f7e319dbaec37761eb5488f9d9a33cce09f3a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473249"
---
# <a name="integration-services-tables-transact-sql"></a>Tabelle Integration Services (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Negli argomenti di questa sezione vengono descritte le tabelle di sistema del database msdb in cui sono archiviate le informazioni utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 Contiene una riga per ogni voce di log generata da un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in fase di esecuzione.  
  
 Questa tabella viene utilizzata solo quando i pacchetti utilizzano il provider di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 Contiene una riga per ogni cartella logica utilizzata dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per organizzare i pacchetti. I valori di colonna definiscono le relazioni padre/figlio tra cartelle nidificate.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] visualizza i pacchetti archiviati in una visualizzazione gerarchica quando ci si connette al servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 Include una riga per ogni pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Questa tabella viene utilizzata solo quando si archiviano pacchetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
