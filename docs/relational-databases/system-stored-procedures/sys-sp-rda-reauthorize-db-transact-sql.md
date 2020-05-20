---
title: sys. sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68267f07c125e05f235c1a0bcb4c7f855274bc86
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814748"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ripristina la connessione autenticata tra un database locale abilitato per l'estensione e il database remoto.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argomenti  
 @credential= * \@ Credential*  
 Credenziale con ambito database associata al database locale abilitato per l'estensione.  
  
 @with_copy= * \@ with_copy*  
 Specifica se creare una copia dei dati remoti e connettersi alla copia (scelta consigliata). * \@ with_copy* è di bit.  
  
 @azure_servername= * \@ azure_servername*  
 Specifica il nome del server di Azure che contiene i dati remoti. * \@ azure_servername* è di tipo sysname.  
  
 @azure_databasename= * \@ azure_databasename*  
 Specifica il nome del database di Azure che contiene i dati remoti. * \@ azure_databasename* è di tipo sysname.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o >0 (esito negativo)  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede autorizzazioni db_owner.  
  
## <a name="remarks"></a>Commenti  
 Quando si esegue [sys. sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) per riconnettersi al database di Azure remoto, questa operazione Reimposta automaticamente la modalità di query su LOCAL_AND_REMOTE, che rappresenta il comportamento predefinito per Stretch database. Ovvero le query restituiscono i risultati dai dati locali e remoti.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene ripristinata la connessione autenticata tra un database locale abilitato per l'estensione e il database remoto. Esegue una copia dei dati remoti (scelta consigliata) e si connette alla nuova copia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys. sp_rda_deauthorize_db &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
