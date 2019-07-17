---
title: Modifiche apportate alla copia di massa per avanzata tipi data e ora (OLE DB e ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 784917e29c0b0a407eb66006bb0e8798602722ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106117"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>Modifiche della copia bulk per i tipi di data e ora migliorati (OLE DB e ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In questo argomento vengono descritti i miglioramenti apportati ai tipi di data/ora per supportare la funzionalità di copia bulk. Le informazioni incluse in questo argomento sono valide sia per OLE DB sia per ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="format-files"></a>File di formato  
 Nella tabella seguente viene descritto l'input utilizzato per specificare i tipi di data/ora e i nomi dei tipi di dati del file host corrispondenti quando si compilano file di formato in modo interattivo.  
  
|tipo di archiviazione di file|Tipo di dati del file host|Risposta alla richiesta: "Specificare il tipo di archiviazione di file del campo < nome_campo > [\<predefinito >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|Datetime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|Date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 Il file XSD per i file di formato XML includerà le aggiunte seguenti:  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>File di dati di tipo carattere  
 Nei file di dati di tipo carattere, i valori di data e ora sono rappresentati come descritto nel "formati di dati: Sezione stringhe e valori letterali"di [supporto dei tipi di dati per ODBC Date e miglioramenti per la fase](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md) per ODBC o di [supporto dei tipi di dati per data OLE DB e miglioramenti per la fase](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) per OLE DB.  
  
 In file di dati nativi, i valori di data e ora per i quattro nuovi tipi vengono rappresentati come rispettive rappresentazioni TDS con una scala pari a 7 (poiché si tratta di al massimo supportato dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e file di dati bcp non archiviano la scala di tali colonne). Non è stata apportata alcuna modifica all'archiviazione dei tipi **datetime** e **smalldatetime** esistenti o delle rispettive rappresentazioni TDS.  
  
 Di seguito vengono indicate le dimensioni dello spazio di archiviazione per i diversi tipi di archiviazione per OLE DB:  
  
|tipo di archiviazione di file|Dimensioni dello spazio di archiviazione in byte|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 Di seguito vengono indicate le dimensioni per ODBC: Si noti che non è necessario archiviare la precisione in alcun file di formato o di dati, in quanto il file BCP.exe recupera sempre la precisione dal server.  
  
|tipo di archiviazione di file|Dimensioni dello spazio di archiviazione in byte|Formato di archiviazione|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>Tipi BCP in sqlncli.h  
 Di seguito vengono indicati i tipi definiti in sqlncli.h per l'utilizzo con le estensioni API BCP in ODBC. Questi tipi vengono passati con il *eUserDataType* parametro ibcpsession:: BCPColFmt in OLE DB.  
  
|tipo di archiviazione di file|Tipo di dati del file host|Tipo in SQLNCLI. h per l'uso con ibcpsession:: BCPColFmt|Value|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|Date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversioni dei tipi di dati BCP  
 Nelle tabelle seguenti vengono fornite informazioni sulla conversione.  
  
 **Nota per OLE DB** Le conversioni seguenti vengono eseguite da IBCPSession. IRowsetFastLoad utilizza conversioni OLE DB come definito in [conversioni eseguite da Client a Server](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md). Si noti che i valori datetime vengono arrotondati a 1/300 di secondo, mentre per i valori smalldatetime i secondi vengono impostati su zero in seguito all'esecuzione delle conversioni client descritte di seguito. L'arrotondamento dei valori datetime viene applicato a ore e minuti, ma non alla data.  
  
|A -><br /><br /> From|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|Date|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|N/D|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|Datetime|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1, 10 (ODBC) 1, 12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|char/wchar (date)|9|-|9, 6 (ODBC) 9, 6, 12 (OLE DB)|9, 6 (ODBC) 9, 6, 12 (OLE DB)|9,6|9,5,6|N/D|N/D|  
|char/wchar (time)|-|9,10|9, 7, 10 (ODBC) 9, 7, 10, 12 (OLE DB)|9, 7, 10 (ODBC) 9, 7, 10, 12 (OLE DB)|9,7,10|9,5,7,10|N/D|N/D|  
|char/wchar (datetime)|9,2|9,4,10|9, 10 (ODBC) 9, 10, 12 (OLE DB)|9, 10 (ODBC) 9, 10, 12 (OLE DB)|9,10|9,5,10|N/D|N/D|  
|char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9, 8, 10 (ODBC) 9, 8, 10, 12 (OLE DB)|9, 8, 10 (ODBC) 9, 8, 10, 12 (OLE DB)|9,8,10|9,10|N/D|N/D|  
  
#### <a name="key-to-symbols"></a>Descrizione dei simboli  
  
|Simbolo|Significato|  
|------------|-------------|  
|-|Non viene supportata alcuna conversione.<br /><br /> Viene generato un record di diagnostica ODBC con SQLSTATE 07006 e il messaggio "Violazione dell'attributo del tipo di dati".|  
|1|Se i dati specificati non sono validi, viene generato un record di diagnostica ODBC con SQLSTATE 22007 e il messaggio "Formato di datetime non valido". Per i valori datetimeoffset, la parte relativa all'ora deve essere compresa nell'intervallo supportato in seguito alla conversione in UTC, anche se non è necessaria alcuna conversione in UTC. Ciò è dovuto al fatto che TDS e il server in genere normalizzano l'ora nei valori datetimeoffset per UTC. Di conseguenza, il client deve verificare che i componenti relativi all'ora siano compresi nell'intervallo supportato in seguito alla conversione in UTC.|  
|2|Il componente relativo all'ora viene ignorato.|  
|3|Per ODBC, se si verifica un troncamento con perdita di dati, viene generato un record di diagnostica con SQLSTATE 22001 e il messaggio 'Stringa di dati, troncata a destra' il numero di cifre per i secondi frazionari (scala) è determinato dalle dimensioni della colonna di destinazione in base al Nella tabella seguente. Per dimensioni di colonna maggiori dell'intervallo specificato nella tabella, si presuppone una scala di 7. Questa conversione deve consentire fino a nove cifre per i secondi frazionari, il massimo consentito in ODBC.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Scala prevista 0** 8<br /><br /> **Scala 1..7 prevista** 10,16<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Scala prevista 0:** 19<br /><br /> **Scala prevista 1..7:** 21..27<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Scala prevista 0:** 26<br /><br /> **Scala prevista 1..7:** 28..34<br /><br /> Per OLE DB, se si verifica un troncamento con perdita di dati, viene inserito un errore. Per datetime2 il numero di cifre per i secondi frazionari, ovvero la scala, è determinato dalle dimensioni della colonna di destinazione in base alla tabella seguente. Per dimensioni di colonna maggiori dell'intervallo specificato nella tabella, si presuppone una scala 9. Questa conversione deve consentire fino a nove cifre per i secondi frazionari, il massimo consentito da OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Scala prevista 0** 8<br /><br /> **Scala prevista 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Scala prevista 0:** 19<br /><br /> **Scala prevista 1..9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Scala prevista 0:** 26<br /><br /> **Scala prevista 1..9:** 28..36|  
|4|Il componente relativo alla data viene ignorato.|  
|5|Il fuso orario è impostato su UTC, ad esempio 00:00.|  
|6|L'ora è impostata su zero.|  
|7|La data è impostata su 1900-01-01.|  
|8|La differenza di fuso orario viene ignorata.|  
|9|La stringa viene analizzata e convertita in un valore date, datetime, datetimeoffset o time a seconda del primo carattere di punteggiatura rilevato e della presenza degli altri componenti. La stringa viene quindi convertita nel tipo di destinazione, in base alle regole indicate nella tabella alla fine di questo argomento per il tipo di origine individuato dal processo. Se i dati forniti non possono essere analizzati senza errore o se qualsiasi componente è al di fuori dell'intervallo consentito o non vi è conversione dal tipo del valore letterale al tipo di destinazione, viene inserito un errore (OLE DB) o viene generato un record di diagnostica ODBC con SQLSTATE 22018 e il messaggio "Carattere non valido per la specifica del cast". Per i parametri datetime e smalldatetime, se l'anno non è compreso nell'intervallo supportato da questi tipi, viene inserito un errore (OLE DB) o viene generato un record di diagnostica con SQLSTATE 22007 e il messaggio "Formato di datetime non valido".<br /><br /> Per datetimeoffset, il valore deve essere compreso nell'intervallo supportato in seguito alla conversione in UTC, anche se non è necessaria alcuna conversione in UTC. Ciò è dovuto al fatto che TDS e il server normalizzano sempre l'ora in valori datetimeoffset per UTC. Il client deve pertanto verificare che i componenti relativi all'ora siano compresi nell'intervallo supportato in seguito alla conversione in UTC. Se il valore non è compreso nell'intervallo UTC supportato, viene inserito un errore (OLE DB) o viene generato un record di diagnostica con SQLSTATE 22007 e il messaggio "Formato di datetime non valido".|  
|10|Se si verifica un troncamento con perdita di dati in una conversione da client a server, viene inserito un errore (OLE DB) o viene generato un record di diagnostica ODBC con SQLSTATE 22008 e il messaggio "Overflow del campo Datetime". Questo errore si verifica anche se il valore non è incluso nell'intervallo che può essere rappresentato dall'intervallo UTC utilizzato dal server. Se si verifica un troncamento dei secondi o dei secondi frazionari in una conversione da server a client, viene generato solo un avviso.|  
|11|Se si verifica un troncamento con perdita di dati, viene generato un record di diagnostica.<br /><br /> In una conversione da server a client, il record è un avviso (ODBC SQLSTATE S1000).<br /><br /> In una conversione da client a server, il record è un errore (ODBC SQLSTATE 22001).|  
|12|I secondi vengono impostati su zero e i secondi frazionari vengono ignorati. Non è possibile alcun errore di troncamento.|  
|N/D|Viene mantenuto il comportamento di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni precedenti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Data e miglioramenti per la fase &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)   
 [Miglioramenti relativi a data e ora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
