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
ms.openlocfilehash: c525b1b457c2bc9f505a83cc89a08a57c27e6279
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881281"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni cartella logica nella gerarchia di cartelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzata da. Queste cartelle vengono visualizzate in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dopo la connessione a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. In una cartella sono visualizzati i pacchetti archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel file system.  
  
 La colonna **ParentFolderId** descrive la gerarchia di cartelle. La cartella nella parte superiore della gerarchia di cartelle contiene un valore null in **ParentFolderId**.  
  
 La colonna **FolderName** contiene il nome delle cartelle visualizzate in Esplora oggetti.  
  
 Questa tabella è archiviata nel database **msdb** .  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**FolderId**|**uniqueidentifier**|GUID della cartella.|  
|**ParentFolderId**|**uniqueidentifier**|GUID della cartella padre.|  
|**nomecartella**|**sysname**|Nome della cartella. Questo nome viene visualizzato nella gerarchia di cartelle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
