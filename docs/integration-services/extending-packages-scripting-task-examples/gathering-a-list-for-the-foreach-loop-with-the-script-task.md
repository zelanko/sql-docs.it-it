---
title: Raccolta di un elenco per il ciclo ForEach con l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], Foreach loops
- Script task [Integration Services], examples
- SSIS Script task, Foreach loops
ms.assetid: 694f0462-d0c5-4191-b64e-821b1bdef055
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 82856b272e4799fc06929fe4f2d153320f879f0e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270784"
---
# <a name="gathering-a-list-for-the-foreach-loop-with-the-script-task"></a>Raccolta di un elenco per il ciclo ForEach con l'attività Script
  L'enumeratore Foreach da variabile enumera gli elementi in un elenco passato in una variabile ed esegue le stesse attività su ogni elemento. È possibile utilizzare codice personalizzato in un'attività Script per popolare un elenco a questo scopo. Per altre informazioni sull'enumeratore, vedere [Contenitore ciclo Foreach](../../integration-services/control-flow/foreach-loop-container.md).  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono usati i metodi dello spazio dei nomi **System.IO** per raccogliere un elenco di cartelle di lavoro di Excel sul computer, più o meno recenti di un numero di giorni specificati dall'utente in una variabile. Nelle directory dell'unità C viene eseguita una ricerca ricorsiva dei file con estensione xls e viene esaminata la data dell'ultima modifica di ogni file per determinare se il file fa parte dell'elenco. I file risultanti vengono aggiunti a un oggetto **ArrayList** che viene quindi salvato in una variabile per uso successivo in un contenitore Ciclo Foreach. Il contenitore Ciclo Foreach è configurato per utilizzare l'enumeratore Foreach da variabile.  
  
> [!NOTE]  
>  La variabile che si usa con l'enumeratore Foreach da variabile deve essere di tipo **Oggetto**. L'oggetto inserito nella variabile deve implementare una delle interfacce seguenti: **System.Collections.IEnumerable**, **System.Runtime.InteropServices.ComTypes.IEnumVARIANT**, **System.ComponentModel IListSource** o **Microsoft.SqlServer.Dts.Runtime.Wrapper.ForEachEnumeratorHost**. Viene usato comunemente un oggetto **Array** o **ArrayList**. **ArrayList** richiede un riferimento e un'istruzione **Imports** per lo spazio dei nomi **System.Collections**.  
  
 È possibile provare a utilizzare questa attività utilizzando valori diversi positivi e negativi per la variabile del pacchetto `FileAge`. È possibile, ad esempio, immettere 5 per cercare i file creati negli ultimi cinque giorni oppure immettere -3 per cercare i file creati più di tre giorni fa. L'esecuzione di questa attività può richiedere alcuni minuti su un'unità con numerose cartelle in cui eseguire la ricerca.  
  
#### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Creare una variabile del pacchetto denominata `FileAge` di tipo integer e immettere un valore integer positivo o negativo. Quando il valore è positivo, il codice cerca i file più recenti del numero specificato di giorni. Quando invece è negativo, cerca i file più obsoleti del numero specificato di giorni.  
  
2.  Creare una variabile del pacchetto denominata `FileList` di tipo **Oggetto** per ricevere l'elenco di file raccolti dall'attività Script per un uso successivo da parte dell'enumeratore Foreach da variabile.  
  
3.  Aggiungere la variabile `FileAge` alla proprietà **ReadOnlyVariables** dell'attività Script e aggiungere la variabile `FileList` alla proprietà **ReadWriteVariables**.  
  
4.  Importare nel codice lo spazio dei nomi **System.Collections** e lo spazio dei nomi **System.IO**.  
  
### <a name="code"></a>codice  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Collections  
Imports System.IO  
  
