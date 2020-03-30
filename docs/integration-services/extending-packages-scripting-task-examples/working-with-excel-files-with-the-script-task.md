---
title: Uso di file di Excel con l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9386f146aee229eb4547ad54b4dd576fda1c0bfc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71286572"
---
# <a name="working-with-excel-files-with-the-script-task"></a>Uso di file di Excel con l'attività Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono disponibili la gestione connessione, l'origine e la destinazione Excel per l'utilizzo di dati archiviati in fogli di calcolo nel formato di file di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. Per le tecniche descritte in questo argomento si utilizza l'attività Script per ottenere informazioni sui database (file di cartelle di lavoro) e sulle tabelle (fogli di lavoro e intervalli denominati) di Excel disponibili.
  
> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
 
> [!TIP]  
>  Se si desidera creare un'attività da riusare con più pacchetti, è possibile usare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  

##  <a name="configuring-a-package-to-test-the-samples"></a><a name="configuring"></a> Configurazione di un pacchetto per testare gli esempi  
 È possibile configurare un singolo pacchetto per testare tutti gli esempi riportati in questo argomento. Negli esempi vengono utilizzate molte variabili del pacchetto e classi di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>Per configurare un pacchetto per l'utilizzo con gli esempi di questo argomento  
  
1.  Creare un nuovo progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e aprire il pacchetto predefinito per la modifica.  
  
2.  **Variabili**. Aprire la finestra **Variabili** e definire le variabili seguenti:  
  
    -   `ExcelFile`, del tipo **String**. Immettere il percorso completo e il nome del file di una cartella di lavoro di Excel esistente.  
  
    -   `ExcelTable`, del tipo **String**. Immettere il nome di un foglio di lavoro o di un intervallo denominato esistente nella cartella di lavoro specificata nel valore della variabile `ExcelFile`. Per questo valore viene applicata la distinzione tra maiuscole e minuscole.  
  
    -   `ExcelFileExists` del tipo**Boolean**.  
  
    -   `ExcelTableExists` del tipo**Boolean**.  
  
    -   `ExcelFolder`, del tipo **String**. Immettere il percorso completo di una cartella che contiene almeno una cartella di lavoro di Excel.  
  
    -   `ExcelFiles`, del tipo **Object**.  
  
    -   `ExcelTables`, del tipo **Object**.  
  
3.  **Istruzioni Imports**. Per la maggior parte degli esempi di codice, è necessario importare uno o entrambi i seguenti spazi dei nomi di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] all'inizio del file script:  
  
    -   **System.IO**, per le operazioni di file system.  
  
    -   **System.Data.OleDb**, per aprire i file di Excel come origini dati.  
  
4.  **Riferimenti**. Gli esempi di codice che leggono informazioni sullo schema da file di Excel richiedono un riferimento aggiuntivo allo spazio dei nomi **System.Xml** nel progetto di script.  
  
5.  Impostare il linguaggio di scripting predefinito per il componente Script usando l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni**. Per ulteriori informazioni, vedere [General Page](../general-page-of-integration-services-designers-options.md).  
  
##  <a name="example-1-description-check-whether-an-excel-file-exists"></a><a name="example1"></a> Descrizione dell'esempio 1: verificare l'esistenza di un file di Excel  
 In questo esempio viene determinato se il file della cartella di lavoro di Excel specificato nella variabile `ExcelFile` esiste, quindi il valore booleano della variabile `ExcelFileExists` viene impostato sul risultato. È possibile utilizzare questo valore booleano per la diramazione nel flusso di lavoro del pacchetto.  
  
### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Aggiungere una nuova attività Script al pacchetto e impostarne il nome su **ExcelFileExists**.  
  
2.  Nella scheda **Script** di **Editor attività Script** fare clic su **ReadOnlyVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelFile**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile **ExcelFile** nella finestra di dialogo **Seleziona variabili**.  
  
3.  Fare clic su **ReadWriteVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelFileExists**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile **ExcelFileExists** nella finestra di dialogo **Seleziona variabili**.  
  
