---
title: Gerarchia delle autorizzazioni (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487151"
---
# <a name="permissions-hierarchy-database-engine"></a>Gerarchia delle autorizzazioni (Motore di database)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] gestisce una raccolta gerarchica di entità che possono essere protette attraverso l'uso di autorizzazioni. Queste entità sono denominate *entità a sicurezza diretta*. Le entità a protezione diretta più significative sono server e database, ma è possibile impostare autorizzazione distinte a un livello più specifico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regola le azioni delle entità sulle entità a protezione diretta verificando che siano state concesse le autorizzazioni corrette.

 Nella figura seguente vengono illustrate le relazioni esistenti tra le gerarchie di autorizzazioni di [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .

 ![Diagramma delle gerarchie di autorizzazioni del motore di database](../../database-engine/media/wj-security-layers.gif "Diagramma delle gerarchie di autorizzazioni del motore di database")

## <a name="chart-of-sql-server-permissions"></a>Grafico delle autorizzazioni di SQL Server
 Per un grafico con dimensioni poster di [!INCLUDE[ssDE](../../../includes/ssde-md.md)] tutte le autorizzazioni in formato PDF [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf), vedere.

## <a name="working-with-permissions"></a>Utilizzo delle autorizzazioni
 Le autorizzazioni possono essere manipolate attraverso le ben note query GRANT, DENY e REVOKE [!INCLUDE[tsql](../../includes/tsql-md.md)] . Le informazioni sulle autorizzazioni sono visualizzate nelle viste di catalogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) e [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) . Le funzioni predefinite offrono inoltre supporto per query sulle informazioni relative alle autorizzazioni.

## <a name="see-also"></a>Vedere anche
 [Protezione](securing-sql-server.md) [delle autorizzazioni SQL Server &#40;motore di database](permissions-database-engine.md) entità a [protezione diretta](securables.md)&#41;[entità &#40;](authentication-access/principals-database-engine.md) motore di database&#41;&#40;Transact-SQL&#41;&#40;Transact [-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) Transact [-SQL &#40;](/sql/t-sql/statements/revoke-transact-sql) [Deny](/sql/t-sql/statements/deny-transact-sql)&#41;Transact- [SQL HAS_PERMS_BY_NAME &#40;](/sql/t-sql/functions/has-perms-by-name-transact-sql)&#41;Transact-SQL [fn_builtin_permissions sys.](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) [&#40;&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) Transact-SQL server_permissions sys. &#40;[&#41;Transact-](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) SQL database_permissions


