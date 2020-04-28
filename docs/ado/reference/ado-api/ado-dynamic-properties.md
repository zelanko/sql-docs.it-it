---
title: Proprietà dinamiche ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71396a071a42d7dd40a6537a2834541aab2b6bad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921098"
---
# <a name="ado-dynamic-properties"></a>Proprietà dinamiche ADO
È possibile aggiungere proprietà dinamiche alle raccolte [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) degli oggetti [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Command](../../../ado/reference/ado-api/command-object-ado.md)o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . L'origine di queste proprietà è un provider di dati, ad esempio il [provider di OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o un provider di servizi, ad esempio il [servizio Microsoft Cursor per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Per ulteriori informazioni su una specifica proprietà dinamica, fare riferimento alla documentazione del provider di dati o del provider di servizi appropriato.  
  
 L' [indice della proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornisce un riferimento incrociato tra i nomi ADO e OLE DB per ogni proprietà dinamica del provider OLE DB standard.  
  
 Le seguenti proprietà dinamiche sono particolarmente interessanti e sono inoltre documentate nelle origini citate in precedenza. La funzionalità speciale con ADO è documentata negli argomenti della Guida ADO elencati di seguito.  
  
|||  
|-|-|  
|[Ottimizzare](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Specifica se è necessario creare un indice in questo campo.|  
|[Prompt](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Specifica se il provider di OLE DB deve richiedere all'utente le informazioni di inizializzazione.|  
|[Nome riforma](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Specifica un nome per l'oggetto **Recordset** .|  
|[Comando di risincronizzazione](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Specifica una stringa di comando fornita dall'utente che il metodo di **Risincronizzazione** emette per aggiornare i dati nella tabella denominata nella proprietà dinamica della **tabella univoca** .|  
|[Tabella univoca, schema univoco, catalogo univoco](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabella univoca** Specifica il nome della tabella di base su cui sono consentiti aggiornamenti, inserimenti ed eliminazioni.<br /><br /> **Schema univoco** Specifica lo schema o il nome del proprietario della tabella.<br /><br /> **Catalogo univoco** Specifica il catalogo o il nome del database che contiene la tabella.|  
|[Aggiornamento della risincronizzazione](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Specifica se il metodo **UpdateBatch** è seguito da un'operazione implicita di **Risincronizzazione** del metodo e, in tal caso, dall'ambito di tale operazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Raccolte ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Costanti enumerate ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Appendice B: errori ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventi ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Metodi ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modello a oggetti ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Oggetti e interfacce ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Proprietà ADO](../../../ado/reference/ado-api/ado-properties.md)
