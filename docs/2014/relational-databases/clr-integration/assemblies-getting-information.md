---
title: Recupero di informazioni sugli assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: ebbb5ac25ea71dc5b9929fb529414b059c0589fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919298"
---
# <a name="getting-information-about-assemblies"></a>Recupero di informazioni sugli assembly
  È possibile recuperare metadati sugli assembly eseguendo query sulle funzioni e sulle viste del catalogo seguenti.  
  
 **Per ottenere informazioni sui singoli assembly**  
  
-   [ASSEMBLYPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/assemblyproperty-transact-sql)  
  
 **Per ottenere informazioni su tutti gli assembly nel database**  
  
-   [sys.assemblies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)  
  
 **Per ottenere informazioni sui file di assembly, tra cui file binari di assembly, file di origine e file di debug**  
  
-   [sys.assembly_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)  
  
 **Per ottenere informazioni sui riferimenti tra assembly**  
  
-   [sys.assembly_references &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)  
  
 **Per ottenere informazioni sull'assembly sui tipi definiti dall'utente**  
  
-   [sys.assembly_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)  
  
-   [sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)  
  
 **Per ottenere informazioni di assembly su common language runtime (CLR) stored procedure, trigger e funzioni**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
 **Per ottenere informazioni sugli oggetti non CLR**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Gli assembly &#40;motore di Database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md)   
 [Implementazione di assembly](assemblies-implementing.md)  
  
  
