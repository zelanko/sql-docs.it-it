---
title: sp_table_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42d2535dedb1161a78362f17a1ad7c79ca49bb87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096118"
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sul conteggio delle righe o sul valore di checksum per una tabella o vista indicizzata oppure confronta le informazioni sul conteggio delle righe o sul valore di checksum specificate con la tabella o vista indicizzata. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione e nel database di sottoscrizione del Sottoscrittore. *Non supportato per il server di pubblicazione Oracle*.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @table = ] 'table'` È il nome della tabella. *Nella tabella* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` Specifica se restituire il numero previsto di righe nella tabella. *expected_rowcount* viene **int**, con un valore predefinito è NULL. con il quale viene restituito il conteggio delle righe effettivo come parametro di output. Se viene specificato un altro valore, questo viene confrontato con il conteggio delle righe effettivo per rilevare eventuali differenze.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` Specifica se restituire il valore di checksum previsto per la tabella. *expected_checksum* viene **numerici**, con un valore predefinito è NULL. con cui viene restituito il valore di checksum effettivo come parametro di output. Se viene specificato un altro valore, questo viene confrontato con il valore di checksum effettivo per rilevare eventuali differenze.  
  
`[ @rowcount_only = ] type_of_check_requested` Specifica il tipo di checksum o conteggio delle righe da eseguire. *type_of_check_requested* viene **smallint**, il valore predefinito è **1**.  
  
 Se **0**, eseguire un conteggio delle righe e una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] checksum compatibile con 7.0.  
  
 Se **1**, eseguire solo un controllo di conteggio delle righe.  
  
 Se **2**, eseguire un conteggio delle righe e checksum binario.  
  
`[ @owner = ] 'owner'` È il nome del proprietario della tabella. *proprietario* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @full_or_fast = ] full_or_fast` Il metodo consente di calcolare il conteggio delle righe. *full_or_fast* viene **tinyint**, il valore predefinito è **2**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Esegue un conteggio completo con COUNT(*).|  
|**1**|Un conteggio rapido in **sysindexes**. Conteggio delle righe **sysindexes** è molto più veloce rispetto al conteggio delle righe nella tabella effettiva. Tuttavia, poiché **sysindexes** in modalità differita è aggiornato, il conteggio delle righe potrebbe non essere accurata.|  
|**2** (impostazione predefinita)|Esegue un conteggio rapido condizionale eseguendo innanzitutto un tentativo con il metodo rapido. Se il metodo rapido evidenzia delle differenze, viene applicato il metodo completo. Se *expected_rowcount* è NULL e la stored procedure viene utilizzata per ottenere il valore, viene utilizzato sempre un Count (\*) completo.|  
  
`[ @shutdown_agent = ] shutdown_agent` Se l'agente di distribuzione è in esecuzione **sp_table_validation**, indica se l'agente di distribuzione viene interrotta immediatamente dopo il completamento della convalida. *shutdown_agent* viene **bit**, il valore predefinito è **0**. Se **0**, l'agente di replica non viene arrestato. Se **1**, viene generato l'errore 20578 e l'agente di replica viene segnalato l'arresto. Questo parametro viene ignorato quando **sp_table_validation** viene eseguito direttamente dall'utente.  
  
`[ @table_name = ] table_name` È il nome della tabella della vista utilizzata per i messaggi di output. *TABLE_NAME* viene **sysname**, il valore predefinito è **@table** .  
  
`[ @column_list = ] 'column_list'` È l'elenco di colonne da utilizzare nella funzione checksum. *column_list* viene **nvarchar (4000)** , con un valore predefinito è NULL. Abilita la convalida degli articoli di tipo merge per specificare un elenco di colonne che non include le colonne calcolate e timestamp.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Se si esegue una convalida mediante checksum e checksum previsto è uguale a quello della tabella **sp_table_validation** restituisce un messaggio che la tabella ha superato la convalida mediante checksum. In caso contrario, restituisce un messaggio per indicare che la tabella potrebbe non essere sincronizzata e specifica la differenza tra il numero di righe previsto e quello effettivo.  
  
 Se si esegue una convalida mediante conteggio delle righe e il numero previsto di righe è uguale al numero della tabella **sp_table_validation** restituisce un messaggio che la tabella ha superato la convalida mediante conteggio delle righe. In caso contrario, restituisce un messaggio per indicare che la tabella potrebbe non essere sincronizzata e specifica la differenza tra il numero di righe previsto e quello effettivo.  
  
## <a name="remarks"></a>Note  
 **sp_table_validation** viene utilizzata in tutti i tipi di replica. **sp_table_validation** non è supportata per server di pubblicazione Oracle.  
  
 Con l'operazione di checksum viene eseguito un controllo di ridondanza ciclico (CRC, Cyclic Redundancy Check) a 32 bit sull'intera immagine delle righe all'interno della pagina. Non esegue un controllo solo su colonne specifiche e non è eseguibile in una vista o in una partizione verticale della tabella. Inoltre, il checksum ignora il contenuto del **testo** e **immagine** colonne (per impostazione predefinita).  
  
 Quando si esegue un'operazione di checksum, è necessario che la struttura della tabella nei due server sia identica, ovvero le tabelle nei due server devono includere le stesse colonne nel medesimo ordine aventi lo stesso tipo di dati, la stessa lunghezza e le stesse condizioni NULL/NOT NULL. Se, ad esempio, nel server di pubblicazione è stata eseguita un'istruzione CREATE TABLE e quindi un'istruzione ALTER TABLE per l'inserimento di colonne, ma lo script applicato al Sottoscrittore è una tabella CREATE semplice, la struttura NON è identica. Se non si è certi che la struttura delle due tabelle sia identica, esaminare [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) e verificare che l'offset di ogni tabella è lo stesso.  
  
 Valori a virgola mobile sono probabile che generino differenze di checksum se in modalità carattere **bcp** è stata usata, che si verifica se la pubblicazione esistono non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori. Ciò è dovuto a differenze di precisione minime ma inevitabili nella conversione da e verso la modalità carattere.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire **sp_table_validation**, è necessario disporre delle autorizzazioni SELECT sulla tabella da convalidare.  
  
## <a name="see-also"></a>Vedere anche  
 [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
