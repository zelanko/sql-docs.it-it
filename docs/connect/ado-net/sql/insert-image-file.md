---
title: Inserimento di un'immagine da un file
description: Viene descritto come usare un'immagine ricavata da un file.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: ee951094ad3042e1d2fa31bdf35fa7e5b32f1d2c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924353"
---
# <a name="inserting-an-image-from-a-file"></a>Inserimento di un'immagine da un file

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

È possibile scrivere un oggetto binario di grandi dimensioni (BLOB) in un database come dati binari o di tipo carattere, a seconda del tipo di campo dell'origine dati. BLOB è un termine generico che fa riferimento ai tipi di dati `text`, `ntext`e `image`, che in genere contengono documenti e immagini.  
  
Per scrivere un valore BLOB nel database, eseguire l'istruzione INSERT o UPDATE appropriata e passare il valore BLOB come parametro di input. Se il BLOB viene archiviato come testo, ad esempio un campo `text` SQL Server, è possibile passare il BLOB come parametro di stringa. Se il BLOB viene archiviato in formato binario, ad esempio un campo `image` SQL Server, è possibile passare una matrice di tipo `byte` come parametro binario.
  
## <a name="example"></a>Esempio  
Nell'esempio di codice seguente vengono aggiunte informazioni sul dipendente nella tabella Dipendenti del database Northwind. Una foto del dipendente viene letta da un file e aggiunta al campo Foto nella tabella, che è un campo immagine.  
  
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
