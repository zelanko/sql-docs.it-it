---
title: sp_server_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_info
- sp_server_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_info
ms.assetid: 2dc2c262-3cfa-4a84-8127-3632ba583543
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 034c4ab2c8ce57ac072e9711fb4e6d621584f273
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529303"
---
# <a name="spserverinfo-transact-sql"></a>sp_server_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco dei nomi degli attributi e dei valori corrispondenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il gateway di database o l'origine dati sottostante.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_server_info [[@attribute_id = ] 'attribute_id']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @attribute_id = ] 'attribute_id'` È l'ID intero dell'attributo. *attribute_id* viene **int**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**ATTRIBUTE_ID**|**int**|ID dell'attributo.|  
|**ATTRIBUTE_NAME**|**varchar(** 60 **)**|Nome dell'attributo.|  
|**ATTRIBUTE_VALUE**|**varchar(** 255 **)**|Impostazione corrente dell'attributo.|  
  
 Nella tabella seguente sono elencati gli attributi. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Le librerie client ODBC vengono utilizzano gli attributi **1**, **2**, **18**, **22**, e **500** alla connessione ora.  
  
|ATTRIBUTE_ID|Descrizione ATTRIBUTE_NAME|ATTRIBUTE_VALUE|  
|-------------------|---------------------------------|----------------------|  
|**1**|DBMS_NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**2**|DBMS_VER|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - *x.xx.xxxx*|  
|**10**|OWNER_TERM|owner|  
|**11**|TABLE_TERM|table|  
|**12**|MAX_OWNER_NAME_LENGTH|128|  
|**13**|TABLE_LENGTH<br /><br /> Specifica il numero massimo di caratteri per un nome di tabella.|128|  
|**14**|MAX_QUAL_LENGTH<br /><br /> Specifica la lunghezza massima del nome di un qualificatore di tabella (la prima parte dei nomi di tabella composti da tre parti).|128|  
|**15**|COLUMN_LENGTH<br /><br /> Specifica il numero massimo di caratteri per un nome di colonna.|128|  
|**16**|IDENTIFIER_CASE<br /><br /> Specifica i nomi definiti dall'utente (nomi di tabella, colonna e stored procedure) nel database (la combinazione di maiuscole e minuscole negli oggetti dei cataloghi di sistema).|SENSITIVE|  
|**17**|TX_ISOLATION<br /><br /> Specifica il livello iniziale di isolamento delle transazioni adottato dal server. Tale livello corrisponde a un livello di isolamento definito in SQL-92.|2|  
|**18**|COLLATION_SEQ<br /><br /> Specifica l'ordinamento del set di caratteri per il server corrente.|charset=iso_1 sort_order=dictionary_iso charset_num=1 sort_order_num=51|  
|**19**|SAVEPOINT_SUPPORT<br /><br /> Specifica se il sistema DBMS sottostante supporta o meno i punti di salvataggio denominati.|Y|  
|**20**|MULTI_RESULT_SETS<br /><br /> Specifica se il database sottostante o il gateway stesso supporta o meno più set di risultati (è possibile inviare più istruzioni attraverso il gateway con più set di risultati restituiti al client).|Y|  
|**22**|ACCESSIBLE_TABLES<br /><br /> Specifica se nella **sp_tables**, il gateway restituisce solo le tabelle, viste e così via, accessibile all'utente corrente (ovvero, l'utente che dispone almeno delle autorizzazioni SELECT per la tabella).|Y|  
|**100**|USERID_LENGTH<br /><br /> Specifica il numero massimo di caratteri per un nome utente.|128|  
|**101**|QUALIFIER_TERM<br /><br /> Specifica il termine del sistema DBMS per il qualificatore di tabella (la prima parte di un nome composto da tre parti).|Database|  
|**102**|NAMED_TRANSACTIONS<br /><br /> Specifica se il sistema DBMS sottostante supporta o meno transazioni denominate.|Y|  
|**103**|SPROC_AS_LANGUAGE<br /><br /> Specifica se è possibile eseguire le stored procedure come eventi del linguaggio.|Y|  
|**104**|ACCESSIBLE_SPROC<br /><br /> Specifica se nella **sp_stored_procedures**, il gateway restituisce solo le stored procedure eseguibili dall'utente corrente.|Y|  
|**105**|MAX_INDEX_COLS<br /><br /> Specifica il numero massimo di colonne di un indice del sistema DBMS.|16|  
|**106**|RENAME_TABLE<br /><br /> Specifica se è possibile rinominare le tabelle.|Y|  
|**107**|RENAME_COLUMN<br /><br /> Specifica se è possibile rinominare le colonne.|Y|  
|**108**|DROP_COLUMN<br /><br /> Specifica se è possibile eliminare le colonne.|Y|  
|**109**|INCREASE_COLUMN_LENGTH<br /><br /> Specifica se è possibile incrementare le dimensioni di colonna.|Y|  
|**110**|DDL_IN_TRANSACTION<br /><br /> Specifica se visualizzare istruzioni DDL nelle transazioni.|Y|  
|**111**|DESCENDING_INDEXES<br /><br /> Specifica se gli indici decrescenti sono supportati.|Y|  
|**112**|SP_RENAME<br /><br /> Specifica se è possibile rinominare una stored procedure.|Y|  
|**113**|REMOTE_SPROC<br /><br /> Specifica se è possibile eseguire stored procedure tramite le funzioni di stored procedure remote di DB-Library.|Y|  
|**500**|SYS_SPROC_VERSION<br /><br /> Specifica la versione delle stored procedure di catalogo implementate.|Numero di versione corrente|  
  
## <a name="remarks"></a>Note  
 **sp_server_info** restituisce un subset delle informazioni fornite da **SQLGetInfo** in ODBC.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
