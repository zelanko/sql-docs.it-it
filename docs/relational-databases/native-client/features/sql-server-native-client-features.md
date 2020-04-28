---
title: Funzionalità
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e10bc2259c8e283a97db89a85940377e50aef3da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388441"
---
# <a name="sql-server-native-client-features"></a>Funzionalità di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Oltre a esporre le funzionalità di Windows (in precedenza Microsoft) Data Access Components (WDAC), in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono implementate anche molte altre funzionalità che consentono di esporre le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Viene descritta una modifica del comportamento a partire da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Utilizzo del mirroring del database](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Viene illustrato [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il modo in cui Native Client supporta l'utilizzo di database con mirroring, ovvero la possibilità di gestire una copia, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mirror, di un database in un server di standby.  
  
 [Esecuzione di operazioni asincrone](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta le operazioni asincrone, ovvero la capacità di restituzione immediata senza blocchi sul thread chiamante.  
  
 [Uso di MARS &#40;Multiple Active Result Set&#41;](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la funzionalità MARS (Multiple Active Result Set) che consente di eseguire e ricevere più set di risultati utilizzando una sola connessione al database.  
  
 [Utilizzo di tipi di dati XML](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta i dati XML, ovvero un tipo di dati basato su XML che è possibile utilizzare come tipo di colonna, tipo di variabile, tipo di parametro o tipo restituito dalla funzione.  
  
 [Utilizzo dei tipi definiti dall'utente (UDT)](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Viene descritto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in che modo Native Client supporta i tipi definiti dall'utente (UDT), che estende il sistema di tipi SQL consentendo di archiviare oggetti e strutture [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di dati personalizzate in un database di.  
  
 [Utilizzo di tipi di dati per valori di grandi dimensioni](../../../relational-databases/native-client/features/using-large-value-types.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta i tipi di dati per valori di grandi dimensioni, ovvero i tipi di dati LOB (Large Object).  
  
 [Modifica delle password a livello di programmazione](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la gestione delle password scadute per consentirne la modifica sul client senza il coinvolgimento dell'amministratore.  
  
 [Utilizzo dell'isolamento dello snapshot](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta il miglioramento del controllo delle versioni delle righe che comporta a sua volta un miglioramento delle prestazioni del database evitando le situazioni di blocco in lettura/scrittura.  
  
 [Utilizzo delle notifiche delle query](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 Si illustra in che modo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la notifica di tipo consumer per la modifica dei set di righe.  
  
 [Esecuzione di operazioni di copia bulk](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Viene descritto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in che modo Native Client supporta operazioni di copia bulk che consentono il trasferimento di grandi quantità di dati all' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] interno o all'esterno di una tabella o vista.  
  
 [Uso della crittografia senza convalida](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 Si illustra l'utilizzo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per crittografare i dati inviati al server senza convalidare il certificato.  
  
 [Parametri con valori di tabella &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 Si illustra il supporto di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per i parametri con valori di tabella.  
  
 [Tipi CLR definiti dall'utente di grandi dimensioni](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 Si illustra il supporto dei tipi CRL definiti dall'utente di grandi dimensioni.  
  
 [Supporto FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md)  
 Viene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] illustrato il supporto di Native Client per la funzionalità FILESTREAM avanzata.  
  
 [Supporto per nomi SPN nelle connessioni client](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 Si illustra in che modo il supporto per i nomi SPN (nome dell'entità servizio) è stato esteso per consentire l'autenticazione reciproca in tutti i protocolli.  
  
 [Supporto per colonne di tipo sparse in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 Si illustra il supporto delle colonne di tipo sparse da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 [Miglioramenti relativi a data e ora](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 Si illustra il supporto aggiunto a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per i tipi di dati di data e ora.  
  
 [Individuazione dei metadati](../../../relational-databases/native-client/features/metadata-discovery.md)  
 Si illustrano i miglioramenti apportati all'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Supporto per UTF-16 in SQL Server Native Client 11.0](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 Si illustra una modifica nel comportamento introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Se si fornisce un buffer a lunghezza fissa quando si associa un risultato della colonna o un parametro di output e se il carattere **WCHAR** scritto nel buffer prima del carattere di terminazione è un punto di codice surrogato alto di una coppia di surrogati e il carattere **WCHAR** successivo è [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] un punto di codice surrogato basso, Native client non aggiungerà il punto di codice surrogato alto al buffer.  
  
 [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Illustra come configurare l'applicazione per sfruttare le funzionalità di ripristino di emergenza a disponibilità elevata aggiunte in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Accesso alle informazioni di diagnostica nel registro eventi estesi](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Si illustrano i miglioramenti apportati a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e alla traccia dei dati che consente l'accesso alle informazioni di diagnostica nel buffer circolare e nel registro XEvents.  
  
 [Supporto SQL Server Native Client per il database locale](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 Si illustra il supporto della funzionalità del database locale da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Procedure per ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Procedure per OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Installazione di SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