4.  Fare clic su **Modifica script** per aprire l'editor di script.  
  
5.  Aggiungere un'istruzione **Imports** per lo spazio dei nomi **System.IO** all'inizio del file di script.  
  
6.  Aggiungere il codice seguente.  
  
### <a name="example-1-code"></a>Codice dell'esempio 1  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example-2-description-check-whether-an-excel-table-exists"></a><a name="example2"></a> Descrizione dell'esempio 2: verificare l'esistenza di una tabella di Excel  
 In questo esempio viene determinato se il foglio di lavoro o l'intervallo denominato di Excel specificato nella variabile `ExcelTable` esiste nel file della cartella di lavoro di Excel specificato nella variabile `ExcelFile`, quindi il valore booleano della variabile `ExcelTableExists` viene impostato sul risultato. È possibile utilizzare questo valore booleano per la diramazione nel flusso di lavoro del pacchetto.  
  
### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Aggiungere una nuova attività Script al pacchetto e impostarne il nome su **ExcelTableExists**.  
  
2.  Nella scheda **Script** di **Editor attività Script** fare clic su **ReadOnlyVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelTable** e **ExcelFile** separati da virgole **.**  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare le variabili **ExcelTable** e **ExcelFile** nella finestra di dialogo **Seleziona variabili**.  
  
3.  Fare clic su **ReadWriteVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelTableExists**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile **ExcelTableExists** nella finestra di dialogo **Seleziona variabili**.  
  
4.  Fare clic su **Modifica script** per aprire l'editor di script.  
  
5.  Aggiungere un riferimento all'assembly **System.Xml** nel progetto di script.  
  
6.  Aggiungere istruzioni **Imports** per gli spazi dei nomi **System.IO** e **System.Data.OleDb** all'inizio del file di script.  
  
7.  Aggiungere il codice seguente.  
  
### <a name="example-2-code"></a>Codice dell'esempio 2  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 12.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 12.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example-3-description-get-a-list-of-excel-files-in-a-folder"></a><a name="example3"></a> Descrizione dell'esempio 3: ottenere un elenco dei file di Excel in una cartella  
 In questo esempio l'elenco dei file di Excel trovati nella cartella specificata nel valore della variabile `ExcelFolder` viene inserito in una matrice, che viene quindi copiata nella variabile `ExcelFiles`. È possibile utilizzare l'enumeratore Foreach From Variable per scorrere i file nella matrice.  
  
### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Aggiungere una nuova attività Script al pacchetto e impostarne il nome su **GetExcelFiles**.  
  
2.  Nella scheda **Script** di **Editor attività Script** fare clic su **ReadOnlyVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelFolder**  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile ExcelFolder nella finestra di dialogo **Seleziona variabili**.  
  
3.  Fare clic su **ReadWriteVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelFiles**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile ExcelFiles nella finestra di dialogo **Seleziona variabili**.  
  
4.  Fare clic su **Modifica script** per aprire l'editor di script.  
  
5.  Aggiungere un'istruzione **Imports** per lo spazio dei nomi **System.IO** all'inizio del file di script.  
  
6.  Aggiungere il codice seguente.  
  
