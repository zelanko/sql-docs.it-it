---
title: Manipolazione dei dati
description: Mette a disposizione esempi di codifica delle applicazioni MARS.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: a3a567d86cb70c5d6d931d631a0f744ea59d359f
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896697"
---
# <a name="manipulating-data"></a>Manipolazione dei dati

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Prima dell'introduzione di MARS (Multiple Active Result Set), gli sviluppatori dovevano usare più connessioni o cursori sul lato server per risolvere determinati scenari. Inoltre, quando venivano usate più connessioni in una situazione di transazione, erano necessarie le connessioni associate (con **sp_getbindtoken** e **sp_bindsession**). Negli scenari seguenti viene illustrato come usare una connessione abilitata per MARS anziché più connessioni.  
  
## <a name="using-multiple-commands-with-mars"></a>Uso di più comandi con MARS  
Nell'applicazione console seguente viene illustrato come usare due oggetti <xref:Microsoft.Data.SqlClient.SqlDataReader> con due oggetti <xref:Microsoft.Data.SqlClient.SqlCommand> e un singolo oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> con MARS abilitato.  
  
### <a name="example"></a>Esempio  
Nell'esempio viene aperta una singola connessione al database di **AdventureWorks**. Usando un oggetto <xref:Microsoft.Data.SqlClient.SqlCommand>, viene creata una <xref:Microsoft.Data.SqlClient.SqlDataReader>. Quando il lettore è in uso viene aperto un secondo <xref:Microsoft.Data.SqlClient.SqlDataReader>, usando i dati del primo <xref:Microsoft.Data.SqlClient.SqlDataReader> come input per la clausola WHERE per il secondo lettore.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in SQL Server. Per la stringa di connessione specificata nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale. Modificare la stringa di connessione in base alle esigenze dell'ambiente in uso.  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>Lettura e aggiornamento dei dati con MARS  
MARS consente di usare una connessione sia per le operazioni di lettura che per operazioni DML (Data Manipulation Language) con più di un'operazione in sospeso. Questa funzionalità consente a un'applicazione di evitare la gestione degli errori dovuti a una connessione occupata. Inoltre, MARS può sostituire l'utente dei cursori sul lato server, che in genere consumano più risorse. Infine, poiché su una singola connessione possono essere eseguite più operazioni, queste possono condividere lo stesso contesto di transazione, eliminando la necessità di usare le stored procedure di sistema **sp_getbindtoken** e **sp_bindsession**.  
  
### <a name="example"></a>Esempio  
Nell'applicazione console seguente viene illustrato come usare due oggetti <xref:Microsoft.Data.SqlClient.SqlDataReader> con tre oggetti <xref:Microsoft.Data.SqlClient.SqlCommand> e un singolo oggetto <xref:Microsoft.Data.SqlClient.SqlConnection> con MARS abilitato. Il primo oggetto comando recupera un elenco di fornitori la cui posizione creditizia è 5. Il secondo oggetto comando usa l'ID fornitore specificato da <xref:Microsoft.Data.SqlClient.SqlDataReader> per caricare il secondo <xref:Microsoft.Data.SqlClient.SqlDataReader> con tutti i prodotti per il fornitore specifico. Ogni record di prodotto viene visitato dal secondo <xref:Microsoft.Data.SqlClient.SqlDataReader>. Viene calcolato il nuovo valore di **OnOrderQty**. Il terzo oggetto comando viene usato per aggiornare la tabella **ProductVendor** con il nuovo valore. L'intero processo viene eseguito nell'ambito di una singola transazione, di cui alla fine viene eseguito il rollback.  
  
> [!NOTE]
>  Nell'esempio seguente viene usato il database di esempio **AdventureWorks** incluso in SQL Server. Per la stringa di connessione specificata nel codice di esempio si presuppone che il database sia installato e disponibile nel computer locale. Modificare la stringa di connessione in base alle esigenze dell'ambiente in uso.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [MARS (Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
