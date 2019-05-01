---
title: SDK per Java extension - estensioni del linguaggio SQL Server
description: Descrizione di estendibilità di Microsoft SDK per Java per Microsoft SQL Server 2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fd050a5120f14b4727b93a74c1f46392ac24dd49
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759098"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>Estendibilità di Microsoft SDK per Java per SQL Server

In SQL Server CTP 2.5, è possibile implementare un programma Java per SQL Server usando l'estendibilità di Microsoft SDK per Java. Si tratta di un'interfaccia per l'estensione del linguaggio Java utilizzato per scambiare dati con SQL Server e per eseguire il codice Java da SQL Server.

> [!Note]
> il SDK nella versione CTP 2.5 è un enorme cambiamento da versioni CTP precedenti. Gli esempi si fosse funzionante dovrà essere aggiornato per usare invece il SDK.

Scaricare il [estendibilità di Microsoft SDK per Java per Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension).

## <a name="implementation-requirements"></a>Requisiti di implementazione

L'interfaccia SDK definisce un set di requisiti che devono essere soddisfatti per SQL Server comunicare con il runtime di Java. Ciò significa che è necessario seguire alcune regole di implementazione della classe principale. SQL Server possono quindi eseguire un metodo specifico nei dati di classe e lo scambio di Java usando l'estensione del linguaggio Java.

Per un esempio di come è possibile usare il SDK, vedere la [esempio end-to-end](java-first-sample.md).

## <a name="sdk-classes"></a>Classi SDK

Questo SDK è costituito da tre classi.

Due classi astratte che definiscono l'interfaccia Java extension Usa per scambiare dati con SQL Server:

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

La terza classe è una classe helper che contiene un'implementazione di un oggetto set di dati. Questa è una classe facoltativa da usare per renderne più semplice iniziare. È possibile usare la propria implementazione di tale classe.

- **PrimitiveDataset**

Seguente illustra i dettagli e il codice sorgente per ogni classe nell'estensione del linguaggio Java per SQL Server.

## <a name="abstractsqlserverextensionexecutor"></a>AbstractSqlServerExtensionExecutor

Si tratta di una classe astratta che contiene l'interfaccia utilizzata per eseguire il codice Java per l'estensione del linguaggio Java per SQL Server.

La classe principale Java deve ereditare da questa classe. Eredita da questa classe significa che esistono alcuni metodi della classe che è necessario implementare nella classe.

Per ereditare da questa classe astratta, si estende con il nome della classe astratta nella dichiarazione di classe:

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

Come minimo, la classe principale deve implementare il metodo execute(...).

### <a name="method-execute"></a>Metodo execute

Il metodo execute è il metodo che viene chiamato da SQL Server tramite l'estensione del linguaggio Java, per richiamare il codice Java da SQL Server. È consigliabile visualizzare questo come un metodo chiave in cui si include l'oggetto principale operazioni desideri eseguire da SQL Server.

Per passare gli argomenti del metodo a Java da SQL Server, usare il `@param` parametro in sp_execute_external_script. Il metodo **eseguire** accetta gli argomenti in questo modo.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

### <a name="method-init"></a>Metodo init

Il metodo init viene eseguito dopo il costruttore e prima del metodo execute. Le operazioni che devono essere eseguite prima execute(...) possono essere eseguite in questo metodo.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="abstractsqlserverextensionexecutor-source-code"></a>Codice sorgente AbstractSqlServerExtensionExecutor

Altri dettagli sono disponibili di seguito nel codice sorgente:

```java
package com.microsoft.sqlserver.javalangextension;

import java.lang.UnsupportedOperationException;

/**
 * Abstract class containing interface for handling input and output data used by the Java
 * extension.
 */
public class AbstractSqlServerExtensionDataset {
    /**
     * Column metadata interfaces
     */
    public void addColumnMetadata(int columnId, String columnName, int columnType, int precision, int scale) {
        throw new UnsupportedOperationException("addColumnMetadata is not implemented");
    }

    public int getColumnCount() {
        throw new UnsupportedOperationException("getColumnCount is not implemented");
    }

    public String getColumnName(int columnId) {
        throw new UnsupportedOperationException("getColumnName is not implemented");
    }

    public int getColumnPrecision(int columnId) {
        throw new UnsupportedOperationException("getColumnPrecision is not implemented");
    }

    public int getColumnScale(int columnId) {
        throw new UnsupportedOperationException("getColumnScale is not implemented");
    }

    public int getColumnType(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    public boolean[] getColumnNullMap(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    /**
     * Adding column interfaces
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addIntColumn is not implemented");
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addBooleanColumn is not implemented");
    }

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addLongColumn is not implemented");
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addFloatColumn is not implemented");
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addDoubleColumn is not implemented");
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addShortColumn is not implemented");
    }

    public void addStringColumn(int columnId, String[] rows) {
        throw new UnsupportedOperationException("addStringColumn is not implemented");
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        throw new UnsupportedOperationException("addBinaryColumn is not implemented");
    }

    /**
     * Retrieving column interfaces
     */
    public int[] getIntColumn(int columnId) {
        throw new UnsupportedOperationException("getIntColumn is not implemented");
    }

    public long[] getLongColumn(int columnId) {
        throw new UnsupportedOperationException("getLongColumn is not implemented");
    }

    public float[] getFloatColumn(int columnId) {
        throw new UnsupportedOperationException("getFloatColumn is not implemented");
    }

    public short[] getShortColumn(int columnId) {
        throw new UnsupportedOperationException("getShortColumn is not implemented");
    }

    public boolean[] getBooleanColumn(int columnId) {
        throw new UnsupportedOperationException("getBooleanColumn is not implemented");
    }

    public double[] getDoubleColumn(int columnId) {
        throw new UnsupportedOperationException("getDoubleColumn is not implemented");
    }

    public String[] getStringColumn(int columnId) {
        throw new UnsupportedOperationException("getStringColumn is not implemented");
    }

    public byte[][] getBinaryColumn(int columnId) {
        throw new UnsupportedOperationException("getBinaryColumn is not implemented");
    }
}
```

