---
title: Rilevamento di un file flat vuoto con l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 860fb5e2b33c4e68e8f7321eff6325639f5757db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112298"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>Rilevamento di un file flat vuoto con l'attività Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'origine file flat non determina se un file flat contiene righe di dati prima di tentare di elaborarlo. È possibile migliorare l'efficienza di un pacchetto, specialmente di un pacchetto che scorre numerosi file flat, ignorando i file che non contengono alcuna riga di dati. L'attività Script consente di cercare un file flat vuoto prima che il pacchetto inizi a elaborare il flusso di dati.  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrizione  
 L'esempio seguente usa i metodi dello spazio dei nomi **System.IO** per testare il file flat specificato in una gestione connessione file flat per determinare se il file è vuoto o se contiene solo le righe non di dati previste, ad esempio intestazioni di colonna o una riga vuota. Lo script prima controlla la dimensione del file. Se la dimensione è pari a zero byte, significa che il file è vuoto. Se la dimensione del file è superiore a zero, lo script legge le righe dal file finché non sussistono più righe o finché il numero di righe supera il numero previsto di righe non di dati. Se il numero di righe nel file è minore o uguale al numero previsto di righe non di dati, il file è considerato vuoto. Il risultato viene restituito come valore booleano in una variabile dell'utente, il cui valore può essere utilizzato per la diramazione nel flusso di controllo del pacchetto. Anche il metodo **FireInformation** visualizza il risultato nella finestra **Output** di[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
#### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Creare e configurare una gestione connessione file flat denominata **EmptyFlatFileTest**.  
  
2.  Creare una variabile di tipo integer denominata `FFNonDataRows` e impostarne il valore sul numero di righe non di dati previsto nel file flat.  
  
3.  Creare una variabile booleana denominata `FFIsEmpty`.  
  
4.  Aggiungere la variabile `FFNonDataRows` alla proprietà **ReadOnlyVariables** dell'attività Script.  
  
5.  Aggiungere la variabile `FFIsEmpty` alla proprietà **ReadWriteVariables** dell'attività Script.  
  
6.  Nel codice importare lo spazio dei nomi **System.IO**.  
  
 Se si scorrono i file con un enumeratore Foreach File, anziché utilizzare una sola gestione connessione file flat, sarà necessario modificare il codice di esempio seguente per ottenere il nome e il percorso del file dalla variabile nella quale il valore enumerato è archiviato anziché dalla gestione connessione.  
  
### <a name="code"></a>codice  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di attività Script](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
