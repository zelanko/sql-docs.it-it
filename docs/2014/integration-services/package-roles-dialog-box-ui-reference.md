---
title: Riferimento all'interfaccia utente della finestra di dialogo ruoli pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- Package Roles dialog box
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 94bb72fd6cb9dca8dd76d3925f86ae64a819b7d7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423798"
---
# <a name="package-roles-dialog-box-ui-reference"></a>Riferimento all'interfaccia utente della finestra di dialogo Ruoli pacchetto
  Usare la finestra di dialogo **Ruoli pacchetto** , disponibile in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], per specificare i ruoli a livello di database che dispongono dell'accesso in lettura al pacchetto e quelli che dispongono dell'accesso in scrittura. I ruoli a livello di database si applicano solo ai pacchetti archiviati nel database  **msdb** di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Per altre informazioni sui ruoli a livello di database di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e le relative autorizzazioni, vedere [Ruoli Integration Services &#40;servizio SSIS&#41;](security/integration-services-roles-ssis-service.md).  
  
 I ruoli elencati nella finestra di dialogo sono quelli attualmente disponibili nel database di sistema **msdb** . Se non viene selezionato alcun ruolo, viene applicato il ruolo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] predefinito. Per impostazione predefinita, il ruolo lettura include **db_ssisadmin**, **db_ssisoperator**e l'utente che ha creato il pacchetto. Gli utenti membri di uno di questi ruoli o creatori dei pacchetti possono enumerare, visualizzare, esportare ed eseguire i pacchetti. Per impostazione predefinita, il ruolo scrittura include **db_ssisadmin** e l'utente che ha creato il pacchetto. L'utente membro di questo ruolo e il creatore dei pacchetti possono importare, eliminare e modificare i pacchetti.  
  
 La colonna **ownersid** nella tabella **sysssispackages** include l'ID di sicurezza (SID) univoco dell'utente che ha creato il pacchetto.  
  
## <a name="options"></a>Opzioni  
 **Nome pacchetto**  
 Consente di specificare il nome del pacchetto.  
  
 **Ruolo lettura**  
 Consente di selezionare un ruolo nell'elenco.  
  
 **Ruolo scrittura**  
 Consente di selezionare un ruolo nell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli a livello di database](../relational-databases/security/authentication-access/database-level-roles.md)   
 [Panoramica sulla sicurezza &#40;Integration Services&#41;](security/security-overview-integration-services.md)  
  
  
