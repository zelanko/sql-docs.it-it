---
title: Spostare file del database | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0b34df711bbe1a80f62bd307ac26e0eee4fa2cbb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726385"
---
# <a name="move-database-files"></a>Spostare file del database
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è possibile spostare i file di database di sistema e definiti dall'utente specificando la nuova posizione dei file nella clausola FILENAME dell'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) . In questo modo è possibile spostare file di dati, di log e del catalogo full-text. Questo può risultare utile nelle situazioni seguenti:  
  
-   Recupero da errore. Ad esempio, il database è in modalità sospetta oppure viene chiuso, a causa di un errore hardware.  
  
-   Rilocazione pianificata.  
  
-   Rilocazione per una manutenzione pianificata del disco.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Spostare database utente](../../relational-databases/databases/move-user-databases.md)|Descrive le procedure necessarie per spostare i file di database definiti dall'utente e i file dei cataloghi in una nuova posizione.|  
|[Spostare i database di sistema](../../relational-databases/databases/move-system-databases.md)|Descrive le procedure necessarie per spostare i file di database di sistema in una nuova posizione.|  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
