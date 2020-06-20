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
ms.openlocfilehash: ec559ba5ccbb53dd92f3a5e1175a10a59fbaf43c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954041"
---
# <a name="getting-information-about-assemblies"></a>Recupero di informazioni sugli assembly
  È possibile recuperare metadati sugli assembly eseguendo query sulle funzioni e sulle viste del catalogo seguenti.  
  
 **Per ottenere informazioni su singoli assembly**  
  
-   [ASSEMBLYPROPERTY &#40;&#41;Transact-SQL](/sql/t-sql/functions/assemblyproperty-transact-sql)  
  
 **Per ottenere informazioni su tutti gli assembly contenuti nel database**  
  
-   [sys.assemblies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)  
  
 **Per ottenere informazioni sui file di assembly, inclusi i file binari, di origine e di debug**  
  
-   [sys.assembly_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)  
  
 **Per ottenere informazioni sui riferimenti tra assembly**  
  
-   [sys.assembly_references &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)  
  
 **Per ottenere informazioni sui tipi definiti dall'utente utilizzati negli assembly**  
  
-   [sys.assembly_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)  
  
-   [sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)  
  
 **Per ottenere informazioni sulle stored procedure, i trigger e le funzioni di Common Language Runtime (CLR) utilizzati negli assembly**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
 **Per ottenere informazioni su oggetti non CLR**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md)   
 [Implementazione di assembly](assemblies-implementing.md)  
  
  
