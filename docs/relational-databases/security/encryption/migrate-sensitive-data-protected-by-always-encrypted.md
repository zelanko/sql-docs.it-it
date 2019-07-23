---
title: Migrare dati sensibili protetti da Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
author: aliceku
ms.author: aliceku
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff72a94df79c6f8fe7b8bb37caeb57587e44b034
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111668"
---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>Migrare dati sensibili protetti da Crittografia sempre attiva
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Per caricare i dati crittografati senza eseguire controlli dei metadati sul server durante le operazioni di copia bulk, creare l'utente con l'opzione **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** . Questa opzione è destinata all'uso da parte di strumenti legacy appartenenti a versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] (come bcp.exe) o con flussi di lavoro Extract-Transform-Load (ETL) di terze parti che non possono usare Always Encrypted. In questo modo un utente può spostare in sicurezza i dati crittografati da un set di tabelle contenenti colonne crittografate a un altro set di tabelle con colonne crittografate (nello stesso database o in un altro).  

 ## <a name="the-allowencryptedvaluemodifications-option"></a>Opzione ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 Sia [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md) che [ALTER USER](../../../t-sql/statements/alter-user-transact-sql.md) hanno un'opzione ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Quando è impostata su ON (il valore predefinito è OFF), questa opzione disattiva i controlli dei dati crittografici sul server nelle operazioni di copia bulk, il che consente all'utente di eseguire la copia bulk dei dati crittografati fra tabelle o database senza decrittografarli.  
  
## <a name="data-migration-scenarios"></a>Scenari di migrazione  
La tabella seguente mostra le impostazioni consigliate appropriate per diversi scenari di migrazione.  
 
![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  

## <a name="bulk-loading-of-encrypted-data"></a>Caricamento bulk di dati crittografati  
Usare la seguente procedura per caricare dati crittografati.  

1.  Impostare l'opzione su ON per l'utente nel database di destinazione dell'operazione di copia bulk. Esempio:  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  Eseguire l'applicazione o lo strumento di copia bulk connettendosi con le credenziali di quell'utente. Se l'applicazione usa un driver client con Always Encrypted, verificare che la stringa di connessione per l'origine dati non contenga **column encryption setting=enabled** per garantire che i dati recuperati dalle colonne crittografate rimangano crittografati. Per altre informazioni, vedere [Always Encrypted &#40;client development&#41; (Always Encrypted - sviluppo client)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)(Always Encrypted - sviluppo client).  
  
3.  Impostare di nuovo l'opzione ALLOW_ENCRYPTED_VALUE_MODIFICATIONS su OFF. Esempio:  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>Possibile danneggiamento dei dati  
L'uso improprio di questa opzione può causare il danneggiamento dei dati. L'opzione **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** consente all'utente di inserire dati di qualsiasi tipo in colonne crittografate del database, compresi i dati crittografati con chiavi diverse, crittografati in modo non corretto o non crittografati. Se l'utente copia accidentalmente dati che non sono crittografati in modo corretto usando lo schema di crittografia (chiave di crittografia della colonna, algoritmo, tipo di crittografia) impostato per la colonna di destinazione, non sarà possibile decrittografare i dati (i dati verranno danneggiati). Questa opzione deve essere utilizzata con attenzione, in quanto può causare il danneggiamento dei dati nel database.  

Lo scenario seguente dimostra come un'importazione non corretta può causare il danneggiamento dei dati:  

1.  L'opzione è impostata su ON per un utente.  
 
2.  L'utente esegue l'applicazione che si connette al database. L'applicazione usa le API bulk per inserire valori di testo normale nelle colonne crittografate. L'applicazione si aspetta che un driver client con Crittografia sempre attiva crittografi i dati durante l'inserimento. L'applicazione, tuttavia, non è configurata correttamente e di conseguenza o usa un driver che non supporta Always Encrypted o la stringa di connessione non contiene **column encryption setting=enabled**.  

3.  L'applicazione invia i valori di testo normale al server. Poiché i controlli dei metadati crittografici sono disattivati nel server per l'utente, il server lascia che i dati non corretti (testo normale anziché testo crittografato) siano inseriti nella colonna crittografata.  
 
4.  La stessa applicazione o un'altra si collega al database usando un driver con Always Encrypted e con **column encryption setting=enabled** nella stringa di connessione e recupera i dati. L'applicazione si aspetta che i dati siano decrittografati in modo trasparente. Tuttavia, il driver non riesce a decrittografare i dati perché sono costituiti da testo crittografato non corretto.  

## <a name="best-practice"></a>Procedura consigliata  
 
Usare account utente designati per i carichi di lavoro con esecuzione prolungata.  
 
Per applicazioni o strumenti di copia bulk con esecuzione breve che richiedono di spostare i dati crittografati senza decrittografarli, impostare l'opzione su ON immediatamente prima di eseguire l'applicazione e impostarla di nuovo su OFF immediatamente dopo averla eseguita.  
 
Evitare l'uso di questa opzione per sviluppare nuove applicazioni. Usare invece un driver client (ad esempio, ADO 4.6.1) che offre un'API per la disattivazione dei controlli dei metadati crittografici per una singola sessione.  

## <a name="see-also"></a>Vedere anche  
[CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
[ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
[Always Encrypted &#40;Motore di database&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Procedura guidata Crittografia sempre attiva](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
[Always Encrypted &#40;client development&#41; (Always Encrypted - sviluppo client)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
