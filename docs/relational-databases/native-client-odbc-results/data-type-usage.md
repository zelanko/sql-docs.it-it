---
title: Utilizzo del tipo di dati Documenti Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0384857c53e898af9fca89bb2ee2351f0b65f986
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297857"
---
# <a name="data-type-usage"></a>Utilizzo del tipo di dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e imporre il seguente utilizzo dei tipi di dati.  
  
|Tipo di dati|Limitazione|  
|---------------|----------------|  
|Valori letterali data|I valori letterali di data,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se archiviati in una colonna SQL_TYPE_TIMESTAMP ( tipi di dati **datetime** o **smalldatetime**), hanno un valore di ora di 12:00:00.000 A.M.|  
|**soldi** e **piccolisoldi**|Solo le parti intere dei tipi di dati **money** e **smallmoney** sono significative. Se la parte decimale dei dati **di SQL** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] money viene troncata durante la conversione del tipo di dati, il driver ODBC Native Client restituisce un avviso, non un errore.|  
|SQL_BINARY (ammette valori Null)|Quando viene eseguita una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 6.0 e precedente, se una colonna SQL_BINARY ammette valori Null, i dati archiviati nell'origine dati non possono essere riempiti di zeri. Quando vengono recuperati i dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tale colonna, il driver ODBC Native Client lo riempie con zeri a destra. Nei dati che vengono creati in operazioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio la concatenazione, tale riempimento non viene eseguito.<br /><br /> Quando inoltre i dati vengono posizionati in una colonna di questo tipo in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 o versione precedente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tronca i dati a destra, se non entrano nella colonna.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client supporta la connessione a 6.5 e versioni precedenti.|  
|SQL_CHAR (troncamento)|Quando si esegue la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 e versione precedente e i dati vengono inseriti in una colonna SQL_CHAR, se i dati non entrano nella colonna, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] li tronca a destra senza visualizzare alcun avviso.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client supporta la connessione a 6.5 e versioni precedenti.|  
|SQL_CHAR (ammette valori Null)|Quando viene eseguita una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 6.0 e precedente, se una colonna SQL_CHAR ammette valori Null, i dati archiviati nell'origine dati non possono essere riempiti con spazi. Quando vengono recuperati i dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tale colonna, il driver ODBC Native Client lo riempie con spazi vuoti a destra. Nei dati che vengono creati in operazioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio la concatenazione, tale riempimento non viene eseguito.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client supporta la connessione a 6.5 e versioni precedenti.|  
|SQL_LONGVARBINARY, SQL_LONGVARCHAR, SQL_WLONGVARCHAR|Gli aggiornamenti delle colonne con tipi di dati SQL_LONGVARBINARY, SQL_LONGVARCHAR o SQL_WLONGVARCHAR (utilizzando una clausola WHERE) che interessano più righe sono completamente supportati quando si è connessi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6. *x* e versioni successive. Quando si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessi a un'istanza di 4.2*x*, viene visualizzato un errore S1000, "Inserimento/aggiornamento parziale. L'inserimento o l'aggiornamento del testo o delle colonne di immagini non è stato completato", se l'aggiornamento riguarda più di una riga.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client supporta la connessione a 6.5 e versioni precedenti.|  
|Parametri delle funzioni per i valori stringa|*string_exp* parametri alle funzioni stringa devono essere di tipo SQL_CHAR o SQL_VARCHAR di dati. I tipi di dati SQL_LONG_VARCHAR non sono supportati nelle funzioni per i valori stringa. Il parametro *count* deve essere minore o uguale a 8.000 perché i SQL_CHAR e SQL_VARCHAR i tipi di dati sono limitati a una lunghezza massima di 8.000 caratteri.|  
|Valori letterali ora|I valori letterali di data[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ora, se archiviati in una colonna SQL_TIMESTAMP ( tipi di dati **datetime** o **smalldatetime**), hanno un valore di data 1 gennaio 1900.|  
|**Timestamp**|Solo un valore NULL può essere inserito manualmente in una colonna **timestamp.** Tuttavia, **timestamp**poiché le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]colonne timestamp vengono aggiornate automaticamente da , un valore NULL viene sovrascritto.|  
|**Tinyint**|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati **tinyint** è senza segno. Una colonna **tinyint** è associata a una variabile di tipo SQL_C_UTINYINT per impostazione predefinita.|  
|Tipi di dati alias|Quando si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessi a un'istanza di 4.2*x*, il driver ODBC aggiunge NULL a una definizione di colonna che non dichiara in modo esplicito il supporto di valori Null di una colonna. Per questo motivo, il supporto di valori Null che viene archiviato nella definizione di un tipo di dati alias viene ignorato.<br /><br /> Quando si è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connessi a un'istanza di 4.2*x*, le colonne con un tipo di dati alias con un tipo di dati di base **char** o **binary** e per le quali non viene dichiarato alcun supporto di valori Null vengono create come tipo di dati **varchar** o **varbinary**. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)e [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) restituiscono SQL_VARCHAR o SQL_VARBINARY come tipo di dati per queste colonne. Ai dati recuperati da queste colonne non viene applicato il riempimento.<br /><br /> Nota: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client supporta la connessione a 6.5 e versioni precedenti.|  
|Tipi di dati LONG|I parametri *data-at-execution* sono limitati per i tipi di dati SQL_LONGVARBINARY e SQL_LONGVARCHAR.|  
|Tipi per valori di grandi dimensioni|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client esporrà i tipi **varchar(max),** **varbinary(max)** e **nvarchar(max)** come SQL_VARCHAR, SQL_VARBINARY e SQL_WVARCHAR (rispettivamente) nelle API che accettano o restituiscono tipi di dati SQL ODBC.|  
|Tipo definito dall'utente (UDT)|Le colonne con tipo definito dall'utente vengono mappate come SQL_SS_UDT. Se una colonna con tipo definito dall'utente viene mappata in modo esplicito a un altro tipo nell'istruzione SQL mediante i metodi ToString() o ToXMLString() del tipo definito dall'utente oppure mediante le funzioni CAST/CONVERT, il tipo di colonna nel set di risultati rifletterà il tipo effettivo nel quale è stata convertita la colonna.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client può essere associato solo a una colonna UDT come binario. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta solamente la conversione tra i tipi di dati SQL_SS_UDT e SQL_C_BINARY.|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]convertirà automaticamente XML in testo Unicode. Il tipo XML viene mappato come SQL_SS_XML.|  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione dei risultati &#40;&#41;ODBCProcessing Results &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
