---
title: Creare chiavi simmetriche identiche su due server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 38eaccffff89b0be7e59f628fcfb9b6e772a02b1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063191"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>Creare chiavi simmetriche identiche su due server
  In questo argomento viene descritto come creare chiavi simmetriche identiche in due server diversi in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Al fine di decrittografare l'argomento ciphertext, è necessario disporre della chiave usata per crittografarlo. Quando la crittografia e la decrittografia vengono eseguite in un unico database, la chiave viene archiviata nel database ed è disponibile, a seconda delle autorizzazioni, sia per la crittografia che per la decrittografia. Viceversa, quando la crittografia e la decrittografia vengono eseguite in database separati, la chiave archiviata in un database non è disponibile per l'utilizzo nell'altro database.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per creare chiavi simmetriche identiche su due server diversi tramite Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando si crea una chiave simmetrica è necessario crittografarla con almeno uno degli elementi seguenti: certificato, password, chiave simmetrica, chiave asimmetrica o PROVIDER. Una chiave può essere crittografata con più elementi di ogni tipo, ovvero una singola chiave simmetrica può essere crittografata contemporaneamente con più certificati, password, chiavi simmetriche e chiavi asimmetriche.  
  
-   Se si crittografa una chiave simmetrica con una password anziché con la chiave pubblica della chiave master del database, viene usato l'algoritmo di crittografia TRIPLE DES. Per questo motivo, le chiavi create con un algoritmo di crittografia avanzato, come AES, vengono a loro volta protette con un algoritmo meno avanzato.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER ANY SYMMETRIC KEY per il database. Se si specifica AUTHORIZATION, è richiesta l'autorizzazione IMPERSONATE per l'utente di database o l'autorizzazione ALTER per il ruolo applicazione. Se la crittografia viene applicata con un certificato o una chiave asimmetrica, è richiesta l'autorizzazione VIEW DEFINITION per il certificato o la chiave asimmetrica. Solo gli account di accesso di Windows e di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e i ruoli applicazione possono disporre di chiavi simmetriche. I gruppi e i ruoli non possono disporre di chiavi simmetriche.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>Per creare chiavi simmetriche identiche su due server diversi  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Creare una chiave eseguendo le seguenti istruzioni CREATE MASTER KEY, CREATE CERTIFICATE e CREATE SYMMETRIC KEY.  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  Connettersi a un'istanza del server separata, aprire una finestra Query diversa ed eseguire le istruzioni SQL precedenti per creare la stessa chiave nel secondo server.  
  
5.  Verificare le chiavi eseguendo prima l'istruzione OPEN SYMMETRIC KEY e quindi l'istruzione SELECT seguente nel primo server.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  Nell'altro server incollare il risultato dell'istruzione SELECT precedente nel codice indicato di seguito come valore di `@blob` ed eseguire il codice per verificare che la chiave duplicata sia in grado di decrittografare il testo crittografato.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  Chiudere la chiave simmetrica in entrambi i server.  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/decryptbykey-transact-sql)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-symmetric-key-transact-sql)  
  
  
