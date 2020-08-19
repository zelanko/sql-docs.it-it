---
description: Oggetto Command (ADO)
title: Oggetto Command (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: rothja
ms.author: jroth
ms.openlocfilehash: b53f70c5f9a0da139346865b67df57a069b03e80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450883"
---
# <a name="command-object-ado"></a>Oggetto Command (ADO)
Definisce un comando specifico che si desidera eseguire su un'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare un oggetto **comando** per eseguire una query su un database e restituire record in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , per eseguire un'operazione bulk o per modificare la struttura di un database. A seconda della funzionalità del provider, alcune raccolte di **comandi** , metodi o proprietà possono generare un errore quando vi si fa riferimento.  
  
 Con le raccolte, i metodi e le proprietà di un oggetto **Command** , è possibile eseguire le operazioni seguenti:  
  
-   Definire il testo eseguibile del comando (ad esempio, un'istruzione SQL) con la proprietà [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) . In alternativa, per le strutture di comando o di query diverse dalle stringhe semplici (ad esempio, query modello XML) definire il comando con la proprietà [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) .  
  
-   Facoltativamente, indicare il dialetto del comando utilizzato in **CommandText** o **CommandStream** con la proprietà [dialect](../../../ado/reference/ado-api/dialect-property.md) .  
  
-   Definire query con parametri o argomenti di stored procedure con oggetti [Parameter](../../../ado/reference/ado-api/parameter-object.md) e la raccolta [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
-   Indica se i nomi dei parametri devono essere passati al provider con la proprietà [namedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) .  
  
-   Eseguire un comando e restituire un oggetto **Recordset** se appropriato con il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
-   Specificare il tipo di comando con la proprietà [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) prima dell'esecuzione per ottimizzare le prestazioni.  
  
-   Controllare se il provider salva una versione preparata o compilata del comando prima dell'esecuzione con la proprietà [preparata](../../../ado/reference/ado-api/prepared-property-ado.md) .  
  
-   Impostare il numero di secondi durante i quali un provider attende che un comando venga eseguito con la proprietà [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) .  
  
-   Associare una connessione aperta a un oggetto **Command** impostando la relativa proprietà [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
-   Impostare la proprietà [Name](../../../ado/reference/ado-api/name-property-ado.md) per identificare l'oggetto **Command** come metodo sull'oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) associato.  
  
-   Passare un oggetto **Command** alla proprietà [source](../../../ado/reference/ado-api/source-property-ado-recordset.md) di un **Recordset** per ottenere i dati.  
  
-   Accedere agli attributi specifici del provider con la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Per eseguire una query senza usare un oggetto **Command** , passare una stringa di query al metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) di un oggetto **Connection** o al metodo [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) di un oggetto **Recordset** . Tuttavia, è necessario un oggetto **comando** quando si desidera salvare in modo permanente il testo del comando ed eseguirlo di nuovo oppure utilizzare parametri di query.  
  
 Per creare un oggetto **comando** indipendentemente da un oggetto **connessione** definito in precedenza, impostare la relativa proprietà **ActiveConnection** su una stringa di connessione valida. ADO crea ancora un oggetto **connessione** , ma non assegna tale oggetto a una variabile oggetto. Tuttavia, se si associano più oggetti **Command** con la stessa connessione, è necessario creare e aprire in modo esplicito un oggetto **Connection** . in questo modo l'oggetto **connessione** viene assegnato a una variabile oggetto. Verificare che l'oggetto **connessione** sia stato aperto correttamente prima di assegnarlo alla proprietà **ActiveConnection** dell'oggetto **Command** , perché l'assegnazione di un oggetto **connessione** chiusa causa un errore. Se non si imposta la proprietà **ActiveConnection** dell'oggetto **Command** su questa variabile oggetto, ADO crea un nuovo oggetto **Connection** per ogni oggetto **Command** , anche se si utilizza la stessa stringa di connessione.  
  
 Per eseguire un **comando**, chiamarlo tramite la relativa proprietà [Name](../../../ado/reference/ado-api/name-property-ado.md) nell'oggetto **Connection** associato. Per il **comando** è necessario impostare la proprietà **ActiveConnection** sull'oggetto **Connection** . Se il **comando** dispone di parametri, passare i relativi valori come argomenti al metodo.  
  
 Se due o più oggetti **Command** vengono eseguiti sulla stessa connessione e l'oggetto **command** è un stored procedure con parametri di output, si verificherà un errore. Per eseguire ogni oggetto **Command** , utilizzare connessioni separate o disconnettere tutti gli altri oggetti **Command** dalla connessione.  
  
 La raccolta **Parameters** è il membro predefinito dell'oggetto **Command** . Di conseguenza, le due istruzioni di codice seguenti sono equivalenti.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   L'oggetto **Command** non è sicuro per lo scripting.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Command](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Appendice A: Provider](../../../ado/guide/appendixes/appendix-a-providers.md)
