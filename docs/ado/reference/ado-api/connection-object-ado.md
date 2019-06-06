---
title: Oggetto Connection (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 701ced4f5e0ad511f4a1c5b39c9775e285d1f751
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695783"
---
# <a name="connection-object-ado"></a>Oggetto Connection (ADO)
Rappresenta una connessione aperta a un'origine dati.  
  
## <a name="remarks"></a>Note  
 Oggetto **connessione** oggetto rappresenta una sessione univoca con un'origine dati. In un sistema di database client/server, potrebbe essere equivalente a una connessione di rete effettivo al server. A seconda delle funzionalità supportate dal provider, alcune raccolte, metodi o proprietà di un **connessione** oggetto potrebbe non essere disponibile.  
  
 Con le raccolte, i metodi e proprietà di un **connessione** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Configurare la connessione prima di aprirlo con il [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), e [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà. **ConnectionString** è la proprietà predefinita di **connessione** oggetto.  
  
-   Impostare il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà al client per richiamare il [Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), che supporta aggiornamenti in batch.  
  
-   Impostare il database predefinito per la connessione con il [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) proprietà.  
  
-   Impostare il livello di isolamento per le transazioni aperto sulla connessione con il [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) proprietà.  
  
-   Specificare un provider OLE DB con il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà.  
  
-   Stabilire e, successivamente, interrompere la connessione fisica all'origine dati con il [aperto](../../../ado/reference/ado-api/open-method-ado-connection.md) e [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodi.  
  
-   Eseguire un comando per la connessione con il [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) metodo e configurare l'esecuzione con il [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) proprietà.  
  
    > [!NOTE]
    >  Per eseguire una query senza l'utilizzo di un oggetto comando, passare una stringa di query per il **Execute** metodo di un **connessione** oggetto. Tuttavia, un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto è obbligatorio quando si desidera salvare in modo permanente il testo del comando ed eseguirla di nuovo, oppure utilizzare i parametri di query.  
  
-   Gestire le transazioni per la connessione aperta, incluse le transazioni nidificate, se il provider di supportarle, con la [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), e [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) i metodi e le [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà.  
  
-   Esaminare gli errori restituiti dall'origine dati con il [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta.  
  
-   Leggere la versione dall'implementazione di ADO utilizzato con il [versione](../../../ado/reference/ado-api/version-property-ado.md) proprietà.  
  
-   Ottenere informazioni sullo schema relative al database con il [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) (metodo).  
  
 È possibile creare **connessione** oggetti indipendentemente da qualsiasi altro oggetto definito in precedenza.  
  
 È possibile eseguire comandi con nome o le stored procedure come se fossero metodi nativi in una **connessione** dell'oggetto, come illustrato nella sezione successiva. Quando un comando denominato ha lo stesso nome di una stored procedure, richiamare la "chiamata al metodo nativo" in un **connessione** oggetto eseguire sempre il comando denominato anziché la stored procedure.  
  
> [!NOTE]
>  Non utilizzare questa funzionalità (chiamare una stored procedure o un comando denominato come se fosse un metodo nativo sul **connessione** oggetto) in un'applicazione di Microsoft® .NET Framework, perché l'implementazione sottostante dei conflitti di funzionalità la modalità di .NET Framework interopera con COM.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Eseguire un comando come un metodo nativo di un oggetto di connessione  
 Per eseguire un comando, assegnargli un nome usando il **comandi** oggetto [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà. Impostare il **ActiveConnection** proprietà delle **comando** oggetto per la connessione. Quindi eseguire un'istruzione in cui il nome del comando viene usato come se fosse un metodo sul **connessione** oggetto, seguito da eventuali parametri e una **Recordset** se vengono restituite tutte le righe dell'oggetto. Impostare il **Recordset** delle proprietà per personalizzare l'oggetto risultante **Recordset**. Ad esempio:  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Eseguire una stored procedure come metodo nativo di un oggetto di connessione  
 Per eseguire una stored procedure, eseguire un'istruzione in cui viene usato il nome della stored procedure come se fosse un metodo sul **connessione** oggetto, seguito da eventuali parametri. ADO farà una "stima" dei tipi di parametro. Ad esempio:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 Il **connessione** oggetto è sicuro per lo scripting.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Gli eventi, metodi e proprietà dell'oggetto connessione](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors Collection (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Appendice A: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
