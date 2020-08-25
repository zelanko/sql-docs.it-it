---
description: Metodi BeginTrans, CommitTrans e RollbackTrans (ADO)
title: Metodi BeginTrans, CommitTrans e RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: rothja
ms.author: jroth
ms.openlocfilehash: cefa913c42440d69345bfa9c8d4b8826a0bc3d84
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776570"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>Metodi BeginTrans, CommitTrans e RollbackTrans (ADO)
Questi metodi di transazione gestiscono l'elaborazione delle transazioni all'interno di un oggetto [connessione](./connection-object-ado.md) come indicato di seguito:  
  
-   **BeginTrans** Inizia una nuova transazione.  
  
-   **CommitTrans** Salva le modifiche e termina la transazione corrente. Potrebbe inoltre avviare una nuova transazione.  
  
-   **RollbackTrans** Annulla tutte le modifiche apportate durante la transazione corrente e termina la transazione. Potrebbe inoltre avviare una nuova transazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valore restituito  
 **BeginTrans** può essere chiamato come funzione che restituisce una variabile **Long** che indica il livello di nidificazione della transazione.  
  
#### <a name="parameters"></a>Parametri  
 *object*  
 Oggetto **Connection** .  
  
## <a name="connection"></a>Connessioni  
 Utilizzare questi metodi con un oggetto **Connection** quando si desidera salvare o annullare una serie di modifiche apportate ai dati di origine come singola unità. Per trasferire il denaro tra gli account, ad esempio, si sottrae un importo da uno e si aggiunge la stessa quantità all'altra. Se uno degli aggiornamenti ha esito negativo, gli account non sono più bilanciati. Apportare queste modifiche all'interno di una transazione aperta garantisce che tutte o nessuna delle modifiche venga attraversata.  
  
> [!NOTE]
>  Non tutti i provider supportano le transazioni. Verificare che la proprietà definita dal provider "**Transaction DDL**" sia presente nella raccolta [Properties](./properties-collection-ado.md) dell'oggetto **Connection** , a indicare che il provider supporta le transazioni. Se il provider non supporta le transazioni, la chiamata a uno di questi metodi restituirà un errore.  
  
 Dopo aver chiamato il metodo **BeginTrans** , il provider non eseguirà più immediatamente il commit delle modifiche apportate fino a quando non si chiama **CommitTrans** o **RollbackTrans** per terminare la transazione.  
  
 Per i provider che supportano le transazioni nidificate, la chiamata al metodo **BeginTrans** all'interno di una transazione aperta avvia una nuova transazione nidificata. Il valore restituito indica il livello di annidamento: un valore restituito pari a "1" indica che è stata aperta una transazione di primo livello, ovvero che la transazione non è annidata all'interno di un'altra transazione, "2" indica che è stata aperta una transazione di secondo livello (una transazione nidificata all'interno di una transazione di primo livello) e così via. La chiamata a **CommitTrans** o **RollbackTrans** interessa solo la transazione aperta più di recente; prima di poter risolvere le transazioni di livello superiore, è necessario chiudere o eseguire il rollback della transazione corrente.  
  
 La chiamata al metodo **CommitTrans** Salva le modifiche apportate all'interno di una transazione aperta sulla connessione e termina la transazione. La chiamata al metodo **RollbackTrans** inverte le modifiche apportate all'interno di una transazione aperta e termina la transazione. Se si chiama un metodo in assenza di una transazione aperta, viene generato un errore.  
  
 A seconda della proprietà [Attributes](./attributes-property-ado.md) dell'oggetto **Connection** , chiamare i metodi **CommitTrans** o **RollbackTrans** può avviare automaticamente una nuova transazione. Se la proprietà **Attributes** è impostata su **adXactCommitRetaining**, il provider avvia automaticamente una nuova transazione dopo una chiamata a **CommitTrans** . Se la proprietà **Attributes** è impostata su **adXactAbortRetaining**, il provider avvia automaticamente una nuova transazione dopo una chiamata a **RollbackTrans** .  
  
## <a name="remote-data-service"></a>Remote Data Service  
 I metodi **BeginTrans**, **CommitTrans**e **RollbackTrans** non sono disponibili in un oggetto **connessione** sul lato client.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi BeginTrans, CommitTrans e RollbackTrans (VB)](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Esempio di metodi BeginTrans, CommitTrans e RollbackTrans (VC + +)](./begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Proprietà Attributes (ADO)](./attributes-property-ado.md)