---
title: Concessione dell'accesso a un oggetto di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 19381b0c5dbe690a60b2c536a8da759205c08c31
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62643447"
---
# <a name="granting-access-to-a-database-object"></a>Concessione dell'accesso a un oggetto di database
  In qualità di amministratore, è possibile eseguire l'istruzione SELECT dalla tabella **Products** e la vista **vw_Names** ed eseguire la procedura **pr_Names** ; Tuttavia, Mary non può. Per concedere a tale utente le autorizzazioni necessarie, utilizzare l'istruzione GRANT.  
  
### <a name="procedure-title"></a>Titolo della procedura  
  
1.  Eseguire l'istruzione seguente per concedere a `Mary` l'autorizzazione `EXECUTE` per la stored procedure `pr_Names` .  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
 In questo scenario, all'utente Mary è consentito solo l'accesso alla tabella **Products** usando la stored procedure. Se si desidera autorizzare l'utente Mary a eseguire un'istruzione SELECT sulla vista, è inoltre necessario eseguire `GRANT SELECT ON vw_Names TO Mary`. Per rimuovere l'accesso agli oggetti di database, utilizzare l'istruzione REVOKE.  
  
> [!NOTE]  
>  Se la tabella, la vista e la stored procedure non appartengono allo stesso schema, la procedura per la concessione delle autorizzazioni risulta più complessa.  
  
## <a name="about-grant"></a>Informazioni sull'istruzione GRANT  
 È necessario disporre dell'autorizzazione EXECUTE per eseguire una stored procedure. Per accedere e modificare i dati, è necessario disporre delle autorizzazioni SELECT, INSERT, UPDATE e DELETE. L'istruzione GRANT è inoltre utilizzata per altre autorizzazioni , ad esempio quella per creare tabelle.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Riepilogo: Configurazione delle autorizzazioni per gli oggetti di database](lesson-2-5-summary-configuring-permissions-on-database-objects.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CONCEDERE &#40;&#41;Transact-SQL](/sql/t-sql/statements/grant-transact-sql)   
 [Revoke &#40;&#41;Transact-SQL](/sql/t-sql/statements/revoke-transact-sql)  
  
  
