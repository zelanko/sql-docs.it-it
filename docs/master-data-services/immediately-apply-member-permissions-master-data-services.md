---
title: Applicare immediatamente autorizzazioni membri
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e297124130d8b0a6231db1be4e21ffac98b35051
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812992"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>Applicare immediatamente autorizzazioni membri (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], anziché attendere che venga applicata la sicurezza membri a intervalli regolari, è possibile applicare immediatamente autorizzazioni per membri.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per eseguire la stored procedure mdm.udpSecurityMemberProcessRebuildModel nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per altre informazioni, vedere [Sicurezza di oggetti di database &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
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
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Autorizzazioni membri gerarchie &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
