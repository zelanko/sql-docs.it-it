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
ms.openlocfilehash: 46f7de1e57686a0f54368407580d90236152d147
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989053"
---
# <a name="ole-db-driver-for-sql-server-features"></a>Funzionalità del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Oltre a esporre le funzionalità di Windows (in precedenza Microsoft) Data Access Components (WDAC), il driver OLE DB per SQL Server implementa anche molte altre funzionalità che consentono di esporre le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione    
 [Uso del mirroring del database](../../oledb/features/using-database-mirroring.md)  
 Viene descritto in che modo il driver OLE DB per SQL Server supporta l'uso di database con mirroring, cioè la capacità di mantenere una copia, o mirror, di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un server di standby.  
  
 [Esecuzione di operazioni asincrone](../../oledb/features/performing-asynchronous-operations.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta le operazioni asincrone, ovvero la capacità di restituzione immediata senza blocchi sul thread chiamante.  

[Uso di Azure Active Directory](using-azure-active-directory.md)  
Vengono illustrati i nuovi metodi di autenticazione introdotti in OLE DB driver 18.2.1 che hanno impostazioni predefinite più sicure e consentono la connessione a un'istanza del database SQL di Azure usando un'identità federata.

 [Uso di MARS &#40;Multiple Active Result Set&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Viene illustrato il modo in cui OLE DB driver per SQL Server supporta MARS (Multiple Active Result Sets). che consente di eseguire e ricevere più set di risultati utilizzando una sola connessione al database.  
  
 [Uso di tipi di dati XML](../../oledb/features/using-xml-data-types.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta i dati XML, ovvero un tipo di dati basato su XML che è possibile usare come tipo di colonna, tipo di variabile, tipo di parametro o tipo restituito dalla funzione.  
  
 [Uso dei tipi definiti dall'utente](../../oledb/features/using-user-defined-types.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta i tipi definiti dall'utente (UDT) che estendono il sistema dei tipi SQL consentendo di archiviare oggetti e strutture dei dati personalizzate in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Uso di tipi valore di grandi dimensioni](../../oledb/features/using-large-value-types.md)  
 Viene illustrato il modo in cui OLE DB driver per SQL Server supporta i tipi di dati con valori di grandi dimensioni, che sono tipi di dati LOB (Large Object).  
  
 [Modifica delle password a livello di codice](../../oledb/features/changing-passwords-programmatically.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta la gestione delle password scadute per consentirne la modifica sul client senza il coinvolgimento dell'amministratore.  
  
 [Uso dell'isolamento dello snapshot](../../oledb/features/working-with-snapshot-isolation.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta il miglioramento del controllo delle versioni delle righe che comporta a sua volta un miglioramento delle prestazioni del database evitando le situazioni di blocco in lettura/scrittura.  
  
 [Uso delle notifiche delle query](../../oledb/features/working-with-query-notifications.md)  
 Viene illustrato il modo in cui OLE DB driver per SQL Server supporta la notifica del consumer per la modifica dei set  
  
 [Esecuzione di operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md)  
 Si illustra in che modo il driver OLE DB per SQL Server supporta operazioni di copia bulk che consentono il trasferimento di grandi quantità di dati all'interno o all'esterno di una tabella o vista di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Uso della crittografia senza convalida](../../oledb/features/using-encryption-without-validation.md)  
 Viene illustrato come utilizzare OLE DB driver per SQL Server per crittografare i dati inviati al server senza convalidare il certificato.  
  
 [Parametri con valori di tabella &#40;driver OLE DB per SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Viene illustrato OLE DB driver per SQL Server supporto per i parametri con valori di tabella.  
  
 [Tipi CLR definiti dall'utente di grandi dimensioni](../../oledb/features/large-clr-user-defined-types.md)  
 Si illustra il supporto dei tipi CRL definiti dall'utente di grandi dimensioni.  
  
 [Supporto FILESTREAM](../../oledb/features/filestream-support.md)  
 Viene illustrato OLE DB driver per SQL Server supporto per la funzionalità FILESTREAM avanzata.  
  
 [Supporto per nomi SPN nelle connessioni client](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Si illustra in che modo il supporto per i nomi SPN (nome dell'entità servizio) è stato esteso per consentire l'autenticazione reciproca in tutti i protocolli.  
  
 [Supporto per colonne di tipo sparse nel driver OLE DB per SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Viene illustrato OLE DB driver per il supporto SQL Server per le colonne di tipo sparse.  
  
 [Miglioramenti relativi a data e ora](../../oledb/features/date-and-time-improvements.md)  
 Viene illustrato il supporto aggiunto al driver OLE DB per SQL Server per i tipi di dati di data e ora.  
  
 [Individuazione dei metadati](../../oledb/features/metadata-discovery.md)  
 Si illustrano i miglioramenti apportati all'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Supporto UTF-16 nel driver OLE DB per SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Si illustra una modifica nel comportamento introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Se si specifica un buffer a lunghezza fissa quando si esegue l'associazione di un risultato della colonna o di un parametro di output e se il carattere **wchar** scritto nel buffer prima del carattere di terminazione è un punto di codice surrogato elevato in una coppia di surrogati, nonché se il carattere **wchar** successivo è un punto di codice surrogato basso, nel driver OLE DB per SQL Server il punto di codice surrogato elevato non viene aggiunto al buffer.  
 
 [Supporto UTF-8 in OLE DB Driver for SQL Server](../../oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
 Viene illustrato il supporto per la codifica UTF-8 e le precauzioni di configurazione che gli utenti devono eseguire quando si utilizzano dati con codifica UTF-8.
  
 [Driver OLE DB per il supporto di SQL Server per il ripristino di emergenza a disponibilità elevata](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Illustra come configurare l'applicazione per sfruttare le funzionalità di ripristino di emergenza a disponibilità elevata aggiunte in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Illustra i miglioramenti apportati al driver OLE DB per SQL Server e alla traccia dei dati, che consente l'accesso alle informazioni di diagnostica nel buffer circolare e nel registro XEvents.  
  
 [Driver OLE DB per il supporto SQL Server per LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Viene illustrato OLE DB driver per il supporto SQL Server per la funzionalità del database locale.  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per SQL Server](../../oledb/oledb-driver-for-sql-server.md)      
 [Procedure relative a OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Installazione del driver OLE DB per SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
