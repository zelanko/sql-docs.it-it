---
title: Inserimento di un'immagine da un file
description: Viene descritto come usare un'immagine da un file.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8f7b561a6aba4539964d73dacfd9e45db2dd6aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452171"
---
# <a name="inserting-an-image-from-a-file"></a>Inserimento di un'immagine da un file

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

È possibile scrivere un oggetto binario di grandi dimensioni (BLOB) in un database come dati binari o di tipo carattere, a seconda del tipo di campo dell'origine dati. BLOB è un termine generico che fa riferimento ai tipi di dati `text`, `ntext` e `image`, che in genere contengono documenti e immagini.  
  
Per scrivere un valore BLOB nel database, eseguire l'istruzione INSERT o UPDATE appropriata e passare il valore BLOB come parametro di input. Se il BLOB viene archiviato come testo, ad esempio un SQL Server `text` campo, è possibile passare il BLOB come parametro di stringa. Se il BLOB viene archiviato in formato binario, ad esempio un SQL Server `image` campo, è possibile passare una matrice di tipo `byte` come parametro binario.
  
## <a name="example"></a>Esempio  
Nell'esempio di codice seguente vengono aggiunte informazioni sul dipendente alla tabella Employees del database Northwind. Una foto del dipendente viene letta da un file e aggiunta al campo Photo della tabella, che è un campo immagine.  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [Dati binari e con valori di grandi dimensioni di SQL Server](sql-server-binary-large-value-data.md)
