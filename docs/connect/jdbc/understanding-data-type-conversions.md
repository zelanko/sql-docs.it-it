---
title: Conversioni di tipi di informazioni sui dati | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 01e3d8b002df2f939528bef8d4faa39d3a5c72f1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52520205"
---
# <a name="understanding-data-type-conversions"></a>Informazioni sulle conversioni dei tipi di dati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per semplificare la conversione dei tipi di dati del linguaggio di programmazione Java in tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono disponibili le conversioni dei tipi di dati necessarie in base alla specifica JDBC. Per offrire maggiore flessibilità, tutti i tipi sono convertibili da e verso **oggetti**, **stringa**, e **byte []** i tipi di dati.

## <a name="getter-method-conversions"></a>Conversioni dei metodi di richiamo

Sulla base dei tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il grafico seguente contiene la mappa di conversione del driver JDBC per i metodi get\<Type>() della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) e le conversioni supportate nei metodi get\<Type>() della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).

![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

Sono disponibili tre categorie di conversione supportate dai metodi getter del driver JDBC:

- **Senza perdita di dati (x)**: conversioni nei casi in cui il tipo di richiamo è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a getBigDecimal in una colonna decimale del server sottostante, la conversione non è necessaria.

- **Convertito (y)**: conversioni dai tipi di server numerici nei tipi di linguaggio Java in cui la conversione è regolare e segue le regole di conversione del linguaggio Java. In tali conversioni, la precisione viene sempre troncata, mai arrotondata, e l'overflow viene gestito come modulo del tipo di destinazione inferiore. Ad esempio, la chiamata getInt su un oggetto sottostante **decimale** colonna che contiene "1,9999 il valore" restituito sarà "1", oppure se sottostante **decimale** valore è "3000000000" il **int** valore causa un overflow in "-1294967296".

- **Dipendente dai dati (z)**: le conversioni dai tipi di caratteri sottostanti in tipi numerici richiedono che i tipi di caratteri contengano valori che è possibile convertire in quel determinato tipo. Non vengono eseguite altre conversioni. Se è troppo grande per il tipo di richiamo, il valore non è valido. Se, ad esempio, viene chiamato getInt per una colonna varchar(50) che contiene "53", il valore viene restituito come **int**. Se invece il valore sottostante è "xyz" o "3000000000", viene generato un errore.

Se getString viene chiamato su un **binario**, **varbinary**, **varbinary (max)**, oppure **immagine** come tipo di dati colonna, viene restituito il valore un valore di stringa esadecimale.

## <a name="updater-method-conversions"></a>Conversioni dei metodi di aggiornamento

Per i dati Java tipizzati passati ai metodi update\<Type() della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) si applicano le seguenti conversioni.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

Sono disponibili tre categorie di conversione supportate dai metodi di aggiornamento del driver JDBC:

- **Senza perdita di dati (x)**: conversioni nei casi in cui il tipo di aggiornamento è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a updateBigDecimal in una colonna decimale del server sottostante, la conversione non è necessaria.

- **Convertito (y)**: conversioni dai tipi di server numerici nei tipi di linguaggio Java in cui la conversione è regolare e segue le regole di conversione del linguaggio Java. In tali conversioni, la precisione viene sempre troncata, mai arrotondata, e l'overflow viene gestito come modulo del tipo di destinazione, ovvero quello inferiore. Ad esempio, la chiamata updateDecimal su un oggetto sottostante **int** colonna che contiene "1,9999 il valore" restituito sarà "1", oppure se sottostante **decimale** valore è "3000000000" il **int**valore causa un overflow in "-1294967296".

- **Dipendente dai dati (z)**: le conversioni dai tipi di dati di origine sottostanti in tipi di dati di destinazione richiedono che i valori contenuti possano essere convertiti nei tipi di destinazione. Non vengono eseguite altre conversioni. Se è troppo grande per il tipo di richiamo, il valore non è valido. Se, ad esempio, updateString viene chiamato su una colonna int che contiene "53", l'aggiornamento verrà eseguito. Se invece il valore String sottostante è "foo" o "3000000000", verrà generato un errore.

Quando updateString viene chiamato su un **binario**, **varbinary**, **varbinary (max)**, oppure **immagine** il tipo di dati colonna, il valore String verrà gestito come valore di stringa esadecimale.

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiama updateBytes, updateBinaryStream o metodi updateBlob, il valore di dati deve essere la rappresentazione di stringa esadecimale dei caratteri XML. Ad esempio

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="setter-method-conversions"></a>Conversioni dei metodi di impostazione

Per i tipi Java tipizzati passati ai metodi set\<Type() delle classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), si applicano le seguenti conversioni.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

Il server cercherà di eseguire la conversione e restituirà degli errori in caso di esito negativo.

Nel caso del **stringa** tipo di dati, se il valore supera la lunghezza di **VARCHAR**, viene eseguito il mapping **LONGVARCHAR**. Analogamente, **NVARCHAR** esegue il mapping ai **LONGNVARCHAR** se il valore supera la lunghezza di **NVARCHAR**. Lo stesso vale per **byte[]**. Valori più lunghi **VARBINARY** diventano **LONGVARBINARY**.

Sono disponibili due categorie di conversione supportate dai metodi setter del driver JDBC:

