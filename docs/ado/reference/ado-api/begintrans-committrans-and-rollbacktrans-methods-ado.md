---
title: BeginTrans, CommitTrans e RollbackTrans (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ee5560a27f7df49a82e964753f792bd46270d3a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696489"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>Metodi BeginTrans, CommitTrans e RollbackTrans (ADO)
Questi metodi gestiscono l'elaborazione all'interno delle transazioni una [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto come indicato di seguito:  
  
-   **BeginTrans** inizia una nuova transazione.  
  
-   **CommitTrans** Salva eventuali modifiche apportate e termina la transazione corrente. Anche possibile avviare una nuova transazione.  
  
-   **RollbackTrans** Annulla tutte le modifiche apportate durante la transazione corrente e termina la transazione. Anche possibile avviare una nuova transazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valore restituito  
 **BeginTrans** può essere chiamato come una funzione che restituisce un **lungo** variabile che indica il livello di nidificazione della transazione.  
  
#### <a name="parameters"></a>Parametri  
 *object*  
 Oggetto **connessione** oggetto.  
  
## <a name="connection"></a>Connessione  
 Usare questi metodi con un **connessione** dell'oggetto quando si desidera salvare o annullare una serie di modifiche apportate ai dati di origine come singola unità. Ad esempio, per il trasferimento di denaro tra conti, si sottrae un importo da uno e si aggiunge la stessa quantità a altro. Se l'aggiornamento ha esito negativo, l'account non è più bilanciare. Queste modifiche all'interno di una transazione aperta assicura che passano attraverso tutte o nessuna delle modifiche.  
  
> [!NOTE]
>  Non tutti i provider supportano le transazioni. Verificare che la proprietà definito dal provider "**transazione DDL**" viene visualizzato nei **connessione** dell'oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta, che indica che il provider supporta transazioni. Se il provider non supporta le transazioni, una chiamata a uno di questi metodi restituirà un errore.  
  
 Dopo aver chiamato il **BeginTrans** metodo, il provider non è più istantaneamente verrà commit le modifiche apportate fino a quando non si chiama **CommitTrans** oppure **RollbackTrans** per terminare il transazione.  
  
 Per i provider che supportano le transazioni nidificate, chiama il **BeginTrans** metodo all'interno di una transazione aperta inizia una nuova transazione nidificata. Il valore restituito indica il livello di annidamento: indica un valore restituito pari a "1" è stata aperta una transazione di primo livello (vale a dire, la transazione non è annidata all'interno di un'altra transazione), "2" indica che è stato aperto una transazione di secondo livello (una transazione annidata all'interno di una transazione di primo livello), e così via. La chiamata **CommitTrans** oppure **RollbackTrans** interessa solo la maggior parte delle transazioni aperti di recente; è necessario chiudere o il rollback della transazione corrente prima che è possibile risolvere alcuna transazione di livello superiore.  
  
 Chiama il **CommitTrans** metodo salva le modifiche apportate all'interno di una transazione aperta per la connessione e termina la transazione. Chiama il **RollbackTrans** metodo inverte le modifiche apportate all'interno di una transazione aperta e termina la transazione. La chiamata a dei metodi quando non sono presenti transazioni aperte genera un errore.  
  
 In base il **connessione** dell'oggetto [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà, la chiamata ai **CommitTrans** o **RollbackTrans** metodi potrebbero avviare automaticamente una nuova transazione. Se il **attributi** è impostata su **adXactCommitRetaining**, il provider avvia automaticamente una nuova transazione dopo un **CommitTrans** chiamare. Se il **attributi** è impostata su **adXactAbortRetaining**, il provider avvia automaticamente una nuova transazione dopo un **RollbackTrans** chiamare.  
  
## <a name="remote-data-service"></a>Servizio dati remoto  
 Il **BeginTrans**, **CommitTrans**, e **RollbackTrans** metodi non sono disponibili sul lato client **connessione** oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BeginTrans, CommitTrans e RollbackTrans (esempio di metodi (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans e RollbackTrans esempio di metodi (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Proprietà attributi (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
