---
title: Uso della crittografia senza convalida | Microsoft Docs
description: Uso della crittografia senza convalida
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 108aef449d80fa01e88fac29e6058754626b6aed
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802892"
---
# <a name="using-encryption-without-validation"></a>Utilizzo della crittografia senza convalida
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crittografa sempre pacchetti di rete associati all'accesso. Se non è stato eseguito il provisioning di nessun certificato nel server quando viene avviato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un certificato autofirmato utilizzato per crittografare pacchetti di accesso.  

I certificati autofirmati non garantisce la sicurezza. L'handshake di crittografia si basa su NT LAN Manager (NTLM). Si consiglia vivamente di effettuare il provisioning di un certificato verificabile in SQL Server per la connettività sicura. Transport Layer Security (TLS) è possibile proteggere solo con convalida del certificato.

Le applicazioni possono inoltre richiedere l'attivazione della crittografia per tutto il traffico di rete mediante le parole chiave della stringa di connessione o le proprietà di connessione. Le parole chiave sono "Encrypt" per OLE DB se si usa una stringa del provider con **IDbInitialize::Initialize** o "Use Encryption for Data" per ADO e OLE DB se si usa una stringa di inizializzazione con **IDataInitialize**. Ciò può anche essere configurata facendo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando il **Forza crittografia protocollo** opzione e configurare il client richieda connessioni crittografate. Per impostazione predefinita, la crittografia di tutto il traffico di rete per una connessione richiede che nel server sia stato eseguito il provisioning di un certificato. Tramite l'impostazione client per considerare attendibile il certificato nel server, potrebbe diventare vulnerabili ad attacchi man-in-the-middle. Se si distribuisce un certificato verificabile nel server, assicurarsi di modificare le impostazioni del client sull'attendibilità del certificato su FALSE.

Per informazioni sulle parole chiave della stringa di connessione, vedere [Uso delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
 Per abilitare l'uso della crittografia quando nel server non è stato eseguito il provisioning di un certificato, è possibile usare Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per impostare le opzioni **Forza crittografia protocollo** e **Certificato server attendibile**. In questo caso, la crittografia utilizzerà un certificato server autofirmato senza convalida se nel server non è stato eseguito il provisioning di alcun certificato verificabile.  
  
 Le applicazioni possono inoltre utilizzare la parola chiave "TrustServerCertificate" o il relativo attributo di connessione associato per garantire l'utilizzo della crittografia. Le impostazioni dell'applicazione non riducono mai il livello di sicurezza impostato dal client di Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], bensì possono potenziarlo. Un'applicazione può ad esempio richiedere la crittografia, se non è stata impostata l'opzione **Forza crittografia protocollo** per il client. Per garantire che la crittografia venga applicata anche quando non è stato eseguito il provisioning di un certificato server, un'applicazione può richiedere la crittografia e "TrustServerCertificate". Tuttavia, se TrustServerCertificate non è attivata nella configurazione client, è comunque necessario il provisioning di un certificato server. Nella tabella seguente vengono descritti tutti i casi:  
  
|Impostazione client Forza crittografia protocollo|Impostazione client Considera attendibile certificato server|Attributo/stringa di connessione Encrypt/Use Encryption for Data|Attributo/stringa di connessione Trust Server Certificate|Risultato|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|no|N/D|No (impostazione predefinita)|Ignorato|Nessuna crittografia.|  
|no|N/D|Sì|No (impostazione predefinita)|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|no|N/D|Sì|Sì|La crittografia viene sempre applicata, ma può essere utilizzato un certificato server auto-firmato.|  
|Sì|no|Ignorato|Ignorato|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|Sì|No (impostazione predefinita)|Ignorato|La crittografia viene sempre applicata, ma può essere utilizzato un certificato server auto-firmato.|  
|Sì|Sì|Sì|No (impostazione predefinita)|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|Sì|Sì|Sì|La crittografia viene sempre applicata, ma può essere utilizzato un certificato server auto-firmato.|  
||||||

> [!CAUTION]
> Nella tabella precedente offre solo una Guida sul comportamento del sistema in configurazioni diverse. Per una connettività sicura, assicurarsi che il client e server di richiedere la crittografia. Verificare inoltre che il server disponga di un certificato verificabile e che il **TrustServerCertificate** impostazione sul client è impostata su FALSE.

## <a name="ole-db-driver-for-sql-server"></a>Driver OLE DB per SQL Server 
 Il provider OLE DB per SQL Server supporta la crittografia senza convalida tramite l'aggiunta della proprietà di inizializzazione dell'origine dati SSPROP_INIT_TRUST_SERVER_CERTIFICATE, implementata nel set di proprietà DBPROPSET_SQLSERVERDBINIT. È stata inoltre aggiunta una nuova parola chiave, "TrustServerCertificate", per la stringa di connessione. Accetta i valori yes o no. Il valore predefinito è no. Quando si utilizzano i componenti del servizio, accetta i valori true o false; false è l'impostazione predefinita.  
  
 Per altre informazioni sui miglioramenti apportati al set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [proprietà di inizializzazione e autorizzazione](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
