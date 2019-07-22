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
ms.openlocfilehash: ef21cdb2a223aaa50b690f5b2b3c30696dd9e196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988856"
---
# <a name="using-encryption-without-validation"></a>Utilizzo della crittografia senza convalida
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crittografa sempre pacchetti di rete associati all'accesso. Se non è stato eseguito il provisioning di nessun certificato nel server quando viene avviato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un certificato autofirmato utilizzato per crittografare pacchetti di accesso.  

I certificati autofirmati non garantiscono la sicurezza. L'handshake crittografato è basato su NT LAN Manager (NTLM). Si consiglia di effettuare il provisioning di un certificato verificabile in SQL Server per la connettività sicura. Il protocollo TLS (Transport Security Layer) può essere reso sicuro solo con la convalida del certificato.

Le applicazioni possono inoltre richiedere l'attivazione della crittografia per tutto il traffico di rete mediante le parole chiave della stringa di connessione o le proprietà di connessione. Le parole chiave sono "Encrypt" per OLE DB se si usa una stringa del provider con **IDbInitialize::Initialize** o "Use Encryption for Data" per ADO e OLE DB se si usa una stringa di inizializzazione con **IDataInitialize**. Questo può essere configurato anche da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando l'opzione **Forza crittografia protocollo** e configurando il client per richiedere connessioni crittografate. Per impostazione predefinita, la crittografia di tutto il traffico di rete per una connessione richiede che nel server sia stato eseguito il provisioning di un certificato. Impostando il client in modo che consideri attendibile il certificato nel server, è possibile che si siano vulnerabili agli attacchi man-in-the-Middle. Se si distribuisce un certificato verificabile nel server, assicurarsi di modificare le impostazioni client relative all'attendibilità del certificato su FALSE.

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
> La tabella precedente fornisce solo una guida al comportamento del sistema in configurazioni diverse. Per una connettività sicura, assicurarsi che sia il client che il server richiedano la crittografia. Verificare inoltre che il server disponga di un certificato verificabile e che l'impostazione **TrustServerCertificate** nel client sia impostata su false.

## <a name="ole-db-driver-for-sql-server"></a>Driver OLE DB per SQL Server 
 Il provider OLE DB per SQL Server supporta la crittografia senza convalida tramite l'aggiunta della proprietà di inizializzazione dell'origine dati SSPROP_INIT_TRUST_SERVER_CERTIFICATE, implementata nel set di proprietà DBPROPSET_SQLSERVERDBINIT. È stata inoltre aggiunta una nuova parola chiave, "TrustServerCertificate", per la stringa di connessione. Accetta i valori yes o no. Il valore predefinito è no. Quando si utilizzano i componenti del servizio, accetta i valori true o false; false è l'impostazione predefinita.  
  
 Per ulteriori informazioni sui miglioramenti apportati al set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [proprietà di inizializzazione e di autorizzazione](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
