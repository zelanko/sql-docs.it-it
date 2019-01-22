---
title: DENY - Credenziali con ambito database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- DENY DATABASE SCOPED CREDENTIAL
- DENY_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, database scoped credentials
- denying permissions [SQL Server], database scoped credential
ms.assetid: c508b1c9-169e-4e7a-9a49-7ddf2ca8f848
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2f58fa15ba67cfcf84a35f130fa70eff0d981c0e
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54327362"
---
# <a name="deny-database-scoped-credential-transact-sql"></a>DENY - Credenziali con ambito database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Nega le autorizzazioni per credenziali con ambito database.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DENY permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *permission*  
 Specifica un'autorizzazione che può essere negata per credenziali con ambito database. Vedere l'elenco riportato di seguito.  
  
 ON DATABASE SCOPED CREDENTIAL **::**_credential_name_  
 Specifica il tipo di credenziali con ambito database per cui viene negata l'autorizzazione. Il qualificatore di ambito "::" è obbligatorio.  
  
 *database_principal*  
 Specifica l'entità a cui viene negata l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
 CASCADE  
 Indica che l'autorizzazione negata viene negata anche ad altre entità alle quali è stata concessa da questa entità.  
  
 *denying_principal*  
 Specifica un'entità dalla quale l'entità che esegue la query ottiene il diritto di negare l'autorizzazione. I tipi validi sono:  
  
-   utente del database  
  
-   ruolo del database  
  
-   ruolo applicazione  
  
-   utente del database sul quale viene eseguito il mapping a un account di accesso di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un gruppo di Windows  
  
-   utente del database sul quale viene eseguito il mapping a un certificato  
  
-   utente del database mappato a una chiave asimmetrica  
  
-   utente del database non mappato ad alcuna entità server.  
  
## <a name="remarks"></a>Remarks  
 Le credenziali con ambito database sono un'entità a protezione diretta a livello di database contenuta nel database padre nella gerarchia delle autorizzazioni. Di seguito sono elencate le autorizzazioni più specifiche e limitate che è possibile negare per credenziali con ambito database, insieme alle autorizzazioni più generali che le includono in modo implicito.  
  
|Autorizzazione delle credenziali con ambito database|Implicita nell'autorizzazione delle credenziali con ambito database|Autorizzazione del database in cui è inclusa|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per le credenziali con ambito database. Se viene usata la clausola AS, l'entità specificata deve essere proprietaria delle credenziali con ambito database.  
  
## <a name="see-also"></a>Vedere anche  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT - Credenziali con ambito database (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [REVOKE - Credenziali con ambito database (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
