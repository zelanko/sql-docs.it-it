---
title: Aggiungere un database crittografato a un gruppo di disponibilità
description: Informazioni sulla procedura per l'aggiunta di un database crittografato (o recentemente decrittografato) a un gruppo di disponibilità Always On.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: cawrites
ms.author: chadam
ms.openlocfilehash: 2569f44e4642df714c8108b6540b81d013d30b82
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584301"
---
# <a name="add-an-encrypted-database-to-an-always-on-availability-group"></a>Aggiungere un database crittografato a un gruppo di disponibilità Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  In questo argomento sono contenute informazioni su come utilizzare correttamente database crittografati o recentemente decrittografati con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se un database viene crittografato o contiene una chiave di crittografia del database (DEK), non è possibile usare [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] o [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] per aggiungere il database a un gruppo di disponibilità. Anche se è stato decrittografato un database crittografato, i backup del log potrebbero contenere dati crittografati. In questo caso, la sincronizzazione dei dati iniziale completa potrebbe non riuscire sul database. Questo avviene perché l'operazione di ripristino del log potrebbe richiedere il certificato usato dalle chiavi di crittografia del database e tale certificato potrebbe non essere disponibile.  
  
     Affinché un database decrittografato sia idoneo a essere aggiunto a un gruppo di disponibilità usando la procedura guidata:  
  
    1.  Creare un backup del log del database primario.  
  
    2.  Creare un backup del log completo del database primario.  
  
    3.  Ripristinare il backup del database nell'istanza del server in cui è ospitata la replica secondaria.  
  
    4.  Creare un nuovo backup del log dal database primario.  
  
    5.  Ripristinare questo backup del log sul database secondario.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Usare la Creazione guidata Gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usare la procedura guidata Aggiungi database a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Transparent Data Encryption &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
