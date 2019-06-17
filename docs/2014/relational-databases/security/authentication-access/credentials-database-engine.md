---
title: Credenziali (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d42f93735723c81baf837736bfabcda2b1707aae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011835"
---
# <a name="credentials-database-engine"></a>Credenziali (Motore di database)
  Una credenziale è un record contenente le informazioni di autenticazione (credenziali) necessarie per connettersi a una risorsa all'esterno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Queste informazioni vengono utilizzate internamente da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La maggior parte delle credenziali contiene un nome utente e una password di Windows.  
  
 Le informazioni archiviate in una credenziale consentono a un utente che ha eseguito la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di accedere a risorse esterne all'istanza del server. Quando la risorsa esterna è Windows, l'utente viene autenticato come l'utente di Windows specificato nella credenziale. È possibile eseguire il mapping di una singola credenziale a più account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , tuttavia, per un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile eseguire il mapping a una sola credenziale.  
  
 Le credenziali del sistema vengono create automaticamente e associate a endpoint specifici. I nomi delle credenziali di sistema iniziano con due segni di cancelletto (##).  
  
 Per altre informazioni sulle credenziali, vedere la [Sys. Credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) vista del catalogo.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Creare una credenziale](../authentication-access/create-a-credential.md) [crea CREDENZIALE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [Sicurezza di SQL Server](../securing-sql-server.md)  
  
  
