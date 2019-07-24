---
title: Informazioni sulle conversioni dei tipi di dati | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7029faf333c00fc18e4f35743706a012b76c1e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004180"
---
# <a name="understanding-data-type-conversions"></a>Informazioni sulle conversioni dei tipi di dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per semplificare la conversione dei tipi di dati del linguaggio di programmazione Java in tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono disponibili le conversioni dei tipi di dati necessarie in base alla specifica JDBC. Per maggiore flessibilità, tutti i tipi sono convertibili in e da tipi di dati **Object**, **String**e **byte []** .

## <a name="getter-method-conversions"></a>Conversioni dei metodi di richiamo

Sulla base dei tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il grafico seguente contiene la mappa di conversione del driver JDBC per i metodi get\<Type>() della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e le conversioni supportate nei metodi get\<Type>() della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

Sono disponibili tre categorie di conversione supportate dai metodi getter del driver JDBC:

- **Senza perdita di dati (x)** : conversioni nei casi in cui il tipo di richiamo è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a getBigDecimal in una colonna decimale del server sottostante, la conversione non è necessaria.

- **Convertito (y)** : conversioni dai tipi di server numerici nei tipi di linguaggio Java in cui la conversione è regolare e segue le regole di conversione del linguaggio Java. In tali conversioni, la precisione viene sempre troncata, mai arrotondata, e l'overflow viene gestito come modulo del tipo di destinazione inferiore. Se ad esempio si chiama getInt su una colonna **decimale** sottostante che contiene "1,9999", verrà restituito "1", oppure se il valore **decimale** sottostante è "3 miliardi", il valore **int** viene overflow in "-1294967296".

- **Dipendente dai dati (z)** : le conversioni dai tipi di caratteri sottostanti in tipi numerici richiedono che i tipi di caratteri contengano valori che è possibile convertire in quel determinato tipo. Non vengono eseguite altre conversioni. Se è troppo grande per il tipo di richiamo, il valore non è valido. Se, ad esempio, viene chiamato getInt per una colonna varchar(50) che contiene "53", il valore viene restituito come **int**. Se invece il valore sottostante è "xyz" o "3000000000", viene generato un errore.

Se getString viene chiamato su un tipo di dati **Binary**, **varbinary**, **varbinary (max)** o **Image** Column, il valore viene restituito come valore stringa esadecimale.

## <a name="updater-method-conversions"></a>Conversioni dei metodi di aggiornamento

Per i dati Java tipizzati passati ai metodi update\<Type() della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) si applicano le seguenti conversioni.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

Sono disponibili tre categorie di conversione supportate dai metodi di aggiornamento del driver JDBC:

- **Senza perdita di dati (x)** : conversioni nei casi in cui il tipo di aggiornamento è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a updateBigDecimal in una colonna decimale del server sottostante, la conversione non è necessaria.

- **Convertito (y)** : conversioni dai tipi di server numerici nei tipi di linguaggio Java in cui la conversione è regolare e segue le regole di conversione del linguaggio Java. In tali conversioni, la precisione viene sempre troncata, mai arrotondata, e l'overflow viene gestito come modulo del tipo di destinazione, ovvero quello inferiore. Ad esempio, se si chiama updateDecimal su una colonna **int** sottostante che contiene "1,9999", verrà restituito "1" o se il valore **decimale** sottostante è "3 miliardi", il valore **int** viene overflow in "-1294967296".

- **Dipendente dai dati (z)** : le conversioni dai tipi di dati di origine sottostanti in tipi di dati di destinazione richiedono che i valori contenuti possano essere convertiti nei tipi di destinazione. Non vengono eseguite altre conversioni. Se è troppo grande per il tipo di richiamo, il valore non è valido. Se, ad esempio, updateString viene chiamato su una colonna int che contiene "53", l'aggiornamento verrà eseguito. Se invece il valore String sottostante è "foo" o "3000000000", verrà generato un errore.

Quando updateString viene chiamato su un tipo di dati **Binary**, **varbinary**, **varbinary (max)** o **Image** , il valore della stringa viene gestito come valore stringa esadecimale.

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiamano i metodi updateBytes, updateBinaryStream o updateBlob, il valore dei dati deve essere la rappresentazione in forma di stringa esadecimale dei caratteri XML. Esempio:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="setter-method-conversions"></a>Conversioni dei metodi di impostazione

Per i tipi Java tipizzati passati ai metodi set\<Type() delle classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), si applicano le seguenti conversioni.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

Il server cercherà di eseguire la conversione e restituirà degli errori in caso di esito negativo.

Nel caso del tipo di dati **String** , se il valore supera la lunghezza di **varchar**, viene eseguito il mapping a **LONGVARCHAR**. Analogamente, **nvarchar** esegue il mapping a **LONGNVARCHAR** se il valore supera la lunghezza di **nvarchar**supportata. Lo stesso vale per **byte[]** . I valori più lunghi di **varbinary** diventano **LONGVARBINARY**.

