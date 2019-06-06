---
title: Comando oggetto (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 089a261eaea2701354af6082827c12491810b74c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699008"
---
# <a name="command-object-ado"></a>Oggetto Command (ADO)
Definisce un comando specifico che si prevede di eseguire su un'origine dati.  
  
## <a name="remarks"></a>Note  
 Usare un **comandi** oggetto di query su un database e restituire i record in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, per eseguire un'operazione bulk o per modificare la struttura di un database. La funzionalità del provider, a seconda alcune **comando** raccolte, metodi o proprietà potrebbe generare un errore quando vi viene fatto riferimento.  
  
 Con le raccolte, i metodi e proprietà di un **comando** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Definire il testo del comando (ad esempio, un'istruzione SQL) eseguibile con il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà. In alternativa, per query o comandi strutture oltre alla semplice stringhe (ad esempio, query modello XML) definiscono il comando con il [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) proprietà.  
  
-   Facoltativamente, indicare il sottolinguaggio del comando usato nel **CommandText** oppure **CommandStream** con il [sottolinguaggio](../../../ado/reference/ado-api/dialect-property.md) proprietà.  
  
-   Definire le query con parametri o gli argomenti di stored procedure con [parametri](../../../ado/reference/ado-api/parameter-object.md) gli oggetti e i [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta.  
  
-   Indicare se i nomi dei parametri deve essere passati al provider con il [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) proprietà.  
  
-   Eseguire un comando e restituire un **Recordset** oggetto se appropriato, tramite il [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) (metodo).  
  
-   Specificare il tipo di comando con il [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) proprietà prima dell'esecuzione per ottimizzare le prestazioni.  
  
-   Controllare se il provider deve salvare una versione preparata (o compilata) del comando prima dell'esecuzione con il [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) proprietà.  
  
-   Impostare il numero di secondi di attesa di un provider per un comando da eseguire con il [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) proprietà.  
  
-   Associare una connessione aperta con un **comandi** oggetto impostando relativo [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà.  
  
-   Impostare il [Name](../../../ado/reference/ado-api/name-property-ado.md) proprietà per identificare le **comando** oggetto come un metodo sull'oggetto associato [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
-   Passare un **comandi** dell'oggetto per il [origine](../../../ado/reference/ado-api/source-property-ado-recordset.md) proprietà di un **Recordset** per ottenere i dati.  
  
-   Accedere agli attributi specifici del provider con il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
> [!NOTE]
>  Per eseguire una query senza usare una **comando** dell'oggetto, passare una stringa di query per il [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) metodo di un **connessione** oggetto o al [aprire](../../../ado/reference/ado-api/open-method-ado-recordset.md)metodo di un **Recordset** oggetto. Tuttavia, un **comando** oggetto è obbligatorio quando si desidera salvare in modo permanente il testo del comando ed eseguirla di nuovo, oppure utilizzare i parametri di query.  
  
 Per creare un **comandi** oggetto indipendentemente da un oggetto definito in precedenza **connessione** dell'oggetto, impostare relativo **ActiveConnection** proprietà in una stringa di connessione valida. ADO crea ancora un **connessione** oggetto, ma non assegna tale oggetto a una variabile oggetto. Tuttavia, se si sta associando più **comandi** gli oggetti con la stessa connessione, in modo esplicito è necessario creare e aprire un **connessione** oggetto; questo viene assegnato il **connessione** oggetto a una variabile oggetto. Assicurarsi che il **connessione** oggetto è stato aperto correttamente prima di assegnarlo al **ActiveConnection** proprietà del **comando** dell'oggetto, perché l'assegnazione di un chiuso **connessione** oggetto provoca un errore. Se non si imposta la **ActiveConnection** proprietà delle **comando** dell'oggetto a questa variabile di oggetto, crea un nuovo oggetto ADO **connessione** per ciascun  **Comando** dell'oggetto, anche se si usa la stessa stringa di connessione.  
  
 Per eseguire una **comandi**, chiamato in base al relativo [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà sull'oggetto associato **connessione** oggetto. Il **comandi** deve avere relativo **ActiveConnection** impostata sul **connessione** oggetto. Se il **comando** dispone di parametri, passare i valori come argomenti al metodo.  
  
 Se due o più **comandi** gli oggetti vengono eseguiti nella stessa connessione e una **comando** oggetto è una stored procedure con parametri di output, si verifica un errore. Per eseguire ciascuna **comandi** dell'oggetto, usare connessioni separate o disconnettere tutti gli altri **comando** oggetti dalla connessione.  
  
 Il **parametri** raccolta è il membro predefinito delle **comando** oggetto. Di conseguenza, le due istruzioni di codice seguenti sono equivalenti.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   Il **comando** oggetto non sicuro per lo script.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Le proprietà degli oggetti, metodi ed eventi di comando](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Appendice A: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
