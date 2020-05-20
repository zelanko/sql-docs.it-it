---
title: provider Microsoft OLE DB per Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: rothja
ms.author: jroth
ms.openlocfilehash: e956ca5486485c3dde8079f6b9067a8fef7e2f3a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761639"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Panoramica di provider Microsoft OLE DB per Oracle
> [!IMPORTANT]
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Usare invece il provider di OLE DB di Oracle.

 Il provider Microsoft OLE DB per Oracle consente a ADO di accedere ai database Oracle.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare l'argomento del *provider* della proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) su:

```vb
MSDAORA
```

 La lettura della proprietà del [provider](../../../ado/reference/ado-api/provider-property-ado.md) restituirà anche questa stringa.

 Se in un database Oracle viene eseguita una query di join con un keyset o un cursore dinamico, si verificherà un errore. Oracle supporta solo un cursore statico di sola lettura.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è la seguente:

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 La stringa è costituita dalle parole chiave seguenti:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il provider di OLE DB per Oracle.|
|**Origine dati**|Specifica il nome di un server.|
|**ID utente**|Specifica il nome utente.|
|**Password**|Specifica la password dell'utente.|

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = Yes** o **Integrated Security = SSPI** anziché le informazioni relative a ID utente e password nella stringa di connessione.

## <a name="provider-specific-connection-parameters"></a>Parametri di connessione specifici del provider
 Il provider supporta diversi parametri di connessione specifici del provider, oltre a quelli definiti da ADO. Come per le proprietà di connessione ADO, queste proprietà specifiche del provider possono essere impostate tramite la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) di una [connessione](../../../ado/reference/ado-api/connection-object-ado.md) o come parte di **ConnectionString**.

 Questi parametri sono descritti in modo completo nella Guida [di riferimento per programmatori OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). L' [indice della proprietà dinamica ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) fornisce un riferimento incrociato tra questi nomi di parametro e le proprietà OLE DB corrispondenti.

|Parametro|Description|
|---------------|-----------------|
|**Handle finestra**|Indica l'handle della finestra da utilizzare per richiedere ulteriori informazioni.|
|**Locale Identifier**|Indica un numero univoco a 32 bit, ad esempio 1033, che specifica le preferenze relative alla lingua dell'utente. Queste preferenze indicano il modo in cui le date e le ore vengono formattate, gli elementi vengono ordinati alfabeticamente, le stringhe vengono confrontate e così via.|
|**Servizi di OLE DB**|Indica una maschera di maschera che specifica OLE DB servizi da abilitare o disabilitare.|
|**Messaggio di richiesta**|Indica se richiedere all'utente quando viene stabilita una connessione.|
|**Proprietà estese**|Stringa contenente informazioni di connessione estese specifiche del provider. Utilizzare questa proprietà solo per le informazioni di connessione specifiche del provider che non possono essere descritte tramite il meccanismo della proprietà.|

## <a name="see-also"></a>Vedere anche
 Proprietà [ConnectionString (](../../../ado/reference/ado-api/connectionstring-property-ado.md) ADO) [provider Property](../../../ado/reference/ado-api/provider-property-ado.md) (ADO) [Recordset Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