Sono disponibili due categorie di conversione supportate dai metodi setter del driver JDBC:

- **Senza perdita di dati (x)** : conversioni per i casi numerici in cui il tipo di impostazione è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a setBigDecimal in una colonna **decimale** del server sottostante, la conversione non è necessaria. Per la conversione da un tipo numeric a un tipo character, il tipo di dati **numeric** Java viene convertito in una **stringa**. Ad esempio, la chiamata a setDouble con un valore pari a "53" in una colonna varchar(50) produrrà un valore character "53" nella colonna di destinazione.

- **Convertito (y)** : conversioni da un tipo **numerico** Java a un tipo **numerico** Server sottostante minore. Questa conversione è regolare e segue le convenzioni di conversione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisione è sempre troncata, mai arrotondata, e l'overflow genera un errore di conversione non supportata. Ad esempio, se si usa updateDecimal con un valore pari a "1,9999" in una colonna Integer sottostante verrà restituito "1" nella colonna di destinazione. Se invece viene passato "3000000000", verrà generato un errore.

- **Dipendente dai dati (z)** : le conversioni da un tipo di **stringa** Java al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati sottostante dipendono dalle condizioni seguenti: il driver invia il valore **stringa** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed esegue le conversioni. Se necessario. Se la proprietà sendStringParametersAsUnicode è impostata su true e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente la conversione di **nvarchar** in **image** e verrà generata un'eccezione SQLServerException. Se la proprietà sendStringParametersAsUnicode è impostata su false e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la conversione di **varchar** in **image** e non viene generata un'eccezione.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le conversioni e restituisce gli errori al driver JDBC in caso di problemi.

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiamano i metodi updateBytes, updateBinaryStream o updateBlob, il valore dei dati deve essere la rappresentazione in forma di stringa esadecimale dei caratteri XML. Esempio:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="conversions-on-setobject"></a>Conversioni in setObject

> [!NOTE]  
> Microsoft JDBC Driver 4,2 (e versioni successive) per SQL Server supporta JDBC 4,1 e 4,2. Per informazioni più dettagliate sui mapping e sulle conversioni dei tipi di dati 4,1 e 4,2, vedere la pagina relativa [alla conformità jdbc 4,1 per il driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e la [conformità a JDBC 4,2 per il driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), oltre alle informazioni riportate di seguito.

Per i dati Java tipizzati passati ai metodi setObject(\<Type>) della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), si applicano le seguenti conversioni.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

Il metodo setObject senza alcun tipo di destinazione specificato utilizzerà il mapping predefinito. Nel caso del tipo di dati **String** , se il valore supera la lunghezza di **varchar**, viene eseguito il mapping a **LONGVARCHAR**. Analogamente, **nvarchar** esegue il mapping a **LONGNVARCHAR** se il valore supera la lunghezza di **nvarchar**supportata. Lo stesso vale per **byte[]** . I valori più lunghi di **varbinary** diventano **LONGVARBINARY**.

Sono disponibili tre categorie di conversione supportate dai metodi setObject del driver JDBC:

- **Senza perdita di dati (x)** : conversioni per i casi numerici in cui il tipo di impostazione è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a setBigDecimal in una colonna **decimale** del server sottostante, la conversione non è necessaria. Per la conversione da un tipo numeric a un tipo character, il tipo di dati **numeric** Java viene convertito in una **stringa**. Ad esempio, la chiamata a setDouble con un valore di "53" in una colonna varchar(50) produrrà un valore character "53" nella colonna di destinazione.

- **Convertito (y)** : conversioni da un tipo **numerico** Java a un tipo **numerico** Server sottostante minore. Questa conversione è regolare e segue le convenzioni di conversione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisione è sempre troncata, mai arrotondata, e l'overflow genera un errore di conversione non supportata. Ad esempio, se si usa updateDecimal con un valore pari a "1,9999" in una colonna Integer sottostante verrà restituito "1" nella colonna di destinazione. Se invece viene passato "3000000000", verrà generato un errore.

- **Dipendente dai dati (z)** : le conversioni da un tipo di **stringa** Java al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati sottostante dipendono dalle condizioni seguenti: il driver invia il valore **stringa** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed esegue le conversioni. Se necessario. Se la proprietà di connessione sendStringParametersAsUnicode è impostata su true e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente la conversione di **nvarchar** in **image** e verrà generata un'eccezione SQLServerException. Se la proprietà sendStringParametersAsUnicode è impostata su false e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la conversione di **varchar** in **image** e non viene generata un'eccezione.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'impostazione bulk delle conversioni e restituisce gli errori al driver JDBC in caso di problemi. Le conversioni lato client sono l'eccezione e vengono eseguite solo nel caso di valori di **Data**, **ora**, **timestamp**, **booleani**e **stringa** .

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiama il metodo setObject(byte[], SQLXML), setObject(inputStream, SQLXML) o setObject(Blob, SQLXML), il valore dei dati deve essere la rappresentazione di stringa esadecimale dei caratteri XML. Esempio:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
