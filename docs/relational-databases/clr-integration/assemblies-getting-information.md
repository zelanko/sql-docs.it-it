---
title: Recupero di informazioni sugli assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], metadata
- status information [SQL Server], assemblies
- metadata [SQL Server], assemblies
ms.assetid: 6aa7f18e-baad-4481-9777-8c3b230b392f
author: rothja
ms.author: jroth
ms.openlocfilehash: fcdd4c8c834d8c250716b6c887c3b08248fac67d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028020"
---
# <a name="assemblies---getting-information"></a>Assembly - Recupero di informazioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile recuperare metadati sugli assembly eseguendo query sulle funzioni e sulle viste del catalogo seguenti.  
  
 **Per ottenere informazioni su singoli assembly**  
  
-   [ASSEMBLYPROPERTY &#40;&#41;Transact-SQL](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
 **Per ottenere informazioni su tutti gli assembly contenuti nel database**  
  
-   [sys.assemblies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  
 **Per ottenere informazioni sui file di assembly, inclusi i file binari, di origine e di debug**  
  
-   [sys.assembly_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-files-transact-sql.md)  
  
 **Per ottenere informazioni sui riferimenti tra assembly**  
  
-   [sys.assembly_references &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-references-transact-sql.md)  
  
 **Per ottenere informazioni sui tipi definiti dall'utente utilizzati negli assembly**  
  
-   [sys.assembly_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md)  
  
-   [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
 **Per ottenere informazioni sulle stored procedure, i trigger e le funzioni di Common Language Runtime (CLR) utilizzati negli assembly**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)  
  
 **Per ottenere informazioni su oggetti non CLR**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md)   
 [Implementazione di assembly](../../relational-databases/clr-integration/assemblies-implementing.md)  
  
  
