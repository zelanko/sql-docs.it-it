---
title: Proprietà ActiveConnection (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ad7cdfdfc3c08175faf0584f2ae5069fcd39acb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719015"
---
# <a name="activeconnection-property-ado-md"></a>Proprietà ActiveConnection (ADO MD)
Indica a quale ADO [connessione](../../../ado/reference/ado-api/connection-object-ado.md) set di celle corrente dell'oggetto o attualmente catalogo a cui appartiene.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **Variant** che contiene una stringa che definisce una connessione oppure **connessione** oggetto. Il valore predefinito è vuoto.  
  
## <a name="remarks"></a>Note  
 È possibile impostare questa proprietà per un valido ADO **connessione** oggetto o a una stringa di connessione valida. Quando questa proprietà è impostata su una stringa di connessione, il provider crea un nuovo **connessione** utilizzando questa definizione dell'oggetto e viene aperta la connessione.  
  
 Se si usa la *ActiveConnection* argomento del [aprire](../../../ado/reference/ado-md-api/open-method-ado-md.md) metodo per aprire una [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto, il **ActiveConnection** proprietà verrà ereditare il valore dell'argomento.  
  
 Impostando il **ActiveConnection** proprietà di un [catalogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) oggetto **Nothing** rilascia i dati associati, inclusi i dati nel [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) raccolta e i relativi [dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md), e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetti. Chiusura di un **connessione** oggetto utilizzato per aprire un **catalogo** ha lo stesso effetto dell'impostazione il **ActiveConnection** proprietà **Nothing**.  
  
 Modifica del database predefinito della connessione fa riferimento il **ActiveConnection** proprietà di un **catalogo** oggetto invalida il contenuto del **catalogo**.  
  
 Si verificherà un errore se si prova a modificare la **ActiveConnection** proprietà di apertura **Cellset** oggetto.  
  
> [!NOTE]
>  In Visual Basic, ricordarsi di usare il **impostato** (parola chiave) durante l'impostazione di **ActiveConnection** proprietà da un **connessione** oggetto. Se si omette il **impostato** (parola chiave), che sarà effettivamente impostato il **ActiveConnection** uguale alla proprietà di **connessione** proprietà predefinita dell'oggetto,  **ConnectionString**. Il codice funzionerà; Tuttavia, si creerà un aggiuntivi per la connessione all'origine dati, che può incidere negativamente sulle prestazioni.  
  
 Quando si usa il provider di dati MSOLAP, impostare l'origine dati in una stringa di connessione a un nome di server e il catalogo iniziale per il nome di un catalogo dall'origine dati. Per connettersi a un file di cubo che viene disconnesso da un server, impostare il percorso per il percorso completo di. File CUB. In entrambi i casi, impostare il provider per il nome del provider. Ad esempio, la stringa seguente usa il Provider MSOLAP per la connessione a un catalogo denominato Bobs Video Store in un server denominato **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 La stringa seguente si connette a un file di cubo locale in corrispondenza della posizione C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Metodo Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
