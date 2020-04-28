---
title: Certificati SQL Server e chiavi simmetriche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server], certificates and asymmetric keys
ms.assetid: 8519aa2f-f09c-4c1c-96b5-abc24811e60c
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ddb7e84f69f501a7857b0d55b1b8a14d11a85694
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75244505"
---
# <a name="sql-server-certificates-and-asymmetric-keys"></a>Certificati SQL Server e chiavi simmetriche
   La crittografia a chiave pubblica (PKI) è un sistema di tutela della segretezza dei messaggi in cui un utente crea una chiave *pubblica* e una chiave *privata*. La chiave privata viene tenuta segreta, mentre la chiave pubblica può essere distribuita ad altri. Sebbene le chiavi siano collegate da una relazione matematica, non è possibile estrapolare facilmente la chiave privata utilizzando la chiave pubblica. La chiave pubblica viene utilizzata per crittografare dati mentre quella privata viene impiegata per decrittografarli. Un messaggio crittografato con la chiave pubblica può essere decrittografato solo utilizzando la chiave privata corretta. Poiché si tratta di due chiavi diverse, queste chiavi sono *asimmetriche*.  
  
 Certificati e chiavi asimmetriche rappresentano entrambi una modalità di utilizzo della crittografia asimmetrica. I certificati vengono spesso utilizzati come contenitori delle chiavi asimmetriche perché possono contenere un maggior numero di informazioni, ad esempio date di scadenza e autorità emittenti. Non c'è differenza tra i due meccanismi per l'algoritmo di crittografia e nessuna differenza nel livello di protezione fornito a parità di lunghezza della chiave. In genere, si utilizza un certificato per crittografare gli altri tipi di chiavi di crittografia in un database o per firmare moduli di codice.  
  
 Certificati e chiavi asimmetriche sono in grado di decrittografare dati crittografati da altri. In genere, la crittografia asimmetrica viene utilizzata per crittografare una chiave simmetrica da archiviare in un database.  
  
 Al contrario di un certificato, una chiave pubblica non presenta un formato particolare e non può essere esportata in un file.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene caratteristiche che consentono di creare e gestire certificati e chiavi da utilizzare con il server e il database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per creare e gestire certificati e chiavi con le altre applicazioni o nel sistema operativo.  
  
## <a name="certificates"></a>Certificati  
 Un certificato è un oggetto di sicurezza provvisto di firma digitale all'interno del quale è presente una chiave pubblica (e facoltativamente una privata) per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile utilizzare certificati generati all'esterno o da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] I certificati sono conformi allo standard per certificati IETF X.509v3.  
  
 L'utilità dei certificati deriva dall'opzione che consente di esportare e importare le chiavi a file di certificato X.509. La sintassi per la creazione di certificati offre opzioni come l'impostazione di una data di scadenza.  
  
### <a name="using-a-certificate-in-sql-server"></a>Utilizzo di un certificato in SQL Server  
 È possibile utilizzare i certificati per proteggere connessioni, eseguire il mirroring del database, firmare pacchetti e altri oggetti o crittografare dati o connessioni. Nella tabella seguente sono elencate risorse aggiuntive per i certificati presenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)|Viene descritto il comando per la creazione di certificati.|  
|[Identificazione dell'origine dei pacchetti con firme digitali](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)|Vengono fornite informazioni sull'utilizzo di certificati per la firma di pacchetti software.|  
|[Usare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|Vengono fornite informazioni sull'utilizzo dei certificati con il mirroring del database.|  
  
## <a name="asymmetric-keys"></a>Chiavi asimmetriche  
 Le chiavi asimmetriche sono utilizzate per proteggere le chiavi simmetriche. È possibile utilizzarle anche per una crittografia limitata dei dati e per la firma digitale di oggetti di database. Una chiave asimmetrica consiste in una chiave privata e in una chiave pubblica corrispondente. Per altre informazioni sulle chiavi simmetriche, vedere [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql).  
  
 È possibile importare le chiavi asimmetriche da file di chiave con nome sicuro, ma non esportarle. Le chiavi asimmetriche, inoltre, non hanno opzioni di scadenza e non sono in grado di crittografare connessioni.  
  
### <a name="using-an-asymmetric-key-in-sql-server"></a>Utilizzo di una chiave asimmetrica in SQL Server  
 È possibile utilizzare chiavi asimmetriche per proteggere dati o firmare testo non crittografato. Nella tabella seguente sono elencate risorse aggiuntive per chiavi asimmetriche presenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)|Viene descritto il comando per la creazione di chiavi asimmetriche.|  
|[SIGNBYASYMKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/signbyasymkey-transact-sql)|Vengono visualizzate le opzioni per la firma di oggetti.|  
  
## <a name="tools"></a>Strumenti  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] vengono forniti strumenti e utilità in grado di generare certificati e file di chiave con nome sicuro. Questi strumenti offrono maggiore flessibilità nel processo di generazione delle chiavi rispetto alla sintassi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È possibile utilizzare questi strumenti per creare chiavi RSA con lunghezze di chiave più complesse e importarle quindi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nella tabella seguente viene indicato dove è possibile trovare questi strumenti.  
  
|||  
|-|-|  
|Strumento|Scopo|  
|[Makecert](https://msdn2.microsoft.com/library/bfsktky3\(VS.80\).aspx)|Vengono creati certificati.|  
|[sn](https://msdn2.microsoft.com/library/k5b5tt23\(VS.80\).aspx)|Vengono creati nomi sicuri per le chiavi simmetriche.|  
  
## <a name="related-tasks"></a>Attività correlate  
 [Scelta di un algoritmo di crittografia](encryption/choose-an-encryption-algorithm.md)  
  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [sys. Certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)   
 [Transparent Data Encryption &#40;TDE&#41;](encryption/transparent-data-encryption.md)  
  