Public Class ScriptMain  
  
  Private Const FILE_AGE As Integer = -50  
  
  Private Const FILE_ROOT As String = "C:\"  
  Private Const FILE_FILTER As String = "*.xls"  
  
  Private isCheckForNewer As Boolean = True  
  Dim fileAgeLimit As Integer  
  Private listForEnumerator As ArrayList  
  
  Public Sub Main()  
  
    fileAgeLimit = DirectCast(Dts.Variables("FileAge").Value, Integer)  
  
    ' If value provided is positive, we want files NEWER THAN n days.  
    '  If negative, we want files OLDER THAN n days.  
    If fileAgeLimit < 0 Then  
      isCheckForNewer = False  
    End If  
    ' Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit)  
  
    listForEnumerator = New ArrayList  
  
    GetFilesInFolder(FILE_ROOT)  
  
    ' Return the list of files to the variable  
    '  for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: " & listForEnumerator.Count.ToString, "Results", Windows.Forms.MessageBoxButtons.OK, Windows.Forms.MessageBoxIcon.Information)  
    Dts.Variables("FileList").Value = listForEnumerator  
  
    Dts.TaskResult = ScriptResults.Success  
  
  End Sub  
  
  Private Sub GetFilesInFolder(ByVal folderPath As String)  
  
    Dim localFiles() As String  
    Dim localFile As String  
    Dim fileChangeDate As Date  
    Dim fileAge As TimeSpan  
    Dim fileAgeInDays As Integer  
    Dim childFolder As String  
  
    Try  
      localFiles = Directory.GetFiles(folderPath, FILE_FILTER)  
      For Each localFile In localFiles  
        fileChangeDate = File.GetLastWriteTime(localFile)  
        fileAge = DateTime.Now.Subtract(fileChangeDate)  
        fileAgeInDays = fileAge.Days  
        CheckAgeOfFile(localFile, fileAgeInDays)  
      Next  
  
      If Directory.GetDirectories(folderPath).Length > 0 Then  
        For Each childFolder In Directory.GetDirectories(folderPath)  
          GetFilesInFolder(childFolder)  
        Next  
      End If  
  
    Catch  
      ' Ignore exceptions on special folders such as System Volume Information.  
    End Try  
  
  End Sub  
  
  Private Sub CheckAgeOfFile(ByVal localFile As String, ByVal fileAgeInDays As Integer)  
  
    If isCheckForNewer Then  
      If fileAgeInDays <= fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    Else  
      If fileAgeInDays > fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    End If  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Math;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Collections;  
using System.IO;  
  
public partial class ScriptMain : Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTARTScriptObjectModelBase  
    {  
  
        private const int FILE_AGE = -50;  
  
        private const string FILE_ROOT = "C:\\";  
        private const string FILE_FILTER = "*.xls";  
  
        private bool isCheckForNewer = true;  
        int fileAgeLimit;  
        private ArrayList listForEnumerator;  
  
        public void Main()  
  {  
  
    fileAgeLimit = (int)(Dts.Variables["FileAge"].Value);  
  
    // If value provided is positive, we want files NEWER THAN n days.  
    // If negative, we want files OLDER THAN n days.  
    if (fileAgeLimit<0)  
    {  
      isCheckForNewer = false;  
    }  
    // Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit);  
  
    listForEnumerator = new ArrayList();  
  
    GetFilesInFolder(FILE_ROOT);  
  
    // Return the list of files to the variable  
    // for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: "+ listForEnumerator.Count, "Results",   
MessageBoxButtons.OK, MessageBoxIcon.Information);  
    Dts.Variables["FileList"].Value = listForEnumerator;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  
  }  
  
        private void GetFilesInFolder(string folderPath)  
        {  
  
            string[] localFiles;  
            DateTime fileChangeDate;  
            TimeSpan fileAge;  
            int fileAgeInDays;  
  
            try  
            {  
                localFiles = Directory.GetFiles(folderPath, FILE_FILTER);  
                foreach (string localFile in localFiles)  
                {  
                    fileChangeDate = File.GetLastWriteTime(localFile);  
                    fileAge = DateTime.Now.Subtract(fileChangeDate);  
                    fileAgeInDays = fileAge.Days;  
                    CheckAgeOfFile(localFile, fileAgeInDays);  
                }  
  
                if (Directory.GetDirectories(folderPath).Length > 0)  
                {  
                    foreach (string childFolder in Directory.GetDirectories(folderPath))  
                    {  
                        GetFilesInFolder(childFolder);  
                    }  
                }  
  
            }  
            catch  
            {  
                // Ignore exceptions on special folders, such as System Volume Information.  
            }  
  
        }  
  
        private void CheckAgeOfFile(string localFile, int fileAgeInDays)  
        {  
  
            if (isCheckForNewer)  
            {  
                if (fileAgeInDays <= fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
            else  
            {  
                if (fileAgeInDays > fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
  
        }  
  
    }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Contenitore Ciclo Foreach](../../integration-services/control-flow/foreach-loop-container.md)   
 [Configurare un contenitore Ciclo Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
  
  
