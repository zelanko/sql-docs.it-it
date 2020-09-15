---
description: Informazioni sulla proprietà dei diagrammi di database (Visual Database Tools)
title: Informazioni sulla proprietà dei diagrammi di database
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d3da1122dcb61b50db189ec798f091496621cbfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88312687"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Informazioni sulla proprietà dei diagrammi di database (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Per poter utilizzare la Progettazione diagrammi di database, è necessario che un membro del ruolo db_owner (un ruolo dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) ne effettui preventivamente la configurazione per il controllo dell'accesso ai diagrammi. Ciascun diagramma ha un solo proprietario, ovvero l'utente che lo ha creato. Per altre informazioni sulla configurazione dei diagrammi, vedere [Impostazione di Progettazione diagrammi di database (../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md).  
  
In relazione alla proprietà dei diagrammi, tenere presente quanto segue:  
  
-   Benché un diagramma possa essere creato da qualsiasi utente che dispone di accesso a un database, potrà essere visualizzato solo dall'utente che lo ha creato e dai membri del ruolo db_owner.  
  
-   La proprietà dei diagrammi può essere trasferita solo ai membri del ruolo db_owner e soltanto se il proprietario precedente è stato rimosso dal database.  
  
-   Se il proprietario di un diagramma viene rimosso dal database, il diagramma rimarrà all'interno del database finché un membro del ruolo db_owner non tenterà di aprirlo. A questo punto, il membro del ruolo db_owner potrà scegliere di subentrare come proprietario del diagramma.  
  
## <a name="see-also"></a>Vedere anche

[Utilizzare diagrammi di database](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Impostare Progettazione diagrammi di database](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)
