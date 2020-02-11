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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919298"
---
# <a name="getting-information-about-assemblies"></a>Recupero di informazioni sugli assembly
  È possibile recuperare metadati sugli assembly eseguendo query sulle funzioni e sulle viste del catalogo seguenti.  
  
 **Per ottenere informazioni su singoli assembly**  
  
-   [ASSEMBLYPROPERTY &#40;&#41;Transact-SQL](/sql/t-sql/functions/assemblyproperty-transact-sql)  
  
 **Per ottenere informazioni su tutti gli assembly contenuti nel database**  
  
-   [sys. Assemblies &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)  
  
 **Per ottenere informazioni sui file di assembly, inclusi i file binari, di origine e di debug**  
  
-   [sys. assembly_files &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)  
  
 **Per ottenere informazioni sui riferimenti tra assembly**  
  
-   [sys. assembly_references &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)  
  
 **Per ottenere informazioni sui tipi definiti dall'utente utilizzati negli assembly**  
  
-   [sys. assembly_types &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)  
  
-   [sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)  
  
 **Per ottenere informazioni sulle stored procedure, i trigger e le funzioni di Common Language Runtime (CLR) utilizzati negli assembly**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
 **Per ottenere informazioni su oggetti non CLR**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md)   
 [Implementazione di assembly](assemblies-implementing.md)  
  
  
