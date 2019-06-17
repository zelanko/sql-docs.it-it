---
title: I dati di informazioni sulle differenze tra i tipi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8dcffcb15493c5f7587999a41fc2bdf545b377cd
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801952"
---
# <a name="understanding-data-type-differences"></a>Informazioni sulle differenze tra i tipi di dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Tra i tipi di dati del linguaggio di programmazione Java e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono riscontrabili alcune differenze. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consente di superare tali differenze tramite diversi tipi di conversioni.  

## <a name="character-types"></a>Tipi di caratteri

I tipi di dati stringa di caratteri JDBC sono **CHAR**, **VARCHAR**, e **LONGVARCHAR**. Il driver JDBC fornisce supporto per l'API di JDBC 4.0. In JDBC 4.0 i tipi di dati stringa di caratteri JDBC possono rivelarsi **NCHAR**, **NVARCHAR**, e **LONGNVARCHAR**. Questi nuovi tipi di stringhe di caratteri mantengono i tipi di caratteri nativi di Java in formato Unicode pertanto non richiedono più conversioni da ANSI a Unicode o viceversa.  
  
| Tipo            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A lunghezza fissa    | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char** e **nchar** eseguire il mapping di tipi di dati direttamente a Microsoft JDBC **CHAR** e **NCHAR** tipi. Si tratta di tipi a lunghezza fissa con spaziatura messi a disposizione dal server nel caso in cui la colonna presenti `SET ANSI_PADDING ON`. Il riempimento è sempre attivato per il tipo **nchar**, mentre per il tipo **char** il riempimento viene aggiunto dal driver JDBC nel caso in cui le colonne char del server non siano riempite con caratteri nulli.                                                                                                                                                                                                                                                                                                                                                                                      |
| A lunghezza variabile | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** e **nvarchar** tipi di cui è stato eseguito il mapping direttamente a Microsoft JDBC **VARCHAR** e **NVARCHAR** rispettivamente i tipi.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **testo** e **ntext** tipi di cui è stato eseguito il mapping a JDBC **LONGVARCHAR** e **LONGNVARCHAR** digitare, rispettivamente. Si tratta di tipi deprecati a partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario utilizzare i tipi di valori di grandi dimensioni, **varchar (max)** oppure **nvarchar (max)** alternativa.<br /><br /> Usare l'aggiornamento\<tipo Numeric > e [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) metodi avrà esito negativo con **testo** e **ntext** colonne del server. L'uso del metodo [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo di conversione dei caratteri specifico è invece supportato per le colonne del server di tipo **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipi di stringhe binarie

I tipi di stringa binaria JDBC sono **binario**, **VARBINARY**, e **LONGVARBINARY**.  
  
| Tipo            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A lunghezza fissa    | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binario** tipo viene mappato direttamente a Microsoft JDBC **BINARY** tipo. Si tratta di un tipo a lunghezza fissa con spaziatura messo a disposizione dal server nel caso in cui la colonna presenti SET ANSI_PADDING ON. La spaziatura viene aggiunta dal driver JDBC se mancante nelle colonne char del server.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** è di tipo JDBC **BINARY** tipo con lunghezza fissa di 8 byte. |
| A lunghezza variabile | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** tipo esegue il mapping a JDBC **VARBINARY** tipo.<br /><br /> Il **udt** digitare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping a JDBC come una **VARBINARY** tipo.                                                                                                                                                                                                                                 |
| Long            | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **immagine** tipo esegue il mapping a JDBC **LONGVARBINARY** tipo. Poiché si tratta di un tipo deprecato a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario usare un tipo valore di grandi dimensioni, **varbinary(max)** .                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipi di valori numerici esatti

Ai tipi di valori numerici esatti di JDBC viene eseguito il mapping direttamente ai tipi corrispondenti di SQL Server.  
  
| Tipo     | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | Il tipo **BIT** di JDBC rappresenta un singolo bit che può essere 0 o 1. Esegue il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** tipo.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | Il tipo **TINYINT** di JDBC rappresenta un singolo byte. Esegue il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** tipo.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | Il tipo **SMALLINT** di JDBC rappresenta un valore intero a 16 bit con segno. Esegue il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint** tipo.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | Il tipo **INTEGER** di JDBC rappresenta un valore intero a 32 bit con segno. Esegue il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** tipo.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | Il tipo **BIGINT** di JDBC rappresenta un valore intero a 64 bit con segno. Esegue il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint** tipo.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | Il tipo **NUMERIC** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori di precisione identica. Il **numerico** tipo è mappato al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numeric** tipo.                                                                                                                                                                                                                                                                   |
| DECIMAL  | Il tipo **DECIMAL** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori pari almeno alla precisione specificata. Il **decimale** tipo esegue il mapping per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimale** tipo.<br /><br /> Del tipo **DECIMAL** di JDBC viene anche eseguito il mapping ai tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** e **smallmoney**, che sono tipi decimali specifici a precisione fissa memorizzati, rispettivamente, in 8 e 4 byte. |
  
## <a name="approximate-numeric-types"></a>Tipi di valori numerici approssimati

I tipi numerici approssimati di JDBC sono **reali**, **DOUBLE**, e **FLOAT**.  
  
| Tipo   | Descrizione                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | Il tipo **REAL** di JDBC presenta sette cifre di precisione (precisione singola). Ne viene eseguito il mapping direttamente al tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | Il tipo **DOUBLE** di JDBC presenta 15 cifre di precisione (precisione doppia). Ne viene eseguito il mapping al tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**float**. Microsoft JDBC **FLOAT** tipo è un sinonimo di **DOPPIE**. Poiché può esserci confusione tra **FLOAT** e **DOUBLE**, **DOUBLE** preferito. |
  
## <a name="datetime-types"></a>Tipi datetime

Microsoft JDBC **TIMESTAMP** esegue il mapping di tipo per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** e **smalldatetime** tipi. Il tipo **datetime** viene memorizzato in due valori interi a 4 byte. Il tipo **smalldatetime** contiene le stesse informazioni (data e ora), ma, essendo memorizzato in due valori small integer a 2 byte, garantisce una precisione inferiore.  
  
> [!NOTE]  
> Il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** è un tipo stringa binario a lunghezza fissa. Non esegue il mapping a uno dei tipi di fase JDBC: **data**, **ora**, o **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Mapping personalizzato dei tipi

La caratteristica del mapping personalizzato dei tipi di JDBC, che usa le interfacce SQLData per i tipi avanzati di JDBC (UDT, Struct e così via), non è implementata nel driver JDBC.  
  
## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
