---
title: Pagina Selezione database (creazione guidata gruppo di disponibilità-procedura guidata Aggiungi database) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.adddatabasewizard.selectdatabases.f1
- sql12.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2c6cdeb27dfd1768c9a494497f5b2b1e0b7350a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62788491"
---
# <a name="select-databases-page-new-availability-group-wizard-add-database-wizard"></a>Pagina Selezione database (creazione guidata gruppo di disponibilità-procedura guidata Aggiungi database)
  In questo argomento della Guida vengono descritte le opzioni della pagina **Specifica database** . Questo argomento si applica alla [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] e alla [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="PageOptions"></a> Opzioni di selezione dei database  
 Nella griglia **Database utente in questa istanza di SQL Server** è elencato ogni database utente locale. Le colonne sono le seguenti:  
  
 **Nome**  
 Visualizza il nome di un database utente locale.  
  
 **Dimensione**  
 Visualizza la dimensione del database, se è disponibile per la procedura guidata.  
  
 **Status**  
 Visualizza un collegamento ipertestuale il cui testo indica se un determinato database soddisfa i prerequisiti per l'aggiunta a un gruppo di disponibilità. Se lo stato è "**Soddisfa i prerequisiti**" è possibile aggiungere il database al gruppo di disponibilità. Se un database non soddisfa tutti i prerequisiti, il collegamento ipertestuale **Stato** fornisce una breve spiegazione dei motivi per cui il database non è idoneo. Per ulteriori informazioni, fare clic sul collegamento ipertestuale.  
  
 È possibile lasciare la procedura guidata sulla pagina **Seleziona database** mentre si eseguono le operazioni necessari per soddisfare un prerequisito del database. Quando si torna alla pagina **Seleziona database** fare clic su **Aggiorna** per aggiornare la griglia.  
  
 **Aggiorna**  
 Fare clic per aggiornare la griglia. Questa opzione è utile dopo avere eseguito un'operazione necessaria per soddisfare un prerequisito del database.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usare la procedura guidata Aggiungi database a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
