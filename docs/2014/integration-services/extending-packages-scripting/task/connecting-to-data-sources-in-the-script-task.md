---
title: Connessione a origini dati nell'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4464b0ca035bc19695b37aea01385f737549fec1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393059"
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>Connessione a origini dati nell'attività Script
  Le gestioni connessioni forniscono accesso a origini dati configurate nel pacchetto. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../../connection-manager/integration-services-ssis-connections.md).  
  
 L'attività Script può accedere a queste gestioni connessioni tramite la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> dell'oggetto **Dts**. Ogni gestione connessione nella raccolta <xref:Microsoft.SqlServer.Dts.Runtime.Connections> archivia informazioni su come eseguire la connessione all'origine dati sottostante.  
  
 Quando si chiama il metodo <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> di una gestione connessione, la gestione connessione si connette all'origine dati, se non è già connessa, e restituisce la connessione o le informazioni di connessione appropriate da utilizzare nel codice dell'attività Script.  
  
> [!NOTE]  
>  È necessario conoscere il tipo di connessione restituito dalla gestione connessione prima di chiamare `AcquireConnection`. Poiché l'oggetto `Option Strict` dell'attività Script è abilitato, è necessario eseguire il cast della connessione, che viene restituita come tipo `Object`, nel tipo di connessione appropriato prima dell'utilizzo.  
  
 È possibile utilizzare il metodo <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> della raccolta <xref:Microsoft.SqlServer.Dts.Runtime.Connections> restituita dalla proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> per cercare una connessione esistente prima di utilizzare la connessione nel codice.  
  
> [!IMPORTANT]  
>  Non è possibile chiamare il metodo AcquireConnection delle gestioni connessioni che restituiscono oggetti non gestiti, ad esempio la gestione connessione OLE DB e la gestione connessione Excel, nel codice gestito di un'attività Script. Tuttavia, è possibile leggere la proprietà ConnectionString di queste gestioni connessioni e connettersi all'origine dati direttamente nel codice usando la stringa di connessione con un `OledbConnection` dal **OleDb** dello spazio dei nomi.  
>   
>  Se è necessario chiamare il metodo AcquireConnection di una gestione connessione che restituisce un oggetto non gestito, usare una gestione connessione [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]. Quando si configura la gestione connessione [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] per l'utilizzo di un provider OLE DB, la connessione viene eseguita tramite il provider di dati [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] per OLE DB. In questo caso, il metodo AcquireConnection restituisce un `System.Data.OleDb.OleDbConnection` anziché un oggetto non gestito. Per configurare una gestione connessione [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] per l'uso con un'origine dati Excel, selezionare il provider OLE DB [!INCLUDE[msCoName](../../../includes/msconame-md.md)] per Jet, specificare un file di Excel e immettere `Excel 8.0` (per Excel 97 e versioni successive) come valore di **Proprietà estese** nella pagina **Tutte** della finestra di dialogo **Gestione connessione**.  
  
## <a name="connections-example"></a>Esempio di connessioni  
 Nell'esempio seguente viene illustrato come accedere alle gestioni connessioni dall'attività Script. Nell'esempio si presuppone che sia sta creata e configurata una gestione connessione [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] denominata **Test ADO.NET Connection** e una gestione connessione file flat denominata **Test Flat File Connection**. Si noti che la gestione connessione [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] restituisce un oggetto `SqlConnection` che è possibile utilizzare immediatamente per connettersi all'origine dati. La gestione connessione file flat, al contrario, restituisce solo una stringa che contiene il percorso e il nome di file. È necessario utilizzare i metodi dello spazio dei nomi `System.IO` per aprire e utilizzare il file flat.  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../connection-manager/integration-services-ssis-connections.md)   
 [Creare gestioni connessioni](../../create-connection-managers.md)  
  
  
