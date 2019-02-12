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
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7c1a5e117ee1c79b918f9785310b9b7c97671729
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025822"
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
  
  
