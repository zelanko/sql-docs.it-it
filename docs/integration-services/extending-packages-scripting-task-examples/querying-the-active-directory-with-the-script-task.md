---
title: Esecuzione di query su Active Directory tramite l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14fa2d0602f0c358cd400e0734e567e853a6db85
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286820"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>Esecuzione di query su Active Directory tramite l'attività Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Le applicazioni di elaborazione di dati aziendali, ad esempio i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], devono in genere elaborare i dati in modo diverso a seconda del grado, della posizione o di altre caratteristiche dei dipendenti archiviati in Active Directory. Active Directory è un servizio directory di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows che rende disponibile un archivio centralizzato di metadati sugli utenti e su altre risorse dell'organizzazione, come computer e stampanti. Lo spazio dei nomi **System.DirectoryServices** in Microsoft .NET Framework fornisce le classi da usare con Active Directory per indirizzare il flusso di lavoro dell'elaborazione dei dati in base alle informazioni archiviate.  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono recuperati il nome, la posizione e il numero di telefono di un dipendente da Active Directory in base al valore della variabile `email`, che contiene l'indirizzo di posta elettronica del dipendente. I vincoli di precedenza del pacchetto possono utilizzare le informazioni recuperate per determinare, ad esempio, se inviare un messaggio di posta elettronica con priorità bassa o una pagina con priorità alta, in base alla posizione del dipendente.  
  
#### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Creare le tre variabili stringa `email`, `name` e `title`. Immettere un indirizzo di posta elettronica aziendale valido come valore della variabile `email`.  
  
2.  Nella pagina **Script** dell'**Editor attività Script** aggiungere la variabile `email` alla proprietà **ReadOnlyVariables**.  
  
3.  Aggiungere le variabili `name` e `title` alla proprietà **ReadWriteVariables**.  
  
4.  Nel progetto di script aggiungere un riferimento allo spazio dei nomi **System.DirectoryServices**.  
  
5.  . Nel codice usare un'istruzione **Imports** per importare lo spazio dei nomi **DirectoryServices**.  
  
> [!NOTE]  
>  Per eseguire correttamente lo script, è necessario che l'azienda utilizzi Active Directory nella propria rete e archivi le informazioni sui dipendenti utilizzati nell'esempio.  
  
### <a name="code"></a>codice  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Articolo tecnico [Processing Active Directory Information in SSIS](https://go.microsoft.com/fwlink/?LinkId=199588) (Elaborazione di informazioni di Active Directory in SSIS) nel sito Web social.technet.microsoft.com  
  
  
