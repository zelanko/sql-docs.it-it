---
title: sp_describe_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_parameter_encryption
- sp_describe_parameter_encryption_TSQL
- sys.sp_describe_parameter_encryption
- sys.sp_describe_parameter_encryption_TSQL
helpviewer_keywords:
- sp_describe_parameter_encryption
ms.assetid: 706ed441-2881-4934-8d5e-fb357ee067ce
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 243207c6175f5604e7cc887bd7c67085e2d86291
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507637"
---
# <a name="spdescribeparameterencryption-transact-sql"></a>sp_describe_parameter_encryption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Analizza l'oggetto specificato [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione e i relativi parametri, per determinare i parametri che corrispondono alle colonne del database che sono protetti tramite la funzionalità Always Encrypted. Restituisce i metadati di crittografia per i parametri che corrispondono alle colonne crittografate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ \@tsql =] 'Transact-SQL_batch'  
 Una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Transact-SQL_batch potrebbe essere nvarchar (n) o nvarchar (max).  
  
 [ \@params =] 'N'parameters  
 *\@params* fornisce una stringa di dichiarazione per i parametri per il batch Transact-SQL, che è simile a sp_executesql. I parametri possono essere nvarchar (n) o nvarchar (max).  
  
 Stringa che contiene le definizioni di tutti i parametri che sono stati incorporati nel [!INCLUDE[tsql](../../includes/tsql-md.md)]_batch. La stringa deve essere una costante o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n* è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato nell'istruzione deve essere definito  *\@params*. Se il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch nell'istruzione non contiene parametri,  *\@params* non è obbligatorio. Il valore predefinito per questo parametro è NULL.  
  
## <a name="return-value"></a>Valore restituito  
 0 indica l'esito positivo. Qualsiasi altro elemento indicano un errore.  
  
## <a name="result-sets"></a>Set di risultati  
 **sp_describe_parameter_encryption** restituisce due set di risultati:  
  
-   Il set di risultati che descrive le chiavi di crittografia configurate per le colonne di database, i parametri dell'oggetto specificato [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione corrispondono a.  
  
-   Il risultato impostato descrizione particolari come parametri deve essere crittografato. Questo set di risultati riferimenti chiavi descritte nel primo set di risultati.  
  
 Ogni riga del primo set di risultati descrive una coppia di chiavi; una chiave di crittografia di colonna crittografata e la chiave master della colonna corrispondente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|ID della riga nel set di risultati.|  
|**database_id**|**int**|Id del database.|  
|**column_encryption_key_id**|**int**|Id chiave di crittografia di colonna. Nota: questo id identifica una riga nel [Sys. column_encryption_keys &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) vista del catalogo.|  
|**column_encryption_key_version**|**int**|Riservato per utilizzi futuri. Attualmente contiene sempre 1.|  
|**column_encryption_key_metadata_version**|**binary(8)**|Un timestamp che rappresenta l'ora di creazione della chiave di crittografia della colonna.|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|Il valore crittografato della chiave di crittografia della colonna.|  
|**column_master_key_store_provider_name**|**sysname**|Il nome del provider per l'archivio chiavi contenente la chiave master della colonna, che è stata utilizzata per produrre il valore crittografato della chiave di crittografia della colonna.|  
|**column_master_key_path**|**nvarchar(4000)**|Il percorso della chiave della chiave master della colonna, che è stata utilizzata per produrre il valore crittografato della chiave di crittografia della colonna.|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|Il nome dell'algoritmo di crittografia utilizzato per produrre il valore di crittografia della chiave di crittografia della colonna.|  
  
 Ogni riga del secondo set di risultati contiene i metadati di crittografia per un parametro.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|ID della riga nel set di risultati.|  
|**parameter_name**|**sysname**|Nome di uno dei parametri specificati nel  *\@params* argomento.|  
|**column_encryption_algorithm**|**tinyint**|Il codice che indica l'algoritmo di crittografia configurato per la colonna, il parametro corrisponde al. I valori attualmente supportati sono: 2 per **AEAD_AES_256_CBC_HMAC_SHA_256**.|  
|**column_encryption_type**|**tinyint**|Codice che indica il tipo di crittografia configurato per la colonna, il parametro corrisponde alla. I valori supportati sono:<br /><br /> 0 - testo normale (la colonna non è crittografata)<br /><br /> 1 - casuale di crittografia<br /><br /> 2 - crittografia deterministica.|  
|**column_encryption_key_ordinal**|**int**|Codice della riga nel risultato del primo set. La riga di cui viene fatto riferimento descrive la chiave di crittografia della colonna configurata per la colonna, il parametro corrisponde alla.|  
|**column_encryption_normalization_rule_version**|**tinyint**|Numero di versione dell'algoritmo di normalizzazione di tipo.|  
  
## <a name="remarks"></a>Note  
 Oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver del client, che supporta Always Encrypted, chiama automaticamente **sp_describe_parameter_encryption** per recuperare i metadati di crittografia per le query con parametri, emessi dall'applicazione. Successivamente, il driver Usa i metadati di crittografia per crittografare i valori dei parametri che corrispondono alle colonne di database protette con Always Encrypted e sostituisce i valori dei parametri in testo normale, inviati dall'applicazione, con la crittografia valori dei parametri, prima di inviare la query al motore di database.  
  
## <a name="permissions"></a>Permissions  
 Richiede la **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** e **VIEW ANY COLUMN MASTER KEY DEFINITION** autorizzazioni nel database.  
  
## <a name="examples"></a>Esempi  
  
```  
CREATE COLUMN MASTER KEY [CMK1]  
WITH  
(  
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',  
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'  
);  
GO  
  
CREATE COLUMN ENCRYPTION KEY [CEK1]  
WITH VALUES  
(  
       COLUMN_MASTER_KEY = [CMK1],  
    ALGORITHM = 'RSA_OAEP',  
    ENCRYPTED_VALUE =   
0x016E000001630075007200720065006E00740075007300650072002F006D007  
9002F00610036003600620062003000660036006400640037003000620064006  
6006600300032006200360032006400300066003800370065003300340030003  
200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF991  
37B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA51  
7A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6  
686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015B  
DB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8  
C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE3  
74DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A3472  
3276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550E  
C5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E0  
35175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D8  
01ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B  
4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF8  
1A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202F  
C24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B0195883360  
4707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E  
9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C  
3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085  
);  
GO  
  
CREATE TABLE t1 (  
c1 INT ENCRYPTED WITH (  
    COLUMN_ENCRYPTION_KEY = [CEK_Auto1],   
    ENCRYPTION_TYPE = Randomized,   
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL,  
);  
  
EXEC sp_describe_parameter_encryption N'INSERT INTO t1 VALUES(@c1)',  N'@c1 INT';  
```  
  
 Ecco il primo set di risultati:  
  
|column_encryption_key_ordinal|database_id|column_encryption_key_id|column_encryption_key_version|column_encryption_key_metadata_version|column_encryption_key_encrypted_value|  
|--------------------------------------|------------------|---------------------------------|--------------------------------------|------------------------------------------------|-----------------------------------------------|  
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA 74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232 F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE2439 2D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B3864 87CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 (Risultati continuano).  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 Ecco il secondo set di risultati:  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@C1|1|1|  
  
 (Risultati continuano).  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>Vedere anche  
 [Always Encrypted &#40;Motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted &#40;client development&#41; (Always Encrypted - sviluppo client)](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
