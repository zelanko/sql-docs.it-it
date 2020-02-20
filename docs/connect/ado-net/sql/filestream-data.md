---
title: Dati FILESTREAM
description: Viene descritto come usare dati con valori di grandi dimensioni archiviati in SQL Server 2008 con l'attributo FILESTREAM.
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 602dfe9c96c1e8713b90c607806dd09ed16a37b6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247755"
---
# <a name="filestream-data"></a>Dati FILESTREAM

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

L'attributo di archiviazione FILESTREAM è destinato all'uso con i dati binari (BLOB) archiviati in una colonna varbinary(max). Prima di FILESTREAM, l'archiviazione dei dati binari richiedeva una gestione speciale. I dati non strutturati, ad esempio documenti di testo, immagini e video, vengono spesso archiviati all'esterno del database e diventano difficili da gestire.

> [!NOTE]
> È necessario installare .NET Framework 3.5 SP1 (o versione successiva) o .NET Core per lavorare con i dati FILESTREAM usando SqlClient.

Se si specifica l'attributo FILESTREAM in una colonna varbinary(max), in SQL Server i dati vengono archiviati nel file system NTFS locale anziché nel file di database. Sebbene vengano archiviati separatamente, è possibile usare le stesse istruzioni Transact-SQL supportate per l'uso di dati varbinary(max) archiviati nel database.

## <a name="sqlclient-support-for-filestream"></a>Supporto di SqlClient per FILESTREAM

Il provider di dati Microsoft SqlClient per SQL Server, <xref:Microsoft.Data.SqlClient>, supporta la lettura e la scrittura nei dati FILESTREAM usando la classe <xref:Microsoft.Data.SqlTypes.SqlFileStream> definita nello spazio dei nomi <xref:System.Data.SqlTypes>. `SqlFileStream` eredita dalla classe <xref:System.IO.Stream>, che specifica i metodi per la lettura e la scrittura nei flussi di dati. La lettura da un flusso trasferisce i dati dal flusso in una struttura di dati, ad esempio una matrice di byte. La scrittura trasferisce i dati dalla struttura di dati in un flusso.

### <a name="creating-the-sql-server-table"></a>Creazione della tabella di SQL Server

Le istruzioni Transact-SQL seguenti consentono di creare una tabella denominata employees e di inserire una riga di dati. Dopo aver abilitato l'archiviazione FILESTREAM, è possibile usare questa tabella insieme agli esempi di codice riportati di seguito. I collegamenti alle risorse della documentazione online di SQL Server sono disponibili alla fine di questo argomento.

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

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>Esempio: Lettura, sovrascrittura e inserimento di dati FILESTREAM

Nell'esempio seguente viene illustrato come leggere i dati da un oggetto FILESTREAM. Il codice ottiene il percorso logico del file, impostando `FileAccess` su `Read` e `FileOptions` su `SequentialScan`. Il codice legge quindi i byte da SqlFileStream nel buffer. I byte vengono quindi scritti nella finestra della console.

L'esempio illustra anche come scrivere dati in un oggetto FILESTREAM nel quale vengono sovrascritti tutti i dati esistenti. Il codice ottiene il percorso logico del file e crea `SqlFileStream`, impostando `FileAccess` su `Write` e `FileOptions` su `SequentialScan`. Un singolo byte viene scritto in `SqlFileStream`, sostituendo tutti i dati nel file.

L'esempio dimostra inoltre come scrivere i dati in un oggetto FILESTREAM usando il metodo Seek per aggiungere i dati alla fine del file. Il codice ottiene il percorso logico del file e crea `SqlFileStream`, impostando `FileAccess` su `ReadWrite` e `FileOptions` su `SequentialScan`. Il codice usa il metodo Seek per cercare alla fine del file, aggiungendo un singolo byte al file esistente.

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

## <a name="resources-in-sql-server-books-online"></a>Risorse nella documentazione online di SQL Server

La documentazione completa per FILESTREAM è disponibile nelle sezioni seguenti della documentazione online di SQL Server.

|Argomento|Descrizione|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|Spiega quando si usa l'archiviazione FILESTREAM e in che modo integra il motore di database di SQL Server con un file system NTFS.|
|[Creazione di applicazioni client per dati FILESTREAM](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|Descrive le funzioni dell'API Windows per l'uso dei dati FILESTREAM.|
|[FILESTREAM e altre funzionalità di SQL Server](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|Include considerazioni, linee guida e limitazioni per l'uso dei dati FILESTREAM con altre funzionalità di SQL Server.|

## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
