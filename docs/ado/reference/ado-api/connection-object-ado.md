---
description: Oggetto Connection (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 68b6a8dd0b0cd75f511c042981672444d9b3bcb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444513"
---
# <a name="connection-object-ado"></a>Oggetto Connection (ADO)
Rappresenta una connessione aperta a un'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
 Un oggetto **Connection** rappresenta una sessione univoca con un'origine dati. In un sistema di database client/server, può essere equivalente a una connessione di rete effettiva al server. A seconda della funzionalità supportata dal provider, alcune raccolte, metodi o proprietà di un oggetto **connessione** potrebbero non essere disponibili.  
  
 Con le raccolte, i metodi e le proprietà di un oggetto **connessione** , è possibile eseguire le operazioni seguenti:  
  
-   Configurare la connessione prima di aprirla con le proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)e [mode](../../../ado/reference/ado-api/mode-property-ado.md) . **ConnectionString** è la proprietà predefinita dell'oggetto **Connection** .  
  
-   Impostare la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) su client per richiamare il [servizio Microsoft Cursor per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), che supporta gli aggiornamenti in batch.  
  
-   Impostare il database predefinito per la connessione con la proprietà [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) .  
  
-   Imposta il livello di isolamento per le transazioni aperte sulla connessione con la proprietà [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) .  
  
-   Specificare un provider OLE DB con la proprietà [provider](../../../ado/reference/ado-api/provider-property-ado.md) .  
  
-   Stabilire e successivamente interrompere la connessione fisica all'origine dati con i metodi [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) e [Close](../../../ado/reference/ado-api/close-method-ado.md) .  
  
-   Eseguire un comando sulla connessione con il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) e configurare l'esecuzione con la proprietà [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) .  
  
    > [!NOTE]
    >  Per eseguire una query senza usare un oggetto Command, passare una stringa di query al metodo **Execute** di un oggetto **Connection** . Tuttavia, è necessario un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) quando si desidera salvare in modo permanente il testo del comando ed eseguirlo di nuovo oppure utilizzare parametri di query.  
  
-   Gestire le transazioni sulla connessione aperta, incluse le transazioni nidificate se supportate dal provider, con i metodi [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)e [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) e la proprietà [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) .  
  
-   Esaminare gli errori restituiti dall'origine dati con la raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) .  
  
-   Leggere la versione dall'implementazione ADO utilizzata con la proprietà [Version](../../../ado/reference/ado-api/version-property-ado.md) .  
  
-   Ottenere informazioni sullo schema relative al database con il metodo [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) .  
  
 È possibile creare oggetti **connessione** indipendentemente da qualsiasi altro oggetto definito in precedenza.  
  
 È possibile eseguire comandi denominati o stored procedure come se fossero metodi nativi su un oggetto **Connection** , come illustrato nella sezione successiva. Quando un comando denominato ha lo stesso nome di un stored procedure, richiamare "Native Method Call" in un oggetto **Connection** sempre eseguire il comando denominato invece della stored procedure.  
  
> [!NOTE]
>  Non usare questa funzionalità (chiamando un comando denominato o stored procedure come se fosse un metodo nativo sull'oggetto **Connection** ) in un'applicazione Microsoft® .NET Framework, perché l'implementazione sottostante della funzionalità è in conflitto con il modo in cui il .NET Framework interagisce con com.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Eseguire un comando come metodo nativo di un oggetto Connection  
 Per eseguire un comando, assegnare un nome al comando utilizzando la proprietà [nome](../../../ado/reference/ado-api/name-property-ado.md) oggetto **comando** . Impostare la proprietà **ActiveConnection** dell'oggetto **Command** sulla connessione. Eseguire quindi un'istruzione in cui il nome del comando viene usato come se fosse un metodo nell'oggetto **Connection** , seguito da qualsiasi parametro e da un oggetto **Recordset** se vengono restituite righe. Impostare le proprietà del **Recordset** per personalizzare il **Recordset**risultante. Ad esempio:  
  
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
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Eseguire un stored procedure come metodo nativo di un oggetto Connection  
 Per eseguire una stored procedure, emettere un'istruzione in cui il nome del stored procedure viene usato come se fosse un metodo nell'oggetto **Connection** , seguito da qualsiasi parametro. ADO effettuerà una "ipotesi migliore" dei tipi di parametro. Ad esempio:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 L'oggetto **Connection** è sicuro per lo scripting.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Connection](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Appendice A: Provider](../../../ado/guide/appendixes/appendix-a-providers.md)
