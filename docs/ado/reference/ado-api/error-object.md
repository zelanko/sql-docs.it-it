---
title: Oggetto Error | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5018dc921267663d64037024ef21c82ac6e3f7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932966"
---
# <a name="error-object"></a>Oggetto Error
Contiene informazioni dettagliate sugli errori di accesso dati che si riferiscono a una singola operazione che interessa il provider.  
  
## <a name="remarks"></a>Note  
 Qualsiasi operazione che interessa oggetti ADO è possibile generare uno o più errori del provider. Come si verifica ogni errore, una o più **errore** gli oggetti vengono inseriti nel [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta del [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. Quando un'altra operazione ADO genera un errore, il **errori** raccolta viene cancellata e il nuovo set di **errore** oggetti viene inserito nella **errori** raccolta.  
  
> [!NOTE]
>  Ciascuna **errore** oggetto rappresenta un errore specifico del provider, non un errore ADO. Errori ADO vengono esposti al meccanismo di gestione delle eccezioni in fase di esecuzione. Ad esempio, in Microsoft Visual Basic, l'occorrenza di un errore specifico del ADO attiverà un' **in caso di errore** eventi e vengono visualizzate nel **errore** oggetto. Per un elenco completo degli errori ADO, vedere la [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) argomento.  
  
 È possibile leggere un' **errore** proprietà dell'oggetto per ottenere i dettagli specifici su ogni errore, inclusi i seguenti:  
  
-   Il [descrizione](../../../ado/reference/ado-api/description-property.md) proprietà, che contiene il testo dell'errore. Questa è la proprietà predefinita.  
  
-   Il [numero](../../../ado/reference/ado-api/number-property-ado.md) proprietà, che contiene il **lungo** valore intero costante dell'errore.  
  
-   Il [origine](../../../ado/reference/ado-api/source-property-ado-error.md) proprietà, che identifica l'oggetto che ha generato l'errore. Ciò è particolarmente utile quando si dispone di più **errore** gli oggetti nel **errori** raccolta seguendo una richiesta a un'origine dati.  
  
-   Il [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) e [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) proprietà, che offrono informazioni dalle origini dati SQL.  
  
 Quando si verifica un errore del provider, questo viene inserito nel **errori** insieme del **connessione** oggetto. ADO supporta la restituzione di più errori per una singola operazione di ADO per consentire le informazioni sull'errore specifico del provider. Per ottenere questa informazioni dettagliate sull'errore in un gestore degli errori, usare le funzionalità di intercettazione degli errori appropriate della lingua o l'ambiente in uso, quindi usare cicli annidati per enumerare le proprietà della ognuno **errore** dell'oggetto di **Errori** raccolta.  
  
> [!NOTE]
>  **Microsoft Visual Basic e gli utenti di VBScript** se non è non valido **connessione** dell'oggetto, è necessario recuperare informazioni sull'errore dal **errore** oggetto.  
  
 Proprio come provider di effettuare, ADO Cancella il **informazioni di errore OLE** dell'oggetto prima di effettuare una chiamata che potrebbe potenzialmente generare un nuovo errore del provider. Tuttavia, il **errori** raccolta sul **connessione** oggetto viene deselezionato e viene popolato solo quando il provider genera un errore nuovo o quando il [Cancella](../../../ado/reference/ado-api/clear-method-ado.md) viene chiamato il metodo.  
  
 Alcune proprietà e metodi restituiscono gli avvisi che vengono visualizzati come **errore** gli oggetti nel **errori** raccolta ma non arrestano l'esecuzione del programma. Prima di chiamare il [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodi su un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ; dell'oggetto di [aprire](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo su un **connessione** ; dell'oggetto o impostare il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà su un **Recordset** dell'oggetto, chiamare il **Clear**metodo su di **errori** raccolta. In questo modo, è possibile leggere il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà delle **errori** insieme per provare gli avvisi restituiti.  
  
 Il **errore** oggetto non sicuro per lo script.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Error](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState proprietà esempio (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState esempio di proprietà (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Raccolta di errori (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Appendice A: provider](../../../ado/guide/appendixes/appendix-a-providers.md)
