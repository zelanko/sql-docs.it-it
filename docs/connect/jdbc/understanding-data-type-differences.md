---
title: Informazioni sulle differenze tra i tipi di dati | Microsoft Docs
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
ms.openlocfilehash: 0cec994768fb5c3a49257da0fb310937c79c25b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004169"
---
# <a name="understanding-data-type-differences"></a>Informazioni sulle differenze tra i tipi di dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Tra i tipi di dati del linguaggio di programmazione Java e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono riscontrabili alcune differenze. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consente di superare tali differenze tramite diversi tipi di conversioni.  

## <a name="character-types"></a>Tipi di caratteri

I tipi di dati stringa di caratteri JDBC sono **char**, **varchar**e **LONGVARCHAR**. Il driver JDBC fornisce supporto per l'API di JDBC 4.0. In JDBC 4,0 i tipi di dati stringa di caratteri JDBC possono essere anche **nchar**, **nvarchar**e **LONGNVARCHAR**. Questi nuovi tipi di stringhe di caratteri mantengono i tipi di caratteri nativi di Java in formato Unicode pertanto non richiedono più conversioni da ANSI a Unicode o viceversa.  
  
| Tipo            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A lunghezza fissa    | I [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati **char** e **nchar** vengono mappati direttamente ai tipi JDBC **char** e **nchar** . Si tratta di tipi a lunghezza fissa con spaziatura messi a disposizione dal server nel caso in cui la colonna presenti `SET ANSI_PADDING ON`. Il riempimento è sempre attivato per il tipo **nchar**, mentre per il tipo **char** il riempimento viene aggiunto dal driver JDBC nel caso in cui le colonne char del server non siano riempite con caratteri nulli.                                                                                                                                                                                                                                                                                                                                                                                      |
| A lunghezza variabile | I [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi **varchar** e **nvarchar** vengono mappati direttamente ai tipi JDBC **varchar** e **nvarchar** , rispettivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Long            | I [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi **Text** e **ntext** vengono mappati rispettivamente al tipo JDBC **LONGVARCHAR** e **LONGNVARCHAR** . Si tratta di tipi deprecati a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partire da, quindi è consigliabile utilizzare tipi di valore di grandi dimensioni, **varchar (max)** o **nvarchar (max)** .<br /><br /> L'utilizzo dei\<metodi Update numeric Type > e [UpdateObject (int, Java. lang. Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) avrà esito negativo sulle colonne del server **Text** e **ntext** . L'uso del metodo [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo di conversione dei caratteri specifico è invece supportato per le colonne del server di tipo **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipi di stringhe binarie

I tipi di stringa binaria JDBC sono **Binary**, **varbinary**e **LONGVARBINARY**.  
  
| Tipo            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A lunghezza fissa    | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **binario** è associato direttamente al tipo **binario** JDBC. Si tratta di un tipo a lunghezza fissa con spaziatura messo a disposizione dal server nel caso in cui la colonna presenti SET ANSI_PADDING ON. La spaziatura viene aggiunta dal driver JDBC se mancante nelle colonne char del server.<br /><br /> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di **timestamp** è un tipo **binario** JDBC con lunghezza fissa di 8 byte. |
| A lunghezza variabile | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **varbinary** esegue il mapping al tipo **varbinary** di JDBC.<br /><br /> Il tipo **definito dall'utente** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il mapping a JDBC come tipo **varbinary** .                                                                                                                                                                                                                                 |
| Long            | Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di **immagine** viene mappato al tipo **LONGVARBINARY** di JDBC. Poiché si tratta di un tipo deprecato a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario usare un tipo valore di grandi dimensioni, **varbinary(max)** .                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipi di valori numerici esatti

Ai tipi di valori numerici esatti di JDBC viene eseguito il mapping direttamente ai tipi corrispondenti di SQL Server.  
  
| Tipo     | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | Il tipo **BIT** di JDBC rappresenta un singolo bit che può essere 0 o 1. Viene eseguito il mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo di **bit** .                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | Il tipo **TINYINT** di JDBC rappresenta un singolo byte. Viene eseguito il mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo **tinyint** .                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | Il tipo **SMALLINT** di JDBC rappresenta un valore intero a 16 bit con segno. Viene eseguito il mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo **smallint** .                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | Il tipo **INTEGER** di JDBC rappresenta un valore intero a 32 bit con segno. Viene eseguito il mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo **int** .                                                                                                                                                                                                                                                                                                                                           |
| bigint   | Il tipo **BIGINT** di JDBC rappresenta un valore intero a 64 bit con segno. Viene eseguito il mapping [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo **bigint** .                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | Il tipo **NUMERIC** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori di precisione identica. Il tipo **numerico** viene mappato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al tipo **numerico** .                                                                                                                                                                                                                                                                   |
| DECIMAL  | Il tipo **DECIMAL** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori pari almeno alla precisione specificata. Il tipo **Decimal** viene mappato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al tipo **decimale**.<br /><br /> Del tipo **DECIMAL** di JDBC viene anche eseguito il mapping ai tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** e **smallmoney**, che sono tipi decimali specifici a precisione fissa memorizzati, rispettivamente, in 8 e 4 byte. |
  
## <a name="approximate-numeric-types"></a>Tipi di valori numerici approssimati

I tipi numerici approssimati di JDBC sono **Real**, **Double**e **float**.  
  
| Tipo   | Descrizione                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | Il tipo **REAL** di JDBC presenta sette cifre di precisione (precisione singola). Ne viene eseguito il mapping direttamente al tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | Il tipo **DOUBLE** di JDBC presenta 15 cifre di precisione (precisione doppia). Ne viene eseguito il mapping al tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**float**. Il tipo **float** JDBC è un sinonimo di **Double**. Poiché può esserci confusione tra **float** e **Double**, è preferibile la **doppia** . |
  
## <a name="datetime-types"></a>Tipi datetime

Il tipo di **timestamp** JDBC viene mappato ai [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi **DateTime** e **smalldatetime** . Il tipo **datetime** viene memorizzato in due valori interi a 4 byte. Il tipo **smalldatetime** contiene le stesse informazioni (data e ora), ma, essendo memorizzato in due valori small integer a 2 byte, garantisce una precisione inferiore.  
  
> [!NOTE]  
> Il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** è un tipo stringa binario a lunghezza fissa. Non esegue il mapping a uno dei tipi di ora JDBC: **Data**, **ora**o **timestamp**.  
  
## <a name="custom-type-mapping"></a>Mapping personalizzato dei tipi

La caratteristica del mapping personalizzato dei tipi di JDBC, che usa le interfacce SQLData per i tipi avanzati di JDBC (UDT, Struct e così via), non è implementata nel driver JDBC.  
  
## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
