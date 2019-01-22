---
title: CREATE ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fa20850f0784b734173f46ceee4235694c15b9cd
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361551"
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una chiave asimmetrica nel database.  
  
 Questa funzionalità non è compatibile con l'esportazione del database mediante Data Tier Application Framework (DACFx). Prima dell'esportazione, è necessario eliminare tutte le chiavi asimmetriche.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
CREATE ASYMMETRIC KEY Asym_Key_Name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <Asym_Key_Source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<Asym_Key_Source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY Assembly_Name  
   | PROVIDER Provider_Name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>Argomenti  
 FROM *Asym_Key_Source*  
 Specifica l'origine da cui caricare la coppia di chiavi asimmetriche.  
  
 AUTHORIZATION *database_principal_name*  
 Specifica il proprietario della chiave asimmetrica. Il proprietario non può essere un ruolo o un gruppo. Se l'opzione viene omessa, il proprietario sarà l'utente corrente.  
  
 FILE ='*path_to_strong-name_file*'  
 Specifica il percorso di un file con nome sicuro da cui caricare la coppia di chiavi.  
  
> [!NOTE]  
>  Questa opzione non è disponibile in un database indipendente.  
  
 EXECUTABLE FILE ='*path_to_executable_file*'  
 Viene specificato un file di assembly da cui caricare la chiave pubblica. Limitato a 260 caratteri da MAX_PATH dall'API Windows.  
  
> [!NOTE]  
>  Questa opzione non è disponibile in un database indipendente.  
  
 ASSEMBLY *Assembly_Name*  
 Specifica il nome di un assembly da cui caricare la chiave pubblica.  
  
ENCRYPTION BY *\<key_name_in_provider>* Specifica la crittografia usata per la chiave e può essere un certificato, una password o una chiave asimmetrica.  
  
 KEY_NAME ='*key_name_in_provider*'  
 Specifica il nome della chiave dal provider esterno. Per altre informazioni sulla gestione delle chiavi esterne, vedere [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 CREATION_DISPOSITION = CREATE_NEW  
 Crea una nuova chiave nel dispositivo EKM. Utilizzare PROV_KEY_NAME per specificare il nome della chiave nel dispositivo. Se nel dispositivo esiste già una chiave, l'istruzione genererà un errore.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 Definisce il mapping di una chiave asimmetrica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una chiave EKM esistente. Utilizzare PROV_KEY_NAME per specificare il nome della chiave nel dispositivo. Se CREATION_DISPOSITION = OPEN_EXISTING non è specificato, l'impostazione predefinita è CREATE_NEW.  
  
 ALGORITHM = \<algorithm>  
 Possono essere specificati cinque algoritmi: RSA_4096, RSA_3072, RSA_2048, RSA_1024 e RSA_512.  
  
 RSA_1024 e RSA_512 sono deprecati. Per usare RSA_1024 o RSA_512 (sconsigliato), è necessario impostare il database sul livello di compatibilità del database 120 o su uno inferiore.  
  
 PASSWORD = '*password*'  
 Specifica la password con cui crittografare la chiave privata. Se questa clausola è assente, la chiave privata verrà crittografata con la chiave master del database. *password* ha un massimo di 128 caratteri. *password* deve soddisfare i requisiti per i criteri password di Windows del computer che sta eseguendo l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Remarks  
 Una *chiave asimmetrica* è un'entità a protezione diretta a livello del database. Nella forma predefinita, questa entità contiene sia una chiave pubblica che una chiave privata. Se eseguita senza la clausola FROM, l'istruzione CREATE ASYMMETRIC KEY genera una nuova coppia di chiavi. Se eseguita con la clausola FROM, l'istruzione CREATE ASYMMETRIC KEY importa una coppia di chiavi da un file o importa una chiave pubblica da un assembly.  
  
 Per impostazione predefinita, la chiave privata è protetta dalla chiave master del database. Se non esiste una chiave master del database, è necessario proteggere la chiave privata con una password. In presenza di una chiave master del database, la password è facoltativa.  
  
 La chiave privata può avere una lunghezza di 512, 1024 o 2048 bit.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CREATE ASYMMETRIC KEY per il database. Se si specifica la clausola AUTHORIZATION, è richiesta l'autorizzazione IMPERSONATE per l'entità di database o l'autorizzazione ALTER per il ruolo applicazione. Solo gli account di accesso di Windows e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i ruoli applicazione possono disporre di chiavi asimmetriche. I gruppi e i ruoli non possono disporre di chiavi asimmetriche.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-an-asymmetric-key"></a>A. Creazione di una chiave asimmetrica  
 Nell'esempio seguente viene creata una chiave asimmetrica denominata `PacificSales09` tramite l'algoritmo `RSA_2048` e la chiave privata viene protetta con una password.  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>b. Creazione di una chiave asimmetrica da un file e concessione dell'autorizzazione a un utente  
 Nell'esempio seguente viene creata la chiave asimmetrica `PacificSales19` da una coppia di chiavi memorizzate in un file; l'utente `Christina` viene quindi autorizzato all'utilizzo della chiave asimmetrica.  
  
```  
CREATE ASYMMETRIC KEY PacificSales19 AUTHORIZATION Christina   
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp'    
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>C. Creazione di una chiave asimmetrica da un provider EKM  
 L'esempio seguente illustra come creare la chiave asimmetrica `EKM_askey1` da una coppia di chiavi memorizzate in un file. La crittografia avviene utilizzando un provider EKM denominato `EKMProvider1` e una chiave nel provider denominata `key10_user1`.  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Scelta di un algoritmo di crittografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
