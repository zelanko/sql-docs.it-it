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
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d6c83ffd407a9b27a04b254fb3e9e5673a600417
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452207"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>Enumerazione di istanze di SQL Server (ADO.NET)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server consente alle applicazioni di trovare SQL Server istanze all'interno della rete corrente. La classe <xref:System.Data.Sql.SqlDataSourceEnumerator> espone queste informazioni allo sviluppatore di applicazioni, fornendo una <xref:System.Data.DataTable> contenente le informazioni su tutti i server visibili. La tabella restituita include un elenco di istanze di server disponibili in rete che corrisponde all'elenco fornito quando un utente tenta di creare una nuova connessione ed espande l'elenco a discesa contenente tutti i server disponibili nella finestra di dialogo **Proprietà connessione**. I risultati visualizzati non sono sempre completi.  
  
> [!NOTE]
>  Come per la maggior parte dei servizi Windows, è preferibile eseguire il servizio SQL Browser con i privilegi minimi possibili. Per altre informazioni sul servizio SQL Browser e su come gestirne il comportamento, vedere la documentazione online di SQL Server.  
  
## <a name="retrieving-an-enumerator-instance"></a>Recupero di un'istanza di enumeratore  
Per recuperare la tabella che contiene le informazioni sulle istanze di SQL Server disponibili, è prima necessario recuperare un enumeratore usando la proprietà condivisa/statica <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A>:  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
Una volta recuperato l'istanza statica, è possibile chiamare il metodo <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>, che restituisce un <xref:System.Data.DataTable> contenente informazioni sui server disponibili:  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
La tabella restituita dalla chiamata al metodo contiene le colonne seguenti, tutte contenenti `string` valori:  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**ServerName**|Nome del server.|  
|**InstanceName**|Nome dell'istanza del server. Blank se il server è in esecuzione come istanza predefinita.|  
|**IsClustered**|Indica se il server fa parte di un cluster.|  
|**Version**|Versione del server Esempio:<br /><br /> -   9.00.x (SQL Server 2005)<br />-10.0. XX (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-11.0. XX (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>Limitazioni di enumerazione  
È possibile che non siano elencati tutti i server disponibili. L'elenco può variare in base a fattori quali i timeout e il traffico di rete. Questo può fare in modo che l'elenco sia diverso per due chiamate consecutive. Verranno elencati solo i server nella stessa rete. I pacchetti broadcast in genere non attraversano i router, motivo per cui potrebbe non essere visualizzato un server elencato, ma sarà stabile tra le chiamate.  
  
È possibile che i server elencati non dispongano di informazioni aggiuntive, ad esempio `IsClustered` e Version. Questo dipende dal modo in cui è stato ottenuto l'elenco. I server elencati tramite il servizio SQL Browser presenteranno maggiori dettagli rispetto a quelli rilevati tramite l'infrastruttura Windows, che elencherà solo i nomi.  
  
> [!NOTE]
>  L'enumerazione server è disponibile solo quando è in esecuzione in attendibilità totale. Gli assembly in esecuzione in un ambiente parzialmente attendibile non saranno in grado di usarli, anche se hanno <xref:Microsoft.Data.SqlClient.SqlClientPermission> autorizzazione di sicurezza dall'accesso di codice (CAS).  
  
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
