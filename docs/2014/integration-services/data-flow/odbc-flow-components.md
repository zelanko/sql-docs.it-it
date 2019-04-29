---
title: Componenti di flusso ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e42099ede229ef7d0b10cf8d88b4ac92c60d3370
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901431"
---
# <a name="odbc-flow-components"></a>Componenti di flusso ODBC
  In questo argomento vengono descritti i concetti necessari per la creazione di un flusso di dati ODBC tramite [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 Con il connettore per ODBC (Open Database Connectivity) di Attunity per [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] gli sviluppatori di SSIS possono creare in modo facile pacchetti per il caricamento e lo scaricamento di dati da database supportati da ODBC.  
  
 Il connettore ODBC è progettato per ottenere prestazioni ottimali per il caricamento o lo scaricamento dei dati in o da un database supportato da ODBC nel contesto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
## <a name="benefits"></a>Vantaggi  
 L'origine ODBC e la destinazione ODBC per [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] offrono un vantaggio competitivo per SSIS in progetti correlati al caricamento o allo scaricamento di dati in o da database supportati da ODBC.  
  
 Sia l'origine ODBC sia la destinazione ODBC consentono l'integrazione di dati a prestazioni elevate con database abilitati per ODBC. È possibile configurare entrambi i componenti per l'utilizzo con associazioni di matrici di parametri a livello di riga per provider ODBC con funzionalità di livello elevato che supportano questa modalità di associazione e associazioni di parametri di singole righe per provider ODBC con funzionalità di basso livello.  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>Introduzione all'origine e alla destinazione ODBC  
 Prima che sia possibile configurare pacchetti che utilizzano [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], è necessario assicurarsi che siano disponibili gli elementi seguenti.  
  
-   [Origine ODBC](odbc-source.md)  
  
-   [Destinazione ODBC](odbc-destination.md)  
  
 L'origine ODBC e la destinazione ODBC offrono un modo semplice per scaricare e caricare dati e trasferire dati da un database di origine supportato da ODBC a un database di destinazione supportato da ODBC.  
  
 Per utilizzare l'origine o la destinazione per caricare o scaricare dati, aprire un nuovo progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Trascinare quindi l'origine e la destinazione nell'area di progettazione di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Tramite il componente di origine ODBC viene eseguita la lettura dei dati dal database di origine supportato da ODBC.  
  
 È possibile connettere l'origine ODBC a qualsiasi destinazione o componente di trasformazione supportato da SSIS.  
  
 **Vedere anche:**  
  
 Origine ODBC  
  
 Editor origine ODBC (pagina Gestione connessione)  
  
 Editor origine ODBC (pagina Output degli errori)  
  
-   Tramite la destinazione ODBC vengono caricati dati in un database supportato da ODBC. È possibile connettere la destinazione a qualsiasi origine o componente di trasformazione supportato da SSIS.  
  
 **Vedere anche:**  
  
 Destinazione ODBC  
  
 Editor destinazione ODBC (pagina Gestione connessione)  
  
 Editor destinazione ODBC (pagina Output errori)  
  
## <a name="operating-scenarios"></a>Scenari operativi  
 In questa sezione vengono descritti alcuni degli utilizzi principali per i componenti di origine e di destinazione ODBC.  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>Copia bulk di dati da tabelle di SQL Server a qualsiasi tabella di database supportata da ODBC  
 È possibile usare i componenti per eseguire la copia bulk di dati da una o più tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'unica tabella di database supportata da ODBC.  
  
 Nell'esempio seguente viene illustrato come creare un'attività Flusso di dati SSIS per l'estrazione di dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il caricamento dei dati in una tabella DB2.  
  
-   Creare un progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Creare una gestione connessione OLE DB connessa al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che contiene i dati che si desidera copiare.  
  
-   Creare una gestione connessione ODBC che utilizza un driver ODBC DB2 installato localmente con un DSN che punta a un database DB2 locale o remoto. In questo database vengono caricati i dati dal database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Trascinare un'origine OLE DB nell'area di progettazione, quindi configurare l'origine per ottenere i dati dal database e dalla tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i dati che si intende estrarre. Utilizzare la gestione connessione OLE DB creata in precedenza.  
  
-   Trascinare una destinazione ODBC nell'area di progettazione, connettere l'output di origine alla destinazione ODBC, quindi configurare la destinazione per il caricamento dei dati nella tabella DB2 con i dati estratti dal database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilizzare la gestione connessione ODBC creata in precedenza.  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>Copia bulk di dati da tabelle di database supportate da ODBC a qualsiasi tabella di SQL Server  
 È possibile utilizzare i componenti per eseguire la copia bulk di dati da una o più tabelle di database supportate da ODBC a un'unica tabella di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Nell'esempio seguente viene illustrato come creare un'attività Flusso di dati SSIS per l'estrazione di dati da una tabella di database Sybase e il caricamento dei dati in una tabella di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Creare un progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   Creare una gestione connessione ODBC che utilizza un driver ODBC Sybase installato localmente con un DSN che punta a un database Sybase locale o remoto. In questo database vengono estratti i dati.  
  
-   Creare una gestione connessione OLE DB connessa al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera caricare i dati.  
  
-   Trascinare un'origine ODBC nell'area di progettazione, quindi configurare l'origine per ottenere i dati dalla tabella Sybase con i dati che si intende copiare. Utilizzare la gestione connessione ODBC creata in precedenza.  
  
-   Trascinare una destinazione OLE DB nella superficie di progettazione, connettere l'output di origine alla destinazione OLE DB, quindi configurare la destinazione per il caricamento dei dati nella tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i dati estratti dal database Sybase. Utilizzare la gestione connessione OLE DB creata in precedenza.  
  
## <a name="supported-data-types"></a>Tipi di dati supportati  
 I componenti SSIS di copia bulk ODBC supportano tutti i tipi di dati ODBC predefiniti e includono il supporto per oggetti di grandi dimensioni (CLOB e BLOB).  
  
I tipi di dati C estensibili non sono supportati, come descritto nelle specifiche di ODBC 3.8. La tabella seguente descrive quali tipi di dati SSIS vengono usati per ogni tipo SQL ODBC. Uno sviluppatore di SSIS può eseguire l'override del mapping predefinito e specificare un tipo di dati SSIS diverso per le colonne di input/output senza influire sulle prestazioni per le conversioni di dati necessarie.  
  
|Tipo SQL ODBC|Tipo di dati SSIS|Commenti|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|Viene eseguito il mapping dei tipi di dati SQL a tipi SSIS Unsigned (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando tramite il driver ODBC viene impostato UNSIGNED_ATTRIBUTE su SQL_TRUE per il tipo di dati SQL.|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|Viene eseguito il mapping dei tipi di dati SQL a tipi SSIS Unsigned (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando tramite il driver ODBC viene impostato UNSIGNED_ATTRIBUTE su SQL_TRUE per il tipo di dati SQL.|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|Viene eseguito il mapping dei tipi di dati SQL a tipi SSIS Unsigned (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando tramite il driver ODBC viene impostato UNSIGNED_ATTRIBUTE su SQL_TRUE per il tipo di dati SQL.|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|Viene eseguito il mapping dei tipi di dati SQL a tipi SSIS Unsigned (DT_UI1, DT_UI2, DT_UI4, DT_UI8) quando tramite il driver ODBC viene impostato UNSIGNED_ATTRIBUTE su SQL_TRUE per il tipo di dati SQL.|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)<br /><br />DT_R8<br /><br />DT_CY|Viene mappato il tipo di dati numeric a DT_NUMERIC quando P è maggiore o uguale a 38 e S è maggiore o uguale a 0 e minore o uguale a P. Viene mappato il tipo di dati numeric a DT_R8 quando viene soddisfatta almeno una delle operazioni seguenti:<br /><br />La precisione è maggiore di 38<br /><br />La scala è minore di zero<br /><br />La scala è maggiore di 38<br /><br />La scala è maggiore della precisione<br /><br /><br /><br />Si noti che viene mappato il tipo di dati numeric a DT_CY quando viene dichiarato come tipo di dati money.|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)<br /><br />DT_R8<br /><br />DT_CY|Viene mappato il tipo di dati decimal a DT_NUMERIC quando P è maggiore o uguale a 38 e S è maggiore o uguale a 0 e minore o uguale a P. Viene mappato il tipo di dati decimal a DT_R8 quando viene soddisfatta almeno una delle operazioni seguenti:<br /><br />La precisione è maggiore di 38<br /><br />La scala è minore di zero<br /><br />La scala è maggiore di 38<br /><br />La scala è maggiore della precisione<br /><br />Si noti che viene mappato il tipo di dati decimal a DT_CY quando viene dichiarato come tipo di dati money.|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|Viene eseguito il mapping dei tipi di dati SQL_TIMESTAMP a DT_DBTIMESTAMP2 se la scala è maggiore di 3. In tutti gli altri casi, viene eseguito il mapping dei tipi di dati a DT_DBTIMESTAMP.|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|DT_STR viene usato se la lunghezza di colonna è minore o uguale a 8000 e la proprietà **ExposeStringsAsUnicode** è false.<br /><br />DT_WSTR viene usato se la lunghezza di colonna è minore o uguale a 8000 e la proprietà **ExposeStringsAsUnicode** è true.<br /><br />DT_TEXT viene usato se la lunghezza di colonna è maggiore di 8000 e la proprietà **ExposeStringsAsUnicode** è false.<br /><br />DT_NTEXT viene usato se la lunghezza di colonna è maggiore di 8000 e la proprietà **ExposeStringsAsUnicode** è true.|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|DT_NTEXT viene usato se la proprietà **ExposeStringsAsUnicode** è true.|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|DT_WSTR viene utilizzato se la lunghezza di colonna è minore o uguale a 4000.<br /><br />DT_NTEXT viene utilizzato se la lunghezza di colonna è maggiore di 4000.|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|DT_BYTES viene utilizzato se la lunghezza di colonna è minore o uguale a 8000.<br /><br />DT_IMAGE viene utilizzato se la lunghezza di colonna è maggiore di 8000.|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|Tipi di dati specifici del provider|DT_BYTES<br /><br />DT_IMAGE|DT_BYTES viene utilizzato se la lunghezza di colonna è minore o uguale a 8000.<br /><br />DT_IMAGE viene utilizzato se la lunghezza di colonna è uguale a zero o maggiore di 8000.|  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Origine ODBC](odbc-source.md)  
  
-   [Destinazione ODBC](odbc-destination.md)  
  
 
