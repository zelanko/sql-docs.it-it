---
title: Funzionalità del driver OLE DB per SQL Server | Microsoft Docs
description: Funzionalità del driver OLE DB per SQL Server
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3cb73bb9ea3685793de692ae9cff1508e8a7656c
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006900"
---
# <a name="ole-db-driver-for-sql-server-features"></a>Funzionalità del driver OLE DB per SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Oltre a esporre le funzionalità di Windows (in precedenza Microsoft) Data Access Components (WDAC), il driver OLE DB per SQL Server implementa anche molte altre funzionalità che consentono di esporre le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione    
 [Uso del mirroring del database](../../oledb/features/using-database-mirroring.md)  
 Viene descritto in che modo il driver OLE DB per SQL Server supporta l'uso di database con mirroring, cioè la capacità di mantenere una copia, o mirror, di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un server di standby.  
  
 [Esecuzione di operazioni asincrone](../../oledb/features/performing-asynchronous-operations.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta le operazioni asincrone, ovvero la capacità di restituzione immediata senza blocchi sul thread chiamante.  

[Uso di Azure Active Directory](using-azure-active-directory.md)  
Vengono illustrati i nuovi metodi di autenticazione introdotti nel driver OLE DB 18.2.1 che hanno impostazioni predefinite più sicure e consentono la connessione a un'istanza del database SQL di Azure usando un'identità federata.

 [Uso di MARS &#40;Multiple Active Result Set&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Viene descritto in che modo OLE DB Driver per SQL Server supporta la funzionalità MARS (Multiple Active Result Set). che consente di eseguire e ricevere più set di risultati utilizzando una sola connessione al database.  
  
 [Uso di tipi di dati XML](../../oledb/features/using-xml-data-types.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta i dati XML, ovvero un tipo di dati basato su XML che è possibile usare come tipo di colonna, tipo di variabile, tipo di parametro o tipo restituito dalla funzione.  
  
 [Uso dei tipi definiti dall'utente](../../oledb/features/using-user-defined-types.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta i tipi definiti dall'utente (UDT) che estendono il sistema dei tipi SQL consentendo di archiviare oggetti e strutture dei dati personalizzate in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Uso di tipi valore di grandi dimensioni](../../oledb/features/using-large-value-types.md)  
 Viene descritto in che modo OLE DB Driver per SQL Server supporta i tipi di dati per valori di grandi dimensioni, ovvero i tipi di dati LOB (Large Object).  
  
 [Modifica delle password a livello di codice](../../oledb/features/changing-passwords-programmatically.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta la gestione delle password scadute per consentirne la modifica sul client senza il coinvolgimento dell'amministratore.  
  
 [Uso dell'isolamento dello snapshot](../../oledb/features/working-with-snapshot-isolation.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta il miglioramento del controllo delle versioni delle righe che comporta a sua volta un miglioramento delle prestazioni del database evitando le situazioni di blocco in lettura/scrittura.  
  
 [Uso delle notifiche delle query](../../oledb/features/working-with-query-notifications.md)  
 Descrive in che modo OLE DB Driver per SQL Server supporta le notifiche del consumer durante la modifica del set di righe.  
  
 [Esecuzione di operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta operazioni di copia bulk che consentono il trasferimento di grandi quantità di dati all'interno o all'esterno di una tabella o vista di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Uso della crittografia senza convalida](../../oledb/features/using-encryption-without-validation.md)  
 Viene descritto come usare OLE DB Driver per SQL Server per crittografare i dati inviati al server senza convalidare il certificato.  
  
 [Parametri con valori di tabella &#40;driver OLE DB per SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Descrive il supporto di OLE DB Driver per SQL Server dei parametri con valori di tabella.  
  
 [Tipi CLR definiti dall'utente di grandi dimensioni](../../oledb/features/large-clr-user-defined-types.md)  
 Si illustra il supporto dei tipi CRL definiti dall'utente di grandi dimensioni.  
  
 [Supporto FILESTREAM](../../oledb/features/filestream-support.md)  
 Descrive il supporto di OLE DB Driver per SQL Server della FILESTREAM avanzata.  
  
 [Supporto per nomi SPN nelle connessioni client](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Si illustra in che modo il supporto per i nomi SPN (nome dell'entità servizio) è stato esteso per consentire l'autenticazione reciproca in tutti i protocolli.  
  
 [Supporto per colonne di tipo sparse nel driver OLE DB per SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Descrive il supporto di OLE DB Driver per SQL Server delle colonne di tipo sparse.  
  
 [Miglioramenti relativi a data e ora](../../oledb/features/date-and-time-improvements.md)  
 Descrive il supporto aggiunto a OLE DB Driver per SQL Server dei tipi di dati di data e ora.  
  
 [Individuazione dei metadati](../../oledb/features/metadata-discovery.md)  
 Si illustrano i miglioramenti apportati all'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Supporto UTF-16 nel driver OLE DB per SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Si illustra una modifica nel comportamento introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Se si specifica un buffer a lunghezza fissa quando si esegue l'associazione di un risultato della colonna o di un parametro di output e se il carattere **wchar** scritto nel buffer prima del carattere di terminazione è un punto di codice surrogato elevato in una coppia di surrogati, nonché se il carattere **wchar** successivo è un punto di codice surrogato basso, nel driver OLE DB per SQL Server il punto di codice surrogato elevato non viene aggiunto al buffer.  
 
 [Supporto UTF-8 in OLE DB Driver for SQL Server](../../oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
 Descrive il supporto della codifica server UTF-8 e le indicazioni di configurazione che gli utenti devono tenere presenti quando vengono usati dati con codifica UTF-8.
  
 [Driver OLE DB per il supporto di SQL Server per il ripristino di emergenza a disponibilità elevata](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Illustra come configurare l'applicazione per sfruttare le funzionalità di ripristino di emergenza a disponibilità elevata aggiunte in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Illustra i miglioramenti apportati al driver OLE DB per SQL Server e alla traccia dei dati, che consente l'accesso alle informazioni di diagnostica nel buffer circolare e nel registro XEvents.  
  
 [Driver OLE DB per il supporto SQL Server per LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Descrive il supporto di OLE DB Driver per SQL Server di Local DB.  
  
 [Uso della stringa di connessione TransparentNetworkIPResolution](../../oledb/features/using-transparent-network-ip-resolution.md)  
 Descrive in che modo OLE DB Driver per SQL Server supporta la risoluzione dell'IP di rete trasparente in un cluster di failover.  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [Procedure relative a OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Installazione del driver OLE DB per SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
