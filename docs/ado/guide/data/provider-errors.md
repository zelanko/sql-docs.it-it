---
title: Errori del provider | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18370885fedb106f02c9b404ea946680aa048b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911370"
---
# <a name="provider-errors"></a>Errori del provider
Quando si verifica un errore del provider, viene restituito un errore di run-time di -2147467259. Quando si riceve questo errore, verificare i **errori** raccolta dell'oggetto attivo **connessione** oggetto, che contiene uno o più errori che descrive quanto accaduto.  
  
## <a name="the-ado-errors-collection"></a>La raccolta di errori ADO  
 Dato che una particolare operazione ADO possa produrre più errori del provider, ADO espone una raccolta di oggetti di errore tramite il **connessione** oggetto. Questa raccolta non contiene oggetti se un'operazione si conclude correttamente e contiene uno o più **errore** oggetti se si è verificato e il provider ha generato una o più errori. Esaminare ogni oggetto error per determinare la causa esatta dell'errore.  
  
 Non appena è terminata la gestione degli eventuali errori che si sono verificati, è possibile cancellare la raccolta chiamando il **cancellare** (metodo). È particolarmente importante cancellare in modo esplicito il **errori** raccolta prima di chiamare le **Risincronizza**, **UpdateBatch**, o **CancelBatch**metodo su un **Recordset** oggetto, il **Open** metodo su un **connessione** dell'oggetto, o impostare il **filtro** proprietà in un **Recordset** oggetto. Cancellando la raccolta in modo esplicito, è possibile essere certi che eventuali **errore** oggetti nella raccolta non sono rimasti da un'operazione precedente.  
  
 Alcune operazioni possono generare avvisi a errori. Gli avvisi sono rappresentati anche dalle **errore** gli oggetti nel **errori** raccolta. Quando un provider aggiunge un avviso alla raccolta, non genera un errore di run-time. Controllare la **conteggio** proprietà delle **errori** insieme per determinare se un avviso è stato generato da una determinata operazione. Se il conteggio è uno o più, un **errore** oggetto è stato aggiunto alla raccolta. Non appena è stato possibile determinare che il **errori** insieme contiene errori o avvisi, è possibile scorrere la raccolta e recuperare informazioni su ognuna **errore** oggetti in esso contenuti. L'esempio breve Visual Basic seguente illustra questo processo:  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 La routine di gestione degli errori include un' **per ogni** ciclo che esamina ogni oggetto nella **errori** raccolta. In questo esempio, accumula un messaggio per la visualizzazione. In un programma funzionante, è necessario scrivere codice per eseguire un'attività appropriata per ogni errore, quale la chiusura di tutto aprire i file e l'arresto del programma in modo ordinato.  
  
## <a name="the-error-object"></a>L'oggetto Error  
 Esaminando un **errore** dell'oggetto è possibile determinare l'errore si è verificato e più importante, individuare l'applicazione o l'oggetto che ha causato l'errore. Il **errore** oggetto presenta le proprietà seguenti:  
  
|Nome proprietà|Descrizione|  
|-------------------|-----------------|  
|**Descrizione**|Una descrizione di testo dell'errore che si è verificato.|  
|**HelpContext, HelpFile**|Fa riferimento al file di argomento della Guida e supporto che contiene una descrizione dell'errore che si è verificato.|  
|**NativeError**|Il numero di errore specifico del provider.|  
|**Numero**|Valore Long Integer che rappresenta il numero (elencati nel **ErrorValueEnum**) dell'errore che si è verificato.|  
|**Origine**|Indica il nome dell'oggetto o applicazione che ha generato un errore.|  
|**SQLState**|Un codice di errore di cinque caratteri che il provider restituisce durante il processo di un'istruzione SQL.|  
  
 L'oggetto ADO **errore** oggetti sono molto simili al standard di Visual Basic **Err** oggetto. Le proprietà descrivono l'errore che si sono verificati. Oltre al numero dell'errore, si ricevono inoltre due tipi correlati di informazioni. Il **NativeError** proprietà contiene un numero di errore specifico del provider in uso. Nell'esempio precedente, il provider è il Provider Microsoft OLE DB per SQL Server, pertanto **NativeError** conterrà errori specifici di SQL Server. Il **SQLState** proprietà ha un codice di cinque lettere che descrive un errore in un'istruzione SQL.  
  
## <a name="event-related-errors"></a>Errori relativi agli eventi  
 Il **errore** oggetto viene usato anche quando si verificano errori relativi agli eventi. È possibile determinare se si è verificato un errore nel processo che ha generato un evento di ADO controllando il **errore** oggetto passato come parametro di evento.  
  
 Se l'operazione che causa un evento si conclude correttamente, il *adStatus* parametro del gestore dell'evento verrà impostato su *adStatusOK*. D'altra parte, se l'operazione che ha generato l'evento ha avuto esito negativo, il *adStatus* parametro è impostato su *adStatusErrorsOccurred*. In tal caso, il *pError* parametro conterrà un' **errore** oggetto che descrive l'errore.
