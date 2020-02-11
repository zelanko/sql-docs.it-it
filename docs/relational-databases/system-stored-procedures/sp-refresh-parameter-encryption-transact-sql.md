---
title: sp_refresh_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5f699f21b1f28537da2e2f0033fe6b17908186a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002459"
---
# <a name="sp_refresh_parameter_encryption-transact-sql"></a>sp_refresh_parameter_encryption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Aggiorna i metadati di Always Encrypted per i parametri della stored procedure non associata a schema specificata, della funzione definita dall'utente, della vista, del trigger DML, del trigger DDL a livello di database o del trigger DDL a livello di server nel database corrente. 

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>Argomenti

`[ @name = ] 'module_name'`Nome del stored procedure, funzione definita dall'utente, vista, trigger DML, trigger DDL a livello di database o trigger DDL a livello di server. *module_name* non può essere un stored procedure di Common Language Runtime (CLR) o una funzione CLR. *module_name* non possono essere associati a schema. *module_name* è `nvarchar`di e non prevede alcun valore predefinito. *module_name* può essere un identificatore in più parti, ma può fare riferimento solo agli oggetti nel database corrente.

`[ @namespace = ] ' < class > '`È la classe del modulo specificato. Quando *module_name* è un trigger DDL, `<class>` è obbligatorio. 
  `<class>` è `nvarchar(20)`. Gli input validi `DATABASE_DDL_TRIGGER` sono `SERVER_DDL_TRIGGER`e.    

## <a name="return-code-values"></a>Valori del codice restituito  

0 (esito positivo) o un numero diverso da zero (esito negativo)


## <a name="remarks"></a>Osservazioni

I metadati di crittografia per i parametri di un modulo possono diventare obsoleti, se:   
* Sono state aggiornate le proprietà di crittografia di una colonna in una tabella a cui fa riferimento il modulo. Una colonna, ad esempio, è stata eliminata e viene aggiunta una nuova colonna con lo stesso nome, ma è stato aggiunto un tipo di crittografia diverso, una chiave di crittografia o un algoritmo di crittografia.  
* Il modulo fa riferimento a un altro modulo con metadati di crittografia dei parametri obsoleti.  

Quando si modificano le proprietà di crittografia di `sp_refresh_parameter_encryption` una tabella, è necessario eseguire per tutti i moduli direttamente o indirettamente che fanno riferimento alla tabella. Questo stored procedure può essere chiamato su tali moduli in qualsiasi ordine, senza richiedere all'utente di aggiornare prima di tutto il modulo interno prima di trasferirsi ai chiamanti.

`sp_refresh_parameter_encryption`non influisce sulle autorizzazioni, sulle proprietà estese `SET` o sulle opzioni associate all'oggetto. 

Per aggiornare un trigger DDL a livello di server, eseguire questa stored procedure dal contesto di un qualsiasi database.

> [!NOTE]
>  Tutte le firme associate all'oggetto vengono eliminate quando si esegue `sp_refresh_parameter_encryption`.

## <a name="permissions"></a>Autorizzazioni

È `ALTER` richiesta l'autorizzazione per il `REFERENCES` modulo e l'autorizzazione per tutti i tipi CLR definiti dall'utente e le raccolte di XML Schema a cui fa riferimento l'oggetto.   

Quando il modulo specificato è un trigger DDL a livello di database, `ALTER ANY DATABASE DDL TRIGGER` richiede l'autorizzazione nel database corrente.    

Quando il modulo specificato è un trigger DDL a livello di server, `CONTROL SERVER` richiede l'autorizzazione.

Per i moduli definiti con la `EXECUTE AS` clausola, `IMPERSONATE` è richiesta l'autorizzazione per l'entità specificata. In genere, l'aggiornamento di un oggetto non `EXECUTE AS` comporta la modifica dell'entità, a meno che `EXECUTE AS USER` il modulo non sia stato definito con e il nome utente del server principale venga risolto in un altro utente rispetto al momento in cui è stato creato il modulo.
 
## <a name="examples"></a>Esempi

Nell'esempio seguente viene creata una tabella e una procedura che fa riferimento alla tabella, viene configurato Always Encrypted, quindi viene illustrata la modifica della `sp_refresh_parameter_encryption` tabella e l'esecuzione della stored procedure.  

Creare innanzitutto la tabella iniziale e un stored procedure che fa riferimento alla tabella.
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

Quindi impostare Always Encrypted chiavi.
```sql
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
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


Infine si sostituisce la colonna SSN con la colonna crittografata, quindi viene eseguita `sp_refresh_parameter_encryption` la procedura per aggiornare i componenti del always Encrypted.
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>Vedere anche 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Procedura guidata Always Encrypted](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

