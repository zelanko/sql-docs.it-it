---
title: Dati FILESTREAM
description: Viene descritto come utilizzare dati con valori di grandi dimensioni archiviati in SQL Server 2008 con l'attributo FILESTREAM.
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 83e793fac40a8e41850f2a45e138dd125130c13e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452213"
---
# <a name="filestream-data"></a>Dati FILESTREAM

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L'attributo di archiviazione FILESTREAM è per i dati binari (BLOB) archiviati in una colonna varbinary (max). Prima di FILESTREAM, l'archiviazione dei dati binari richiedeva una gestione speciale. I dati non strutturati, ad esempio documenti di testo, immagini e video, vengono spesso archiviati all'esterno del database, rendendolo difficile da gestire.

> [!NOTE]
> È necessario installare la .NET Framework 3,5 SP1 (o versione successiva) o .NET Core per utilizzare i dati FILESTREAM utilizzando SqlClient.

Se si specifica l'attributo FILESTREAM in una colonna varbinary(max), in SQL Server i dati vengono archiviati nel file system NTFS locale anziché nel file di database. Sebbene vengano archiviati separatamente, è possibile usare le stesse istruzioni Transact-SQL supportate per l'uso di dati varbinary(max) archiviati nel database.

## <a name="sqlclient-support-for-filestream"></a>Supporto SqlClient per FILESTREAM

Il provider di dati Microsoft SqlClient per SQL Server, <xref:Microsoft.Data.SqlClient>, supporta la lettura e la scrittura nei dati FILESTREAM usando la classe <xref:Microsoft.Data.SqlTypes.SqlFileStream> definita nello spazio dei nomi <xref:System.Data.SqlTypes>. `SqlFileStream` eredita dalla classe <xref:System.IO.Stream>, che fornisce metodi per la lettura e la scrittura nei flussi di dati. La lettura da un flusso trasferisce i dati dal flusso in una struttura di dati, ad esempio una matrice di byte. La scrittura trasferisce i dati dalla struttura dei dati in un flusso.

### <a name="creating-the-sql-server-table"></a>Creazione della tabella SQL Server

Le istruzioni Transact-SQL seguenti consentono di creare una tabella denominata employees e di inserire una riga di dati. Una volta abilitata l'archiviazione FILESTREAM, è possibile usare questa tabella insieme agli esempi di codice seguenti. I collegamenti alle risorse della documentazione online di SQL Server sono disponibili alla fine di questo argomento.

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>Esempio: lettura, sovrascrittura e inserimento di dati FILESTREAM

Nell'esempio seguente viene illustrato come leggere i dati da un FILESTREAM. Il codice ottiene il percorso logico del file, impostando il `FileAccess` su `Read` e il `FileOptions` `SequentialScan`. Il codice legge quindi i byte da SqlFileStream nel buffer. I byte vengono quindi scritti nella finestra della console.

Nell'esempio viene inoltre illustrato come scrivere dati in un FILESTREAM in cui tutti i dati esistenti vengono sovrascritti. Il codice ottiene il percorso logico del file e crea la `SqlFileStream`, impostando il `FileAccess` su `Write` e la `FileOptions` su `SequentialScan`. Un singolo byte viene scritto nel `SqlFileStream`, sostituendo tutti i dati nel file.

L'esempio dimostra inoltre come scrivere i dati in un oggetto FILESTREAM usando il metodo Seek per aggiungere i dati alla fine del file. Il codice ottiene il percorso logico del file e crea la `SqlFileStream`, impostando il `FileAccess` su `ReadWrite` e la `FileOptions` su `SequentialScan`. Il codice usa il metodo Seek per cercare alla fine del file, aggiungendo un singolo byte al file esistente.

```csharp
using System;
using Microsoft.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

Per un altro esempio, vedere [Come archiviare e recuperare dati binari in una colonna di flusso di file](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str).

## <a name="resources-in-sql-server-books-online"></a>Risorse in documentazione online di SQL Server

La documentazione completa per FILESTREAM è disponibile nelle sezioni seguenti della documentazione online di SQL Server.

|Argomento|Descrizione|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|Viene descritto quando utilizzare l'archiviazione FILESTREAM e in che modo integra la SQL Server motore di database con un file system NTFS.|
|[Creazione di applicazioni client per dati FILESTREAM](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|Vengono descritte le funzioni dell'API Windows per l'utilizzo di dati FILESTREAM.|
|[FILESTREAM e altre funzionalità di SQL Server](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|Vengono fornite considerazioni, linee guida e limitazioni per l'utilizzo di dati FILESTREAM con altre funzionalità di SQL Server.|

## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
