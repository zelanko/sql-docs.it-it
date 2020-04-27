---
title: INFORMATION_SCHEMA. SCHEMI restituisce i nomi di schema in un database, non i database in un'istanza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e3683ee043785ec6adc349ac52301280c7bc2b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094726"
---
# <a name="information_schemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA restituisce i nomi degli schemi di un database, non i database di un'istanza
  Sono state rilevate istruzioni che fanno riferimento alla vista INFORMATION_SCHEMA.SCHEMATA. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la vista restituisce tutti i database inclusi in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mentre in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive restituisce tutti gli schemi di un database.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la vista INFORMATION_SCHEMA.SCHEMATA restituisce tutti i database inclusi in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mentre ora restituisce tutti gli schemi di un database, in modo conforme allo standard SQL.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare l'applicazione in modo che faccia riferimento alla vista del catalogo **sys. databases** per restituire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tutti i database in un'istanza di.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
