---
title: Raccolte e gli oggetti ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 62616ecebb8fa7795462c7e22437aabebb56bcaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700961"
---
# <a name="ado-objects-and-collections"></a>Oggetti e raccolte di ADO
ADO è costituito da quattro raccolte e gli oggetti seguenti nove.  
  
|Oggetto o una raccolta|Descrizione|  
|--------------------------|-----------------|  
|**Connessione** oggetto|Rappresenta una sessione univoca con un'origine dati. Nel caso di un sistema di database client/server, potrebbe essere equivalente a una connessione di rete effettivo al server. A seconda delle funzionalità supportate dal provider, alcune raccolte, metodi o proprietà di un **connessione** oggetto potrebbe non essere disponibile.|  
|**Command**|Utilizzato per definire un comando specifico, ad esempio una query SQL, deve essere eseguita su un'origine dati.|  
|**Recordset** oggetto|Rappresenta l'intero set di record da una tabella di base o i risultati di un comando eseguito. Tutti i **Recordset** gli oggetti sono costituiti da record (righe) e campi (colonne).|  
|**Record** oggetto|Rappresenta una singola riga di dati, da un **Recordset** o dal provider. Questo record potrebbe rappresentare un record di database o un altro tipo di oggetto, ad esempio un file o directory, a seconda del provider.|  
|**Stream** oggetto|Rappresenta un flusso di dati binari o testo. Ad esempio, un documento XML può essere caricato in un flusso di input o restituito da alcuni provider come i risultati di una query di comando. Oggetto **Stream** oggetto può essere utilizzato per modificare i campi o record che contengono questi flussi di dati.|  
|**Parametro** oggetto|Rappresenta un parametro o un argomento associato a un **comando** oggetto, in base a una stored procedure o query con parametri.|  
|**Campo** oggetto|Rappresenta una colonna di dati con un tipo di dati comune. Ciascuna **campo** corrisponde a una colonna in oggetto il **Recordset**.|  
|**Proprietà** oggetto|Rappresenta una caratteristica di un oggetto ADO che viene definito dal provider. Gli oggetti ADO presentano due tipi di proprietà: predefinito e dinamico. Tali proprietà predefinite sono implementati in ADO e immediatamente disponibili per qualsiasi nuovo oggetto. Il **proprietà** oggetto è un contenitore per le proprietà dinamiche, definito dal provider sottostante.|  
|**Error**|Contiene informazioni dettagliate sugli errori di accesso dati che si riferiscono a una singola operazione che interessa il provider.|  
|**Campi** raccolta|Contiene tutti i **campo** gli oggetti di un **Recordset** oppure **Record** oggetto.|  
|**Proprietà** raccolta|Contiene tutti i **proprietà** gli oggetti per un'istanza specifica di un oggetto.|  
|**Parametri** raccolta|Contiene tutti i **parametri** gli oggetti di un **comando** oggetto.|  
|**Errori** raccolta|Contiene tutti i **errore** gli oggetti creati in risposta a un singolo errore relativi al provider.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)
