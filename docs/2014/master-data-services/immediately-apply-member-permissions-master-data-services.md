---
title: Applicare immediatamente le autorizzazioni ai membri (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f76cb9aaf111f17928c8a6afbd2888d62bbc4d91
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971401"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>Applicare immediatamente autorizzazioni membri (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], anziché attendere che venga applicata la sicurezza membri a intervalli regolari, è possibile applicare immediatamente autorizzazioni per membri.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per eseguire la stored procedure mdm.udpSecurityMemberProcessRebuildModel nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per altre informazioni, vedere [Sicurezza di oggetti di database &#40;Master Data Services&#41;](database-object-security-master-data-services.md).  
  
### <a name="to-immediately-apply-hierarchy-member-permissions"></a>Per applicare immediatamente autorizzazioni per membri della gerarchia  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e connettersi all'istanza [!INCLUDE[ssDE](../includes/ssde-md.md)] per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Creare una nuova query.  
  
3.  Digitare il testo seguente, sostituendo *database* con il nome del database e *Model_Name* con il nome del modello.  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  Consente di eseguire la query.  
  
## <a name="see-also"></a>Vedere anche  
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Autorizzazioni membri gerarchie &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
