---
title: sys.sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d700fd19999da3905a0ff69231a286a022d57e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982919"
---
# <a name="syssprdareauthorizedb-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Consente di ripristinare la connessione autenticata tra un database locale abilitato per Stretch e il database remoto.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argomenti  
 @credential = *@credential*  
 È la credenziale con ambito database associata al database locale abilitato per l'estensione.  
  
 @with_copy = *@with_copy*  
 Specifica se creare una copia dei dati remoti e connettersi alla copia (scelta consigliata). *@with_copy* è di tipo bit.  
  
 @azure_servername = *@azure_servername*  
 Specifica il nome del server Azure che contiene i dati remoti. *@azure_servername* è di tipo sysname.  
  
 @azure_databasename = *@azure_databasename*  
 Specifica il nome del database di Azure che contiene i dati remoti. *@azure_databasename* è di tipo sysname.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o > 0 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 Richiede autorizzazioni db_owner.  
  
## <a name="remarks"></a>Note  
 Quando si esegue [Sys. sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) per ristabilire la connessione al database di Azure remoto, questa operazione automaticamente Reimposta la modalità query LOCAL_AND_REMOTE, ovvero il comportamento predefinito per Stretch Database. Vale a dire, le query restituiscono risultati dai dati locali e remoti.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente ripristina la connessione autenticata tra un database locale abilitato per Stretch e il database remoto. Crea una copia dei dati remoti (scelta consigliati) e si connette alla nuova copia.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
