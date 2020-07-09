---
title: Extensible Key Management con Azure Key Vault
description: Usare il Connettore SQL Server per Extensible Key Management con Azure Key Vault per SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/22/2016
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 71145a184d13ad4ca4393cd1468293e40f0ad594
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896851"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per Insieme credenziali chiavi [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure consente alla crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di usare il servizio dell'insieme di credenziali delle chiavi di Azure come provider di [Extensible Key Management &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) per proteggere le [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] chiavi di crittografia.  
  
 Questo argomento descrive il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Altre informazioni sono disponibili in [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)e [Manutenzione e risoluzione dei problemi del Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  
  
##  <a name="what-is-extensible-key-management-ekm-and-why-use-it"></a><a name="Uses"></a> Che cos'è Extensible Key Management (EKM) e perché usarlo?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include diversi tipi di crittografia che consentono di proteggere i dati sensibili, inclusi [Transparent Data Encryption &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md), [Crittografia a livello di colonna](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (CLE) e [Crittografia dei backup](../../../relational-databases/backup-restore/backup-encryption.md). Nella gerarchia delle chiavi tradizionale di tutti questi casi i dati vengono crittografati usando una chiave (DEK) simmetrica. Per proteggerla ulteriormente, tale chiave viene crittografata con una gerarchia di chiavi archiviate in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'alternativa a questo modello è il modello di provider EKM. L'architettura del provider EKM consente a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di proteggere le chiavi DEK usando una chiave asimmetrica archiviata all'esterno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un provider del servizio di crittografia esterno. Questo modello aggiunge un altro livello di sicurezza e separa la gestione delle chiavi e dei dati.  
   
 L'immagine seguente confronta la tradizionale gerarchia delle chiavi con la gestione del servizio al sistema dell'insieme di credenziali delle chiavi di Azure.  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 Il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funge da ponte tra [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e l'insieme di credenziali delle chiavi di Azure, in modo che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possa sfruttare la scalabilità, le prestazioni elevate e la disponibilità elevata del servizio dell'insieme di credenziali delle chiavi di Azure. L'immagine seguente rappresenta il funzionamento della gerarchia delle chiavi nell'architettura del provider EKM con l'insieme di credenziali delle chiavi di Azure e il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  L'insieme di credenziali delle chiavi di Azure può essere usato con le installazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle macchine virtuali di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure e per i server locali. Il servizio dell'insieme di credenziali delle chiavi consente inoltre di usare i moduli di protezione hardware (HSM) controllati e monitorati rigorosamente per un livello di protezione maggiore per le chiavi di crittografia asimmetriche. Per altre informazioni sull'insieme di credenziali delle chiavi, vedere [Insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521401).  
  
 L'immagine seguente illustra il flusso di processo di EKM con l'insieme di credenziali delle chiavi. I numeri dei passaggi del processo nell'immagine non sono concepiti per corrispondere ai numeri dei passaggi della configurazione riportati di seguito.  
  
 ![EKM di SQL Server con Azure Key Vault](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "EKM di SQL Server con Azure Key Vault")  

> [!NOTE]  
>  Le versioni 1.0.0.440 e precedenti sono state sostituite e non sono più supportate negli ambienti di produzione. Eseguire l'aggiornamento alla versione 1.0.1.0 o successiva visitando l'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e seguendo le istruzioni nella pagina [Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) in "Aggiornamento del Connettore SQL Server".
  
 Per il passaggio successivo, vedere [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md).  
  
 Per gli scenari di utilizzo, vedere [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
