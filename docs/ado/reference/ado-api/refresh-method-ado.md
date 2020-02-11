---
title: Metodo Refresh (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a676bf5eb3d8d98f1b2eb9367aa8ad56f0da209d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931256"
---
# <a name="refresh-method-ado"></a>Metodo Refresh (ADO)
Aggiorna gli oggetti di una raccolta in modo da riflettere gli oggetti disponibili e specifici del provider.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **Refresh** esegue diverse attività a seconda della raccolta da cui viene chiamata.  
  
### <a name="parameters"></a>Parametri  
 L'utilizzo del metodo **Refresh** sulla raccolta [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) di un oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) consente di recuperare informazioni sui parametri lato provider per la query stored procedure o con parametri specificata nell'oggetto **Command** . La raccolta sarà vuota per i provider che non supportano chiamate di stored procedure o query con parametri.  
  
 È necessario impostare la proprietà [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) dell'oggetto **Command** su un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) valido, la proprietà [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) su un comando valido e la proprietà [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) su **adCmdStoredProc** prima di chiamare il metodo **Refresh** .  
  
 Se si accede alla raccolta **Parameters** prima di chiamare il metodo **Refresh** , ADO chiamerà automaticamente il metodo e popola la raccolta automaticamente.  
  
> [!NOTE]
>  Se si utilizza il metodo **Refresh** per ottenere informazioni sui parametri dal provider e vengono restituiti uno o più oggetti [parametro](../../../ado/reference/ado-api/parameter-object.md) di tipo di dati a lunghezza variabile, ADO può allocare memoria per i parametri in base alle dimensioni massime potenziali, che causeranno un errore durante l'esecuzione. È necessario impostare in modo esplicito la proprietà [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) per questi parametri prima di chiamare il metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) per evitare errori.  
  
### <a name="fields"></a>Campi  
 L'utilizzo del metodo **Refresh** sulla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) non ha alcun effetto visibile. Per recuperare le modifiche dalla struttura del database sottostante, è necessario utilizzare il metodo [Requery](../../../ado/reference/ado-api/requery-method.md) oppure, se l'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) non supporta i segnalibri, il metodo [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
### <a name="properties"></a>Proprietà  
 Se si usa il metodo **Refresh** su una raccolta **Properties** di alcuni oggetti, la raccolta viene popolata con le proprietà dinamiche esposte dal provider. Queste proprietà forniscono informazioni sulle funzionalità specifiche del provider, oltre alle proprietà predefinite supportate da ADO.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta assi](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Raccolta Columns](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Raccolta Dimensions](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Raccolta di errori](../../../ado/reference/ado-api/errors-collection-ado.md)|[Raccolta Fields](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Raccolta di gruppi](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta Hierarchies](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Raccolta Indexes](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta di chiavi](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta levels](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Raccolta members](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Raccolta Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Raccolta Positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Raccolta Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Raccolta delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md)|[Raccolta Tables](../../../ado/reference/adox-api/tables-collection-adox.md)|[Raccolta utenti](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Raccolta views](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Esempio di metodo Refresh (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Proprietà Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Metodo Refresh (Servizi Desktop remoto)](../../../ado/reference/rds-api/refresh-method-rds.md)
