---
title: Raccolta di parametri (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dbfff2a8db4405e19eb448e7bd7db5c8ac236f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138617"
---
# <a name="parameters-collection-ado"></a>Raccolta Parameters (ADO)
Contiene tutti i [parametri](../../../ado/reference/ado-api/parameter-object.md) gli oggetti di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto.  
  
## <a name="remarks"></a>Note  
 Oggetto **comandi** oggetto dispone di un **parametri** raccolta costituita da **parametro** oggetti.  
  
 Usando il [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) metodo su un **comando** dell'oggetto **parametri** raccolta recupera le informazioni sui parametri di provider per la stored procedure o query con parametri specificato nella **comando** oggetto. Alcuni provider di servizi non supportano chiamate a stored procedure o le query con parametri. chiama il **aggiornare** metodo sul **parametri** raccolta quando si usa un provider di questo tipo verrà restituito un errore.  
  
 Se non è stato definito il proprio **parametro** gli oggetti e si accede il **parametri** raccolta prima di chiamare il **Aggiorna** metodo ADO chiama automaticamente il metodo e popolare la raccolta per l'utente.  
  
 È possibile ridurre al minimo le chiamate al provider per migliorare le prestazioni se si conoscono le proprietà dei parametri associati con la stored procedure o query con parametri che si desidera chiamare. Usare la [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) metodo per creare **parametro** oggetti con le impostazioni di proprietà appropriata e usare il [Append](../../../ado/reference/ado-api/append-method-ado.md) metodo a cui aggiungere i il  **Parametri** raccolta. Ciò consente di impostare e restituire i valori dei parametri senza la necessità di chiamare il provider per le informazioni sui parametri. Se si scrive in un provider che non fornisce informazioni sui parametri, è necessario popolare manualmente le **parametri** insieme utilizzando questo metodo per essere in grado di utilizzare i parametri. Usare la [eliminare](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) metodo per rimuovere **parametro** oggetti dal **parametri** insieme, se necessario.  
  
 Gli oggetti nel **parametri** raccolta di un **Recordset** passare dall'ambito (pertanto diventi non disponibile) quando il **Recordset** viene chiuso.  
  
 Quando si chiama una stored procedure con **comando**, il parametro di valore restituito/output di una stored procedure viene recuperato come indicato di seguito:  
  
1.  Quando si chiama una stored procedure che non ha parametri, il **aggiornare** metodo sulle **parametri** raccolta deve essere chiamata prima di chiamare il **Execute** metodo sul **Comando** oggetto.  
  
2.  Quando si chiama una stored procedure con parametri e l'aggiunta in modo esplicito un parametro per il **parametri** raccolta con **Append**, deve essere aggiunto il parametro di valore restituito/output per il **Parametri** raccolta. Il valore restituito deve essere aggiunto prima di tutto per il **parametri** raccolta. Uso **Append** per aggiungere gli altri parametri nel **parametri** insieme nell'ordine di definizione. Ad esempio, la stored procedure SPWithParam include due parametri. Il primo parametro, *InParam*, è un parametro di input definiti come adVarChar (20) e il secondo parametro *OutParam*, è un parametro di output definito come adVarChar (20). È possibile recuperare il parametro di valore restituito/output con il codice seguente.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  Quando si chiama una stored procedure con parametri e configurazione dei parametri chiamando il **elemento** metodo sulle **parametri** raccolta, il parametro di valore restituito/output della stored procedure può possibile recuperarne il **parametri** raccolta. Ad esempio, la stored procedure SPWithParam include due parametri. Il primo parametro, *InParam*, è un parametro di input definiti come adVarChar (20) e il secondo parametro *OutParam*, è un parametro di output definito come adVarChar (20). È possibile recuperare il parametro di valore restituito/output con il codice seguente.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà di raccolta dei parametri, metodi ed eventi](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Metodo CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)