### <a name="primitivedataset"></a>PrimitiveDataset

Questa classe è un'implementazione di **AbstractSqlServerExtensionDataset** che archivia i tipi semplici come matrici di primitive. Viene fornito nel SDK semplicemente come una classe helper che è facoltativa da usare.

Se non si usa questa classe, è necessario implementare una classe che eredita da **AbstractSqlServerExtensionDataset**.  

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.IllegalArgumentException;
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

/**
 * Implementation of AbstractSqlServerExtensionDataset that stores
 * simple types as primitives arrays
 */
public class PrimitiveDataset extends AbstractSqlServerExtensionDataset {
    Map<Integer, String>  columnNames;
    Map<Integer, Integer> columnTypes;
    Map<Integer, Integer> columnPrecisions;
    Map<Integer, Integer> columnScales;
    Map<Integer, Object>  columns;
    Map<Integer, boolean[]> columnNullMaps;

    public PrimitiveDataset() {
        columnTypes = new HashMap<>();
        columnNames = new HashMap<>();
        columnPrecisions = new HashMap<>();
        columnScales = new HashMap<>();
        columns = new HashMap<>();
        columnNullMaps = new HashMap<>();
    }

    /**
     * Column metadata interfaces. Metadata is stored in a hash map, using the column ID as the key
     */
    public void addColumnMetadata(int columnId, String columnName, int sqlType, int precision, int scale) {
        if (columnTypes.containsKey(columnId))
        {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " already exists");
        }

        columnTypes.put(columnId, sqlType);
        columnNames.put(columnId, columnName);
        columnPrecisions.put(columnId, precision);
        columnScales.put(columnId, scale);
    }

    public int getColumnCount() {
        return columnTypes.size();
    }

    public String getColumnName(int columnId) {
        checkColumnMetadata(columnId);
        return columnNames.get(columnId);
    }

    public int getColumnPrecision(int columnId) {
        checkColumnMetadata(columnId);
        return columnPrecisions.get(columnId).intValue();
    }

    public int getColumnScale(int columnId) {
        checkColumnMetadata(columnId);
        return columnScales.get(columnId).intValue();
    }

    public int getColumnType(int columnId) {
        checkColumnMetadata(columnId);
        return columnTypes.get(columnId).intValue();
    }

    public boolean[] getColumnNullMap(int columnId) {
        checkColumnMetadata(columnId);
        return columnNullMaps.get(columnId);
    }

    /**
     * Adding column data interfaces. Column data is stored in a hash map, using the column ID as the key and
     * an array of the corresponding type representing each row. Primitives cannot be null, thus null values
     * are represented by an additional boolean array containing a flag to indicate if that value is null.
     * A null indicator array indicates that there are no null values in that column.
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    };

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addStringColumn(int columnId, String[] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    /**
     * Retreiving column data interfaces. For primitive types, calling getColumnNullMap() for the column ID
     * will return the boolean array indicating null values.
     */
    public int[] getIntColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (int[])columns.get(columnId);
    }

    public long[] getLongColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (long[])columns.get(columnId);
    }

    public float[] getFloatColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (float[])columns.get(columnId);
    }

    public short[] getShortColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (short[])columns.get(columnId);
    }

    public boolean[] getBooleanColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (boolean[])columns.get(columnId);
    }

    public double[] getDoubleColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (double[])columns.get(columnId);
    }

    public String[] getStringColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (String[])columns.get(columnId);
    }

    public byte[][] getBinaryColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (byte[][])columns.get(columnId);
    }

    private void checkColumnMetadata(int columnId)
    {
        if (!columnTypes.containsKey(columnId)) {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " does not exist");
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi

+ [-To-end di esempio Java usando il SDK](java-first-sample.md)
+ [Come chiamare Java in SQL Server](howto-call-java-from-sql.md)
+ [Estensioni di linguaggio in SQL Server](extension-java.md)
+ [Tipi di dati Java e SQL Server](java-sql-datatypes.md)