### <a name="example-3-code"></a>Codice dell'esempio 3  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xlsx"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xlsx";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>Soluzione alternativa  
 Anziché utilizzare un'attività Script per raccogliere un elenco di file di Excel in una matrice, è anche possibile utilizzare l'enumeratore ForEach File per scorrere tutti i file di Excel presenti in una cartella. Per altre informazioni, vedere [Esecuzione di un ciclo su file e tabelle di Excel usando un contenitore Ciclo Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="example-4-description-get-a-list-of-tables-in-an-excel-file"></a><a name="example4"></a> Descrizione dell'esempio 4: ottenere un elenco di tabelle in un file di Excel  
 In questo esempio l'elenco dei fogli di lavoro e degli intervalli denominati trovati nel file della cartella di lavoro di Excel specificata dal valore della variabile `ExcelFile` viene inserito in una matrice, che viene quindi copiata nella variabile `ExcelTables`. È possibile utilizzare l'enumeratore Foreach From Variable per scorrere le tabelle nella matrice.  
  
> [!NOTE]  
>  Nell'elenco di tabelle di una cartella di Excel sono inclusi sia i fogli di lavoro (con suffisso $) sia gli intervalli denominati. Se è necessario applicare un filtro all'elenco per individuare solo fogli di lavoro o solo intervalli denominati, può essere necessario scrivere codice aggiuntivo a tale scopo.  
  
### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Aggiungere una nuova attività Script al pacchetto e impostarne il nome su **GetExcelTables**.  
  
2.  Nella scheda **Script** di **Editor attività Script** fare clic su **ReadOnlyVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelFile**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile ExcelFile nella finestra di dialogo **Seleziona variabili**.  
  
3.  Fare clic su **ReadWriteVariables** e immettere il valore della proprietà usando uno dei metodi seguenti:  
  
    -   Digitare **ExcelTables**.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare la variabile ExcelTables nella finestra di dialogo **Seleziona variabili**.  
  
4.  Fare clic su **Modifica script** per aprire l'editor di script.  
  
5.  Aggiungere un riferimento allo spazio dei nomi **System.Xml** nel progetto di script.  
  
6.  Aggiungere un'istruzione **Imports** per lo spazio dei nomi **System.Data.OleDb** all'inizio del file di script.  
  
7.  Aggiungere il codice seguente.  
  
### <a name="example-4-code"></a>Codice dell'esempio 4  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 12.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 12.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>Soluzione alternativa  
 Anziché utilizzare un'attività Script per raccogliere un elenco delle tabelle di Excel in una matrice, è anche possibile utilizzare ForEach ADO.NET Schema Rowset Enumerator per scorrere tutte le tabelle, ovvero fogli di lavoro e intervalli denominati, nel file di una cartella di lavoro di Excel. Per altre informazioni, vedere [Esecuzione di un ciclo su file e tabelle di Excel usando un contenitore Ciclo Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="displaying-the-results-of-the-samples"></a><a name="testing"></a> Visualizzazione dei risultati degli esempi  
 Se tutti gli esempi di questo argomento sono stati configurati nello stesso pacchetto, è possibile connettere tutte le attività Script a un'attività Script aggiuntiva che visualizza l'output di tutti gli esempi.  
  
### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>Per configurare un'attività Script per visualizzare l'output degli esempi di questo argomento  
  
1.  Aggiungere una nuova attività Script al pacchetto e impostarne il nome su **DisplayResults**.  
  
2.  Connettere i quattro esempi di attività Script l'uno all'altro, in modo che ogni attività venga eseguita al completamento di quella precedente, quindi connettere il quarto esempio di attività all'attività **DisplayResults**.  
  
3.  Aprire l'attività **DisplayResults** in **Editor attività Script**.  
  
4.  Nella scheda **Script** fare clic su **ReadOnlyVariables** e usare uno dei metodi seguenti per aggiungere tutte le sette variabili elencate in [Configurazione di un pacchetto per testare gli esempi](#configuring):  
  
    -   Digitare i nomi di ogni variabile separati da virgole.  
  
         -oppure-  
  
    -   Fare clic sul pulsante con i puntini di sospensione ( **...** ) accanto al campo della proprietà e selezionare le variabili nella finestra di dialogo **Seleziona variabili**.  
  
5.  Fare clic su **Modifica script** per aprire l'editor di script.  
  
6.  Aggiungere istruzioni **Imports** per gli spazi dei nomi **Microsoft.VisualBasic** e **System.Windows.Forms** all'inizio del file di script.  
  
7.  Aggiungere il codice seguente.  
  
8.  Eseguire il pacchetto ed esaminare i risultati visualizzati in una finestra di messaggio.  
  
### <a name="code-to-display-the-results"></a>Codice per visualizzare i risultati  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
 [Esecuzione di un ciclo su file e tabelle di Excel usando un contenitore Ciclo Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