- **Senza perdita di dati (x)**: conversioni per i casi numerici in cui il tipo di impostazione è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a setBigDecimal in una colonna **decimale** del server sottostante, la conversione non è necessaria. Per la conversione da un tipo numeric a un tipo character, il tipo di dati **numeric** Java viene convertito in una **stringa**. Ad esempio, la chiamata a setDouble con un valore pari a "53" in una colonna varchar(50) produrrà un valore character "53" nella colonna di destinazione.

- **Convertito (y)**: le conversioni da un linguaggio **numerici** tipo a un server sottostante **numerico** tipo inferiori. Questa conversione è regolare e segue le convenzioni di conversione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisione è sempre troncata, mai arrotondata, e l'overflow genera un errore di conversione non supportata. Ad esempio, se si usa updateDecimal con un valore pari a "1,9999" in una colonna Integer sottostante verrà restituito "1" nella colonna di destinazione. Se invece viene passato "3000000000", verrà generato un errore.

- **Dipendente dai dati (z)**: le conversioni da un linguaggio **stringa** tipo sottostante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende dal tipo di dati per le condizioni seguenti: il driver invia il **stringa** valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le conversioni, se necessario. Se la proprietà sendStringParametersAsUnicode è impostata su true e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente la conversione di **nvarchar** in **image** e verrà generata un'eccezione SQLServerException. Se la proprietà sendStringParametersAsUnicode è impostata su false e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la conversione di **varchar** in **image** e non viene generata un'eccezione.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le conversioni e restituisce gli errori al driver JDBC in caso di problemi.

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiama updateBytes, updateBinaryStream o metodi updateBlob, il valore di dati deve essere la rappresentazione di stringa esadecimale dei caratteri XML. Ad esempio

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="conversions-on-setobject"></a>Conversioni in setObject

> [!NOTE]  
> Microsoft JDBC driver 4.2 (e versioni successive) per SQL Server supporta JDBC 4.1 e 4.2. Per ulteriori dettagli su versioni 4.1 e 4.2 i mapping di tipo di dati e le conversioni, vedere [conformità a JDBC 4.1 per il Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [JDBC 4.2 conformità per il Driver JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), oltre alle informazioni seguenti.

Per i dati Java tipizzati passati ai metodi setObject(\<Type>) della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), si applicano le seguenti conversioni.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

Il metodo setObject senza alcun tipo di destinazione specificato utilizzerà il mapping predefinito. Nel caso del **stringa** tipo di dati, se il valore supera la lunghezza di **VARCHAR**, viene eseguito il mapping **LONGVARCHAR**. Analogamente, **NVARCHAR** esegue il mapping ai **LONGNVARCHAR** se il valore supera la lunghezza di **NVARCHAR**. Lo stesso vale per **byte[]**. Valori più lunghi **VARBINARY** diventano **LONGVARBINARY**.

Sono disponibili tre categorie di conversione supportate dai metodi setObject del driver JDBC:

- **Senza perdita di dati (x)**: conversioni per i casi numerici in cui il tipo di impostazione è inferiore o identico al tipo di server sottostante. Ad esempio, quando si esegue la chiamata a setBigDecimal in una colonna **decimale** del server sottostante, la conversione non è necessaria. Per la conversione da un tipo numeric a un tipo character, il tipo di dati **numeric** Java viene convertito in una **stringa**. Ad esempio, la chiamata a setDouble con un valore di "53" in una colonna varchar(50) produrrà un valore character "53" nella colonna di destinazione.

- **Convertito (y)**: le conversioni da un linguaggio **numerici** tipo a un server sottostante **numerico** tipo inferiori. Questa conversione è regolare e segue le convenzioni di conversione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisione è sempre troncata, mai arrotondata, e l'overflow genera un errore di conversione non supportata. Ad esempio, se si usa updateDecimal con un valore pari a "1,9999" in una colonna Integer sottostante verrà restituito "1" nella colonna di destinazione. Se invece viene passato "3000000000", verrà generato un errore.

- **Dipendente dai dati (z)**: le conversioni da un linguaggio **stringa** tipo sottostante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende dal tipo di dati per le condizioni seguenti: il driver invia il **stringa** valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue le conversioni, se necessario. Se la proprietà di connessione sendStringParametersAsUnicode è impostata su true e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente la conversione di **nvarchar** in **image** e verrà generata un'eccezione SQLServerException. Se la proprietà sendStringParametersAsUnicode è impostata su false e il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottostante è **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la conversione di **varchar** in **image** e non viene generata un'eccezione.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'impostazione bulk delle conversioni e restituisce gli errori al driver JDBC in caso di problemi. Le conversioni sul lato client non sono frequenti e vengono eseguite solo nel caso di **data**, **ora**, **timestamp**, **booleano**e  **Stringa** valori.

Quando il tipo di dati colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è **XML**, il valore dei dati deve essere un tipo **XML** valido. Quando si chiama il metodo setObject(byte[], SQLXML), setObject(inputStream, SQLXML) o setObject(Blob, SQLXML), il valore dei dati deve essere la rappresentazione di stringa esadecimale dei caratteri XML. Ad esempio

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Si noti che se i caratteri XML sono espressi in codifiche di caratteri specifiche, è necessario un indicatore dell'ordine dei byte (BOM, Byte-Order Mark).

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
