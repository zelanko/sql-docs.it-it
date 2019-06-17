---
title: sysssispackagefolders (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2604fa585bc7b27fc385336e1af71079efb68404
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489781"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni cartella logica nella gerarchia di cartelle che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Usa. Queste cartelle vengono visualizzate in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dopo la connessione a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. In una cartella sono visualizzati i pacchetti archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel file system.  
  
 Il **parentfolderid** colonna descrive la gerarchia di cartelle. La cartella nella parte superiore della gerarchia di cartelle contiene un valore null in **parentfolderid**.  
  
 Il **nomecartella** colonna contiene il nome delle cartelle visualizzate in Esplora oggetti.  
  
 Questa tabella è archiviata nel **msdb** database.  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|GUID della cartella.|  
|**parentfolderid**|**uniqueidentifier**|GUID della cartella padre.|  
|**foldername**|**sysname**|Nome della cartella. Questo nome viene visualizzato nella gerarchia di cartelle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
