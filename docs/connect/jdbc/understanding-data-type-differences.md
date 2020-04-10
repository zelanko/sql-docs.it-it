---
title: Informazioni sulle differenze tra i tipi di dati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 623a665e0292e67d9f38b3fbc7203427a0cad544
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921219"
---
# <a name="understanding-data-type-differences"></a>Informazioni sulle differenze tra i tipi di dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Tra i tipi di dati del linguaggio di programmazione Java e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono riscontrabili alcune differenze. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] consente di superare tali differenze tramite diversi tipi di conversioni.  

## <a name="character-types"></a>Tipi di caratteri

I tipi di dati della stringa di caratteri JDBC sono **CHAR**, **VARCHAR** e **LONGVARCHAR**. Il driver JDBC fornisce supporto per l'API di JDBC 4.0. In JDBC 4.0 i tipi di dati della stringa di caratteri JDBC possono essere anche **NCHAR**, **NVARCHAR** e **LONGNVARCHAR**. Questi nuovi tipi di stringhe di caratteri mantengono i tipi di caratteri nativi di Java in formato Unicode pertanto non richiedono più conversioni da ANSI a Unicode o viceversa.  
  
| Type            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A lunghezza fissa    | I tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char** e **nchar** vengono mappati direttamente ai tipi JDBC **CHAR** e **NCHAR**. Si tratta di tipi a lunghezza fissa con spaziatura messi a disposizione dal server nel caso in cui la colonna presenti `SET ANSI_PADDING ON`. Il riempimento è sempre attivato per il tipo **nchar**, mentre per il tipo **char** il riempimento viene aggiunto dal driver JDBC nel caso in cui le colonne char del server non siano riempite con caratteri nulli.                                                                                                                                                                                                                                                                                                                                                                                      |
| A lunghezza variabile | I tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** e **nvarchar** vengono mappati direttamente ai tipi JDBC **VARCHAR** e **NVARCHAR**, rispettivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| long            | I tipi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text** e **ntext** vengono mappati rispettivamente ai tipi JDBC **LONGVARCHAR** e **LONGNVARCHAR**. Poiché si tratta di tipi deprecati a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario usare al loro posto i tipi per valori di grandi dimensioni, **varchar(max)** o **nvarchar(max)** .<br /><br /> Non è possibile usare i metodi update\<Tipo numerico> e [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) per le colonne del server **text** e **ntext**. L'uso del metodo [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) con un tipo di conversione dei caratteri specifico è invece supportato per le colonne del server di tipo **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipi di stringhe binarie

I tipi per stringa binaria JDBC sono **BINARY**, **VARBINARY** e **LONGVARBINARY**.  
  
| Type            | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A lunghezza fissa    | Il tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary** viene mappato direttamente al tipo JDBC **BINARY**. Si tratta di un tipo a lunghezza fissa con spaziatura messo a disposizione dal server nel caso in cui la colonna presenti SET ANSI_PADDING ON. La spaziatura viene aggiunta dal driver JDBC se mancante nelle colonne char del server.<br /><br /> Il tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** è un tipo JDBC **BINARY** con lunghezza fissa di 8 byte. |
| A lunghezza variabile | Il tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** viene mappato al tipo JDBC **VARBINARY**.<br /><br /> Il tipo **udt** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato a JDBC come tipo **VARBINARY**.                                                                                                                                                                                                                                 |
| long            | Il tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **image** viene mappato al tipo JDBC **LONGVARBINARY**. Poiché si tratta di un tipo deprecato a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è necessario usare un tipo valore di grandi dimensioni, **varbinary(max)** .                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipi di valori numerici esatti

Ai tipi di valori numerici esatti di JDBC viene eseguito il mapping direttamente ai tipi corrispondenti di SQL Server.  
  
| Type     | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | Il tipo **BIT** di JDBC rappresenta un singolo bit che può essere 0 o 1. Viene mappato a un tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit**.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | Il tipo **TINYINT** di JDBC rappresenta un singolo byte. Viene mappato a un tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint**.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | Il tipo **SMALLINT** di JDBC rappresenta un valore intero a 16 bit con segno. Viene mappato a un tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint**.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | Il tipo **INTEGER** di JDBC rappresenta un valore intero a 32 bit con segno. Viene mappato a un tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | Il tipo **BIGINT** di JDBC rappresenta un valore intero a 64 bit con segno. Viene mappato a un tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint**.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | Il tipo **NUMERIC** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori di precisione identica. Il tipo **NUMERIC** viene mappato al tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numeric**.                                                                                                                                                                                                                                                                   |
| DECIMAL  | Il tipo **DECIMAL** di JDBC rappresenta un valore decimale a precisione fissa che può contenere valori pari almeno alla precisione specificata. Il tipo **DECIMAL** viene mappato al tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal**.<br /><br /> Il tipo JDBC **DECIMAL** viene mappato anche ai tipi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **money** e **smallmoney**, che sono tipi decimali specifici a precisione fissa memorizzati, rispettivamente, in 8 e 4 byte. |
  
## <a name="approximate-numeric-types"></a>Tipi di valori numerici approssimati

I tipi numerici approssimati JDBC sono **REAL**, **DOUBLE** e **FLOAT**.  
  
| Type   | Descrizione                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | Il tipo JDBC **REAL** presenta sette cifre di precisione (precisione singola) e viene mappato direttamente al tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | Il tipo JDBC **DOUBLE** presenta 15 cifre di precisione (precisione doppia) e viene mappato al tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**. Il tipo JDBC **FLOAT** è sinonimo di **DOUBLE**. Per non creare confusione tra **FLOAT** e **DOUBLE**, è preferibile usare il tipo **DOUBLE**. |
  
## <a name="datetime-types"></a>Tipi datetime

Il tipo JDBC **TIMESTAMP** viene mappato ai tipi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** e **smalldatetime**. Il tipo **datetime** viene memorizzato in due valori interi a 4 byte. Il tipo **smalldatetime** contiene le stesse informazioni (data e ora), ma, essendo memorizzato in due valori small integer a 2 byte, garantisce una precisione inferiore.  
  
> [!NOTE]  
> Il tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** è un tipo stringa binario a lunghezza fissa. Non viene mappato ai tipi JDBC relativi a data e ora: **DATE**, **TIME** o **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Mapping personalizzato dei tipi

La caratteristica del mapping personalizzato dei tipi di JDBC, che usa le interfacce SQLData per i tipi avanzati di JDBC (UDT, Struct e così via), non è implementata nel driver JDBC.  
  
## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
