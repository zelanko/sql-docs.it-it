---
title: Cronologia di ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7fcdee5d45cffb14af2f1e0dc73941689c7fda4d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702839"
---
# <a name="ado-features-for-each-release"></a>Funzionalità di ADO per ogni versione

Questo argomento elenca le nuove funzionalità introdotte per ogni versione del ADOX ADO e ADO MD.

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0 è incluso in Windows Vista, come parte di Windows Data Access Components (Windows DAC) 6.0. ADO 6.0 è funzionalmente equivalente a ADO 2.8.

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8 è stato incluso in Windows XP e Windows Server 2003, come parte di Microsoft Data Access Components (MDAC) 2.8. Una versione ridistribuibile di MDAC 2.8 è anche disponibile. Si noti che questa versione ridistribuibile deve essere installata solo in Windows 2000. ADO 2.8 risolve diversi problemi correlati alla sicurezza:

 *Accesso alle unità disco rigido non è consentito all'esterno di un'area attendibile.*
Tra i domini di scripting che interessano i siti non trusted, sono disabilitate le seguenti operazioni: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset. Save**, e **Open**, usato in combinazione con il **adCmdFile**  flag o con il Provider Microsoft OLE DB Persistence (MSPersist).

 **Open** _,_ **Recordset. Save** _,_ **Stream.SaveToFile** _, e_ **Stream.LoadFromFile** _operano su solo i file fisici._
Questi metodi, a questo punto, verificare che gli handle di file scegliere solo i file fisici.

 **Recordset.ActiveCommand** _restituisce un errore quando viene richiamato da una pagina HTML o ASP._
Ciò impedisce che il **comando** oggetto dall'utilizzo improprio.

 _I numerosi_**recordset**_restituito da un'annidata_**forma**_comando ha un limite superiore._
Un comando shape annidato restituisce ora un massimo di 512 **recordset**. Ciò significa che un **forma** comando non può essere annidato non sono più a qualsiasi livello. Al contrario, il livello di nidificazione massimo è 512, se ogni comando genera un singolo (figlio) **Recordset**. Se, a qualsiasi livello, un **Shape** comando restituisce più **recordset**, il livello massimo di profondità sarà meno di 512.

## <a name="ado-27"></a>ADO 2.7

 *supporto delle piattaforme a 64 bit* ADO 2.7 introduce il supporto per processori a 64 bit.

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject**_metodo_ iniziando con ADO 2.6, gli oggetti ADO MD possono essere recuperati tramite nomi univoci, come specificato dal [proprietà UniqueName (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md). I nomi degli oggetti padre non debbano essere noti e le raccolte padre non sono necessario essere popolati per recuperare un oggetto dello schema. Visualizzare [metodo GetSchemaObject (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Comando flussi* il **comando** oggetto supporta i comandi nel formato di flusso come alternativa all'utilizzo di **CommandText** proprietà. Il [proprietà CommandStream (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) può essere utilizzato per specificare i modelli XML o gli updategram come le **comando** di input con il Provider Microsoft OLE DB per SQL Server.

 **Sottolinguaggio**_proprietà_ [sottolinguaggio](../../ado/reference/ado-api/dialect-property.md) è una nuova proprietà che definisce la sintassi e regole generali che il provider Usa analisi di flusso o nella stringa.

 **Command. Execute**_metodo_ il [metodo Execute](../../ado/reference/ado-api/execute-method-ado-command.md) di ADO **comando** oggetto è stato migliorato per l'uso di flussi per l'input e output.

 *Campo statusvalues* se l'utente rileva un errore DB_E_ERRORSOCCURRED quando si modifica un **campo** di un **Recordset**, ADO compilerà ora il **Field.Status**proprietà con le informazioni sullo stato appropriato in modo che l'utente dispone di ulteriori informazioni sulle cause dell'errore. Visualizzare [proprietà Status (campo ADO)](../../ado/reference/ado-api/status-property-ado-field.md).

 **NamedParameters**_proprietà_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) è una proprietà di nuovo il **comando** oggetto che indica che deve utilizzare il provider denominato parametri.

 *Set di risultati nei flussi* ADO possa restituire set di risultati da un'origine dati in un **Stream**, anziché un **Recordset** oggetto. Usa la versione più recente del Provider Microsoft OLE DB per SQL Server, è possibile ottenere i risultati XML dal provider eseguendo una query "Per XML". Oggetto **Stream** che riceve il set di risultati può essere aperto con un comando "Per XML" come origine. Visualizzare [recupero di set di risultati in flussi](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *Singola riga resultset* ADO **Record** oggetto può ora essere aperto in una stringa di comando oppure **comando** oggetto che restituisce una riga di dati dal provider. Ciò comporta un miglioramento delle prestazioni con i provider MDAC 2.6. Visualizzare [metodo Open (Record ADO)](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2.5

 **Record** _oggetto_ ADO 2.5 introduce il **Record** oggetto da rappresentare e gestire una riga a un **Recordset** o un provider di dati o un oggetto che incapsula un dati semistrutturati, ad esempio un file o directory.

 **Stream** _oggetto_ ADO 2.5 introduce anche il **Stream** oggetti per rappresentare un flusso di dati binari o testo.

 *Associazione URL* ADO 2.5 viene presentato l'utilizzo di un URL, come alternativa a un testo stringa e un comando di connessione, come nomi di oggetti di archivio dati. Un URL può essere utilizzato con l'oggetto esistente **Connection** e **Recordset** oggetti, nonché come con la nuova **Record** e **Stream** oggetti.

 *Provider di dati che supportano associazione URL* ADO 2.5 supporta i provider OLE DB che riconosce gli schemi URL. Ciò include il Provider OLE DB per Internet Publishing, che accede al file system di Windows 2000 e riconosce lo schema HTTP esistente.
