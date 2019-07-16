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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931256"
---
# <a name="refresh-method-ado"></a>Metodo Refresh (ADO)
Aggiorna gli oggetti in una raccolta in modo da riflettere gli oggetti disponibili e specifiche del provider.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Note  
 Il **Aggiorna** metodo esegue attività diverse a seconda della raccolta da cui è stata chiamata.  
  
### <a name="parameters"></a>Parametri  
 Usando il **Refresh** metodo sul [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto recupera le informazioni sui parametri lato provider per la stored procedure o query con parametri specificata nel **comando** oggetto. La raccolta sarà vuota per i provider che non supportano chiamate a stored procedure o query con parametri.  
  
 È consigliabile impostare il [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) proprietà delle **comando** oggetto su un valore valido [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto, il [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà per un comando valido e il [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) proprietà **adCmdStoredProc** prima di chiamare il **Aggiorna** (metodo).  
  
 Se si accede il **parametri** raccolta prima di chiamare le **aggiornare** metodo, ADO automaticamente chiamerà il metodo e popolare la raccolta per l'utente.  
  
> [!NOTE]
>  Se si usa la **Refresh** metodo per ottenere informazioni sui parametri del provider di e restituisce uno o più tipi di dati a lunghezza variabile [parametro](../../../ado/reference/ado-api/parameter-object.md) oggetti, ADO possa allocare memoria per i parametri di base alle relative dimensioni massime possibili, che verrà generato un errore durante l'esecuzione. È necessario impostare esplicitamente il [dimensioni](../../../ado/reference/ado-api/size-property-ado-parameter.md) proprietà per tali parametri prima di chiamare le [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) metodo per evitare errori.  
  
### <a name="fields"></a>Campi  
 Usando il **Refresh** metodo sul [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta non ha alcun effetto visibile. Per recuperare le modifiche apportate dalla struttura di database sottostante, è necessario usare il [rieseguire una query](../../../ado/reference/ado-api/requery-method.md) metodo oppure, se il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objekt nepodporuje segnalibri, il [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)metodo.  
  
### <a name="properties"></a>Proprietà  
 Usando il **Refresh** metodo su un **proprietà** raccolta di alcuni oggetti popola la raccolta con le proprietà dinamiche esposte dal provider. Queste proprietà forniscono informazioni sulle funzionalità specifiche per il provider, oltre a supportate da ADO la proprietà predefinite.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta Axes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Raccolta di colonne](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Raccolta di dimensioni](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Raccolta di errori](../../../ado/reference/ado-api/errors-collection-ado.md)|[Raccolta di campi](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Raccolta di gruppi](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta hierarchies](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Raccolta di indici](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta di chiavi](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta Levels](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Raccolta di membri](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Raccolta di parametri](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Raccolta Positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Raccolta di oggetti procedure](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Raccolta delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md)|[Raccolta di tabelle](../../../ado/reference/adox-api/tables-collection-adox.md)|[Raccolta degli utenti](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Raccolta di oggetti View](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Esempio del metodo Refresh (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Proprietà Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Metodo Refresh (Servizi Desktop remoto)](../../../ado/reference/rds-api/refresh-method-rds.md)
