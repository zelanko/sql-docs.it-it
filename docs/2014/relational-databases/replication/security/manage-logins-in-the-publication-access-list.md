---
title: Gestire gli account nell'elenco di accesso alla pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4ce984303ea0a9e9a85f20e7d921a720be6ef299
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74479239"
---
# <a name="manage-logins-in-the-publication-access-list"></a>Gestione degli account nell'elenco di accesso alla pubblicazione
  In questo argomento si illustra come gestire gli account di accesso nell'elenco di accesso alla pubblicazione in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. L'accesso a una pubblicazione viene controllato tramite l'elenco di accesso alla pubblicazione. Accessi e gruppi possono essere aggiunti e rimossi dell'elenco di accesso alla pubblicazione.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
-   **Per gestire gli account di accesso nell'elenco di accesso alla pubblicazione, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   Prima di aggiungere l'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] all'elenco di accesso alla pubblicazione, è necessario associarlo a un utente di database nel database di pubblicazione.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
 L'elenco di accesso alla pubblicazione nella pagina **Elenco di accesso alla pubblicazione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** consente di gestire gli account di accesso. Per altre informazioni sull'accesso a questa finestra di dialogo, vedere [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-manage-logins-in-the-pal"></a>Per gestire gli account nell'elenco di accesso alla pubblicazione  
  
1.  Nella pagina **Elenco di accesso alla pubblicazione** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** usare i pulsanti **Aggiungi**, **Rimuovi**  e **Rimuovi tutto** per aggiungere e rimuovere gruppi e account di accesso dall'elenco di accesso alla pubblicazione. Non rimuovere **distributor_admin** dall'elenco di accesso alla pubblicazione. Questo account è usato dalla replica.  
  
    > [!NOTE]  
    >  Se si usano un server di distribuzione remoto, gli account nell'elenco di accesso alla pubblicazione devono essere disponibili sia nel server di pubblicazione che nel server di distribuzione. L'account deve essere un account di dominio o un account locale definito in entrambi i server. Le password associate a entrambi gli account di accesso devono essere identiche.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>Per visualizzare gruppi e account di accesso che appartengono all'elenco di accesso alla pubblicazione  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_help_publication_access](/sql/relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql). Per ** \@pubblicazione**specificare il nome della pubblicazione. Verranno visualizzate informazioni sui gruppi e gli account di accesso presenti nell'elenco di accesso alla pubblicazione.  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>Per aggiungere gruppi e account di accesso all'elenco di accesso alla pubblicazione  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_grant_publication_access](/sql/relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql). Per ** \@pubblicazione**specificare il nome della pubblicazione; per ** \@account di accesso**, specificare il nome dell'account di accesso o del gruppo da aggiungere.  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>Per rimuovere gruppi e account di accesso dall'elenco di accesso alla pubblicazione  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_revoke_publication_access](/sql/relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql). Per ** \@pubblicazione**specificare il nome della pubblicazione; per ** \@account di accesso**, specificare il nome dell'account di accesso o del gruppo da rimuovere.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di sicurezza dell'agente di replica](replication-agent-security-model.md)   
 [Proteggere una topologia di replica](view-and-modify-replication-security-settings.md)   
 [Proteggere il server di pubblicazione](secure-the-publisher.md)  
  
  
