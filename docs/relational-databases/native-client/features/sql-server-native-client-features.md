---
title: Funzionalità di SQL Server Native Client | Documenti di Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2bf0766c2a9d90bc49189b4e99b208173709669e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62744403"
---
# <a name="sql-server-native-client-features"></a>Funzionalità di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Oltre a esporre le funzionalità di Windows (in precedenza Microsoft) Data Access Components (WDAC), in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono implementate anche molte altre funzionalità che consentono di esporre le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>In questa sezione  
 [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Viene descritta una modifica del comportamento a partire da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Uso del mirroring del database](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Viene descritto come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta l'utilizzo di database con mirroring, ovvero la possibilità di mantenere una copia, o mirror, di un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database su un server di standby.  
  
 [Esecuzione di operazioni asincrone](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta le operazioni asincrone, ovvero la capacità di restituzione immediata senza blocchi sul thread chiamante.  
  
 [Uso di MARS &#40;Multiple Active Result Set&#41;](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la funzionalità MARS (Multiple Active Result Set) che consente di eseguire e ricevere più set di risultati utilizzando una sola connessione al database.  
  
 [Uso di tipi di dati XML](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta i dati XML, ovvero un tipo di dati basato su XML che è possibile utilizzare come tipo di colonna, tipo di variabile, tipo di parametro o tipo restituito dalla funzione.  
  
 [Uso dei tipi definiti dall'utente](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Viene descritto come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta User-Defined tipi (UDT), che estende il sistema di tipo SQL, consentendo di archiviare gli oggetti e strutture di dati personalizzati in un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database.  
  
 [Uso di tipi valore di grandi dimensioni](../../../relational-databases/native-client/features/using-large-value-types.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta i tipi di dati per valori di grandi dimensioni, ovvero i tipi di dati LOB (Large Object).  
  
 [Modifica delle password a livello di codice](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la gestione delle password scadute per consentirne la modifica sul client senza il coinvolgimento dell'amministratore.  
  
 [Uso dell'isolamento dello snapshot](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta il miglioramento del controllo delle versioni delle righe che comporta a sua volta un miglioramento delle prestazioni del database evitando le situazioni di blocco in lettura/scrittura.  
  
 [Uso delle notifiche delle query](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la notifica di tipo consumer per la modifica dei set di righe.  
  
 [Esecuzione di operazioni di copia bulk](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Viene descritto come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta operazioni di copia di massa che consentono il trasferimento di grandi quantità di dati all'interno o all'esterno di un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabella o vista.  
  
 [Uso della crittografia senza convalida](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 Si illustra l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per crittografare i dati inviati al server senza convalidare il certificato.  
  
 [I parametri con valori di tabella &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 Si illustra il supporto di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per i parametri con valori di tabella.  
  
 [Tipi CLR definiti dall'utente di grandi dimensioni](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 Si illustra il supporto dei tipi CRL definiti dall'utente di grandi dimensioni.  
  
 [Supporto FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md)  
 Viene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il supporto Client nativo per la funzionalità FILESTREAM avanzata.  
  
 [Supporto per nomi SPN nelle connessioni client](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 Si illustra in che modo il supporto per i nomi SPN (nome dell'entità servizio) è stato esteso per consentire l'autenticazione reciproca in tutti i protocolli.  
  
 [Supporto di colonne di tipo sparse in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 Si illustra il supporto delle colonne di tipo sparse da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 [Miglioramenti relativi a data e ora](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 Si illustra il supporto aggiunto a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per i tipi di dati di data e ora.  
  
 [Individuazione dei metadati](../../../relational-databases/native-client/features/metadata-discovery.md)  
 Si illustrano i miglioramenti apportati all'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Supporto di UTF-16 in SQL Server Native Client 11.0](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 Si illustra una modifica nel comportamento introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Se si fornisce un buffer di lunghezza fissa quando si associa un parametro di output o dei risultati di colonna e se la **wchar** caratteri scritti nel buffer prima che il carattere di terminazione è un punto di codice surrogato alto di una coppia di surrogati e la successiva **wchar** carattere rappresenta un punto di codice surrogato basso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non aggiungerà il punto di codice surrogato nel buffer.  
  
 [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Illustra come configurare l'applicazione per sfruttare le funzionalità di ripristino di emergenza a disponibilità elevata aggiunte in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Si illustrano i miglioramenti apportati a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e alla traccia dei dati che consente l'accesso alle informazioni di diagnostica nel buffer circolare e nel registro XEvents.  
  
 [Supporto di SQL Server Native Client per Local DB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 Si illustra il supporto della funzionalità del database locale da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Procedure relative a ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Procedure relative a OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Installazione di SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
