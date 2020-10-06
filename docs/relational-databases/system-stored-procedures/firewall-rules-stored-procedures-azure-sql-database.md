---
description: Stored procedure per le regole del firewall (database SQL di Azure)
title: Stored procedure delle regole firewall
titleSuffix: Azure SQL Database
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- firewall rules stored procedures
- firewall_rules, setting
- firewall_rules, Azure SQL Database
- firewall systems, Azure SQL Database
ms.assetid: 3d4c2585-00de-46b5-8eee-0efb71cb3aea
author: VanMSFT
ms.author: vanto
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e6a14687e8210133e2a80c0f678aebe7c9b31194
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753816"
---
# <a name="firewall-rules-stored-procedures-azure-sql-database"></a>Stored procedure per le regole del firewall (database SQL di Azure)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  In questa sezione sono contenute le stored procedure che impostano o eliminano le regole firewall. [!INCLUDE[tsql_md](../../includes/tsql-md.md)] le regole del firewall possono essere utilizzate con [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] . Per altre informazioni, vedere [configurare le regole del firewall del database SQL di Azure-Panoramica](/azure/azure-sql/database/firewall-configure).

:::row:::
    :::column:::
        [sp_set_firewall_rule &#40;Database di SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_firewall_rule &#40;database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_set_database_firewall_rule &#40;Database di SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_database_firewall_rule &#40;database SQL di Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::

&nbsp;
  
Per [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , usare le regole di Windows Firewall. Per altre informazioni, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).   
