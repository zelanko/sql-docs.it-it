---
title: Enumerazione di istanze di SQL Server (ADO.NET)
description: Viene descritto come enumerare le istanze attive di SQL Server.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: d3dcb896975d33e4d2e59e438cf03dfe41a77860
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907157"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>Enumerazione di istanze di SQL Server (ADO.NET)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server consente alle applicazioni di trovare le istanze di SQL Server all'interno della rete corrente. La classe <xref:System.Data.Sql.SqlDataSourceEnumerator> espone queste informazioni allo sviluppatore di applicazioni, offrendo una classe <xref:System.Data.DataTable> che contiene informazioni su tutti i server visibili. La tabella restituita include un elenco di istanze di server disponibili in rete che corrisponde all'elenco fornito quando un utente tenta di creare una nuova connessione ed espande l'elenco a discesa contenente tutti i server disponibili nella finestra di dialogo **Proprietà connessione**. I risultati visualizzati non sono sempre completi.  
  
> [!NOTE]
>  Come per la maggior parte dei servizi di Windows, è preferibile eseguire il servizio SQL Browser con privilegi minimi. Per altre informazioni sul servizio SQL Browser e su come gestirne il comportamento, vedere la documentazione online di SQL Server.  
  
## <a name="retrieving-an-enumerator-instance"></a>Recupero dell'istanza di un enumeratore  
Per recuperare la tabella che contiene le informazioni sulle istanze di SQL Server disponibili, è prima necessario recuperare un enumeratore usando la proprietà condivisa/statica <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A>:  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
Dopo aver recuperato l'istanza statica, è possibile chiamare il metodo <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> che restituisce una classe <xref:System.Data.DataTable> contenente informazioni sui server disponibili:  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
La tabella restituita dalla chiamata al metodo contiene le colonne seguenti, tutte contenenti valori `string`:  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**ServerName**|Nome del server.|  
|**InstanceName**|Nome dell'istanza del server. Vuota se il server è in esecuzione come istanza predefinita.|  
|**IsClustered**|Indica se il server fa parte di un cluster.|  
|**Version**|Versione del server Ad esempio:<br /><br /> -   9.00.x (SQL Server 2005)<br />-   10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>Limitazioni di enumerazione  
È possibile che non siano elencati tutti i server disponibili. L'elenco può variare in base a fattori quali timeout e traffico di rete. Ciò può determinare elenchi diversi in due chiamate consecutive. Verranno elencati solo i server nella stessa rete. I pacchetti broadcast in genere non attraversano i router. Ecco perché è possibile che un server non sia visibile nell'elenco, ma sarà stabile tra le diverse chiamate.  
  
È possibile che i server elencati non includano informazioni aggiuntive, ad esempio `IsClustered` e la versione. Questo dipende da come è stato ottenuto l'elenco. I server elencati tramite il servizio SQL Browser presenteranno maggiori dettagli rispetto a quelli rilevati tramite l'infrastruttura Windows, che elencherà solo i nomi.  
  
> [!NOTE]
>  L'enumerazione dei server è disponibile solo durante l'esecuzione in attendibilità totale. Gli assembly in esecuzione in un ambiente parzialmente attendibile non potranno usarla, anche se hanno l'autorizzazione CAS (sicurezza dall'accesso di codice) <xref:Microsoft.Data.SqlClient.SqlClientPermission>.  
  
SQL Server fornisce informazioni per <xref:System.Data.Sql.SqlDataSourceEnumerator> tramite l'uso di un servizio Windows esterno denominato SQL Browser. Questo servizio è abilitato per impostazione predefinita, ma gli amministratori possono disattivarlo o disabilitarlo, rendendo invisibile l'istanza del server a questa classe.  
  
## <a name="example"></a>Esempio  
L'applicazione console seguente consente di recuperare informazioni su tutte le istanze di SQL Server visibili e di visualizzarle nella finestra della console.  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
