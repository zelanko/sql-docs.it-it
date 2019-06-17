---
title: Modificare vincoli di arco | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693322"
---
# <a name="modify-edge-constraints"></a>Modificare vincoli di arco
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  È possibile modificare un vincolo di arco in [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile modificare il vincolo di arco di una tabella archi modificando l'ordine delle clausole del vincolo di arco o aggiungendo una nuova clausola.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per modificare un vincolo di arco con:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL
 Per modificare un vincolo di arco usando Transact-SQL, è prima necessario eliminare il vincolo di arco esistente e quindi ricrearlo con la nuova definizione. Per altre informazioni, vedere [Eliminare vincoli di arco](../../relational-databases/tables/delete-edge-constraint.md) e [Creare vincoli di arco](../../relational-databases/tables/create-edge-constraints.md).    
 
