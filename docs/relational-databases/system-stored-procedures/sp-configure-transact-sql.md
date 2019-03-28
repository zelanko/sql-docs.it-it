---
title: sp_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 23b75beb0782fc0a13155d12890cbe3a620e1733
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530243"
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  Visualizza o modifica le impostazioni di configurazione globali per il server corrente.

> [!NOTE]  
>  Per le opzioni di configurazione a livello di database, vedere [ALTER DATABASE ambito di configurazione &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Per configurare Soft-NUMA, vedere [Soft-NUMA &#40;di SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @configname = ] 'option_name'` È il nome di un'opzione di configurazione. *option_name* è **varchar(35)** e il valore predefinito è NULL. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] riconosce qualsiasi stringa univoca che faccia parte del nome della configurazione. Se non si specifica alcun nome di opzione, viene restituito l'elenco completo delle opzioni.  
  
 Per informazioni sulle opzioni di configurazione disponibili e le relative impostazioni, vedere [opzioni di configurazione &#40;di SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
`[ @configvalue = ] 'value'` È la nuova impostazione di configurazione. *value* è **int**e il valore predefinito è NULL. Il valore massimo dipende dalla singola opzione.  
  
 Per visualizzare il valore massimo per ogni opzione, vedere la **massima** colonna di **sys.configurations** visualizzazione catalogo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Se eseguita senza parametri, **sp_configure** restituisce un set di risultati con cinque colonne e Ordina le opzioni in ordine alfabetico in ordine crescente, come illustrato nella tabella seguente.  
  
 I valori per **config_value** e **run_value** non sono automaticamente equivalenti. Dopo aver aggiornato un'impostazione di configurazione usando **sp_configure**, l'amministratore di sistema è necessario aggiornare il valore di configurazione utilizzando l'istruzione RECONFIGURE o RECONFIGURE WITH OVERRIDE. Per altre informazioni, vedere la sezione Osservazioni.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|Nome dell'opzione di configurazione.|  
|**minimum**|**int**|Valore minimo dell'opzione di configurazione.|  
|**maximum**|**int**|Valore massimo dell'opzione di configurazione.|  
|**config_value**|**int**|Valore a cui è stata impostata l'opzione di configurazione usando **sp_configure** (valore nelle **Configurations**). Per ulteriori informazioni su queste opzioni, vedere [opzioni di configurazione &#40;di SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) e [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**int**|Valore dell'opzione di configurazione (valore in **value_in_use**).<br /><br /> Per ulteriori informazioni, vedere [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>Note  
 Uso **sp_configure** per visualizzare o modificare le impostazioni a livello di server. Per modificare le impostazioni a livello di database, utilizzare ALTER DATABASE. Per modificare le impostazioni che interessano solo la sessione utente corrente, utilizzare l'istruzione SET.  
  
## <a name="updating-the-running-configuration-value"></a>Aggiornamento del valore di configurazione corrente  
 Quando si specifica un nuovo *valore* per un' *opzione*, il set di risultati Mostra questo valore di **config_value** colonna. Questo valore inizialmente è diverso dal valore di **run_value** colonna che mostra il valore di configurazione attualmente in esecuzione. Per aggiornare il valore di configurazione nel **run_value** colonna, l'amministratore di sistema deve eseguire RECONFIGURE o RECONFIGURE WITH OVERRIDE.  
  
 Sia RECONFIGURE che RECONFIGURE WITH OVERRIDE funzionano con tutte le opzioni di configurazione. L'istruzione RECONFIGURE, tuttavia, non accetta i valori di opzione che non rientrano in un intervallo ragionevole o che possono causare conflitti tra le opzioni. Ad esempio RECONFIGURE genera un errore se il **intervallo di recupero** valore è maggiore di 60 minuti o se il **maschera di affinità** valore si sovrappone con il **maschera di affinità i/o**valore. RECONFIGURE WITH OVERRIDE, invece, accetta qualsiasi valore di opzione con il tipo di dati corretto e impone la riconfigurazione utilizzando il valore specificato.  
  
> [!CAUTION]  
>  Un valore non corretto può compromettere la configurazione dell'istanza del server. Utilizzare RECONFIGURE WITH OVERRIDE con cautela.  
  
 L'istruzione RECONFIGURE aggiorna alcune opzioni in modo dinamico. Per altre è necessario arrestare e riavviare il server. Ad esempio, il **memoria server min** e **massima di memoria del server** opzioni memoria server vengono aggiornate dinamicamente la [!INCLUDE[ssDE](../../includes/ssde-md.md)]; pertanto, possono essere modificate senza riavviare il server. Riconfigurazione, al contrario, il valore di **il fattore di riempimento** opzione richiede il riavvio di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Dopo aver eseguito RECONFIGURE per un'opzione di configurazione, è possibile visualizzare se l'opzione è stata aggiornata in modo dinamico eseguendo **sp_configure'***nome_opzione***'**. I valori di **run_value** e **config_value** colonne devono corrispondere a un'opzione aggiornato in modo dinamico. È possibile anche verificare quali opzioni sono dinamiche osservando la **is_dynamic** della colonna della **Sys. Configurations** vista del catalogo.  
  
> [!NOTE]  
>  Se un oggetto specificato *valore* troppo elevato per un'opzione, il **run_value** colonna riflette il fatto che il [!INCLUDE[ssDE](../../includes/ssde-md.md)] ha impostato come predefinito per la memoria dinamica, anziché usare un'impostazione che non è valida.  
  
 Per ulteriori informazioni, vedere [RICONFIGURARE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>Opzioni avanzate  
 Configurazione di alcune opzioni, ad esempio **maschera di affinità** e **intervallo di recupero**, sono designati come opzioni avanzate. Per impostazione predefinita non è possibile visualizzarle e modificarle. Per renderli disponibili, impostare il **ShowAdvancedOptions** l'opzione di configurazione a 1.  
  
 Per ulteriori informazioni sulle opzioni di configurazione e le relative impostazioni, vedere [opzioni di configurazione &#40;di SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per modificare un'opzione di configurazione o per eseguire l'istruzione RECONFIGURE, è necessario essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. Visualizzazione dell'elenco delle opzioni di configurazione avanzate  
 Nell'esempio seguente viene illustrato come impostare ed elencare tutte le opzioni di configurazione. Le opzioni di configurazione avanzate vengono visualizzate se innanzitutto si imposta `show advanced option` su `1`. In seguito alla modifica di questa opzione, se si esegue `sp_configure` senza parametri, verranno visualizzate tutte le opzioni di configurazione.  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 Ecco il messaggio: "Opzione di configurazione 'show advanced options' modificato da 0 a 1. Per eseguire l'installazione, utilizzare RECONFIGURE".  
  
 Eseguire `RECONFIGURE` e visualizzare tutte le opzioni di configurazione:  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. Modifica di un'opzione di configurazione  
 Nell'esempio seguente viene impostato il valore di `recovery interval` del sistema su `3` minuti.  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. Elencare tutte le impostazioni di configurazione disponibili  
 L'esempio seguente mostra come impostare ed elencare tutte le opzioni di configurazione.  
  
```  
EXEC sp_configure;  
```  
  
 Il risultato restituisce il nome dell'opzione seguito dai valori minimi e massimo per l'opzione. Il **config_value** è il valore che [!INCLUDE[ssDW](../../includes/ssdw-md.md)] utilizzerà per la riconfigurazione è completa. **config_value** è il valore in uso. The **config_value** e **run_value** sono in genere uguali, a meno che il valore non sia in corso di modifica.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. Elencare le impostazioni di configurazione per un nome di configurazione  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Impostare la connettività Hadoop  
 L'impostazione Hadoop connectivity richiede alcuni passaggi aggiuntivi oltre a eseguire sp_configure. Per istruzioni complete, vedere [Crea origine dati esterna &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
