---
title: Modifiche di rilievo apportate alle funzionalità del Motore di database in SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: b2fda344839ee7d885a11313d088140738dfb640
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803413"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Modifiche di rilievo apportate alle funzionalità del Motore di database in SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Questo argomento descrive le modifiche di rilievo apportate al [!INCLUDE[ssDE](../includes/ssde-md.md)] di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile che questi problemi si verifichino quando viene effettuato un aggiornamento.  
  
##  <a name="SQL15"></a> Modifiche di rilievo in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   La colonna *sample_ms* di `sys.dm_io_virtual_file_stats` è stata ampliata passando da un tipo di dati **int** a un tipo di dati **bigint**.  
  
-   La colonna *TimeStamp* di `sys.fn_virtualfilestats` è stata ampliata passando da un tipo di dati **int** a un tipo di dati **bigint**.  

-   Nel livello di compatibilità del database 130, le conversioni implicite dai tipi di dati **datetime** a **datetime2** mostrano una maggiore precisione prevedendo i millisecondi frazionari, risultanti in diversi valori convertiti. Usare il cast esplicito per il tipo di dati datetime2 ogni volta che si presenta uno scenario di confronto misto tra tipi di dati datetime e datetime2. Per altre informazioni, vedere questo [articolo del supporto tecnico Microsoft](https://support.microsoft.com/help/4010261).

-   Con il livello di compatibilità database 130, le operazioni che eseguono conversioni implicite tra determinati tipi di dati numerici e di data/ora offrono una maggiore precisione e possono dare come risultato valori convertiti diversi. È incluso l'utilizzo di funzioni che richiedono calcoli, come ad esempio `DATEDIFF` e `ROUND`. Per altre informazioni, vedere questo [articolo del supporto tecnico Microsoft](https://support.microsoft.com/help/4010261).

## <a name="previous-versions"></a> Versioni precedenti  

Per informazioni sulle modifiche di rilievo in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e in alcune versioni precedenti, vedere [Modifiche che possono causare problemi di funzionamento apportate alle funzionalità del Motore di database in SQL Server 2014](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014).

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentazione archiviata per versioni molto vecchie di SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Vedere anche  
 [Funzionalità del motore di database deprecate in SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funzionalità del motore di database non più usate in SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilità con le versioni precedenti del motore di database di SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Miglioramenti di SQL Server 2016 o SQL Server 2017 in Windows relativi alla gestione di alcuni tipi di dati e operazioni non comuni](https://support.microsoft.com/help/4010261)   
