---
title: Interfacce e oggetti ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0bba8402bb49d481886e4c81071443873834c8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248903"
---
# <a name="ado-objects-and-interfaces"></a>Interfacce e oggetti ADO
Le relazioni tra tali oggetti sono rappresentate nel [modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md).  
  
 Ogni oggetto può essere contenuto nella relativa raccolta corrispondente. Ad esempio, un' [errore](../../../ado/reference/ado-api/error-object.md) oggetto può essere contenuto in un [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta. Per altre informazioni, vedere [raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md) o un argomento di raccolta specifico.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|Utilizzato per recuperare il comando OLE DB sottostante da un oggetto ADOCommand.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|Costruisce un oggetto ADO **Record** oggetto da OLE DB **riga** oggetto in un'applicazione C/C++.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|Costruisce un oggetto ADO **Recordset** oggetto da OLE DB **set di righe** oggetto in un'applicazione C/C++.|  
|[Interfaccia ADOStreamConstruction](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|Costruisce un oggetto ADO **Stream** oggetto da OLE DB **IStream** oggetto in un'applicazione C/C++.|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|Definisce un comando specifico che si prevede di eseguire su un'origine dati.<br /><br /> Il **comando** oggetto non sicuro per lo script.|  
|[Connessione](../../../ado/reference/ado-api/connection-object-ado.md)|Rappresenta una connessione aperta a un'origine dati.<br /><br /> Il **connessione** oggetto è sicuro per lo scripting.|  
|[Interfaccia IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|Ottiene l'oggetto origine dati OLE DB sottostante per il provider di forma.|  
|[Errore](../../../ado/reference/ado-api/error-object.md)|Contiene informazioni dettagliate sugli errori di accesso dati che si riferiscono a una singola operazione che interessa il provider.<br /><br /> Il **errore** oggetto non sicuro per lo script.|  
|[Campo](../../../ado/reference/ado-api/field-object.md)|Rappresenta una colonna di dati con un tipo di dati comune.|  
|[Parametro](../../../ado/reference/ado-api/parameter-object.md)|Rappresenta un parametro o un argomento associato a un **comando** oggetto basato su una query con parametri o stored procedure.<br /><br /> Il **parametro** oggetto non sicuro per lo script.|  
|[Proprietà](../../../ado/reference/ado-api/property-object-ado.md)|Rappresenta una caratteristica dinamica di un oggetto ADO che viene definito dal provider.|  
|[Record](../../../ado/reference/ado-api/record-object-ado.md)|Rappresenta una riga di una **Recordset**, o una directory o file in un file system. Il **Record** oggetto è sicuro per lo scripting.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|Rappresenta il set di record da una tabella di base o i risultati di un comando eseguito. In qualsiasi momento, il **Recordset** oggetto fa riferimento a un singolo record all'interno del set come record corrente.<br /><br /> Il **Recordset** oggetto è sicuro per lo scripting.|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|Rappresenta un flusso binario dei dati.<br /><br /> Il **Stream** oggetto è sicuro per lo scripting.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte di ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Proprietà dinamiche ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice b: Errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
