---
title: Allocare un Handle di connessione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63cb5aac5fda552be721ed80e85cda388015a5fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134241"
---
# <a name="allocating-a-connection-handle"></a>Allocazione di un handle di connessione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Prima che l'applicazione possa connettersi a un'origine dati o a un driver, è necessario che allochi un handle di connessione. Questa operazione viene eseguita chiamando **SQLAllocHandle** con il *HandleType* parametro impostato su SQL_HANDLE_DBC e *InputHandle* che punta a un handle di ambiente inizializzato.  
  
 Le caratteristiche della connessione vengono controllate mediante l'impostazione degli attributi di connessione. Poiché ad esempio le transazioni si verificano al livello della connessione, il livello di isolamento delle transazioni è un attributo di connessione. Allo stesso modo, il timeout di accesso, ovvero il numero di secondi di attesa durante il tentativo di connessione prima del timeout, è un attributo di connessione.  
  
 Gli attributi di connessione sono impostati con [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), e le relative impostazioni correnti vengono recuperate con [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md). Se **SQLSetConnectAttr** viene chiamato prima di tentata una connessione, gestione Driver ODBC archivia gli attributi nella relativa struttura della connessione e li imposta nel driver come parte del processo di connessione. Alcuni attributi di connessione devono essere impostati prima che l'applicazione tenti di connettersi, altri possono essere impostati al termine della connessione. SQL_ATTR_ODBC_CURSORS, ad esempio, deve essere impostato prima che venga stabilita una connessione, mentre SQL_ATTR_AUTOCOMMIT può essere impostato dopo la connessione.  
  
 È possibile migliorare le prestazioni delle applicazioni in esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0 o successiva reimpostando le dimensioni del pacchetto di rete TDS (Tabular Data Stream). Le dimensioni predefinite del pacchetto sono impostate nel server su 4 KB. Per ottenere le massime prestazioni le dimensioni del pacchetto devono essere in genere impostate su un valore compreso tra 4 e 8 KB. Se dal test si evince che con dimensioni diverse si possono ottenere prestazioni migliori, sarà possibile reimpostarle. Le applicazioni ODBC possono eseguire questa operazione prima della connessione chiamando **SQLSetConnectAttr** con l'opzione SQL_ATTR_PACKET_SIZE. Le prestazioni di alcune applicazioni migliorano con dimensioni del pacchetto superiori, ma i miglioramenti sono in genere minimi nel caso di dimensioni maggiori di 8 KB.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client ha un numero di attributi di connessione estesa che un'applicazione può utilizzare per aumentare la funzionalità. Alcuni di questi attributi controllano le stesse opzioni che possono essere specificate nelle origini dati e utilizzate per sostituire eventuali opzioni impostate in un'origine dati. Se ad esempio un'applicazione utilizza identificatori tra virgolette, può impostare l'attributo SQL_COPT_SS_QUOTED_IDENT specifico del driver su SQL_QI_ON per assicurarsi che questa opzione sia sempre impostata indipendentemente dall'impostazione presente in qualsiasi origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
