---
title: Connessione di contesto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b091f515af926fb17cea424b4f8875baf0fa83a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068419"
---
# <a name="context-connection"></a>Connessione di contesto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il problema dell'accesso ai dati interni rappresenta uno scenario comune. Si tratta della situazione in cui si desidera accedere allo stesso server su cui viene eseguita la funzione o la stored procedure CLR (Common Language Runtime). Una possibilità consiste nel creare una connessione usando **SqlConnection**, specificare una stringa di connessione che punta al server locale e aprire la connessione. Questa procedura richiede la specifica di credenziali per l'accesso. La connessione è in una sessione di database diverso rispetto a stored procedure o funzione, può presentare diversi **impostare** opzioni, si trova in una transazione separata, non rileva le tabelle temporanee e così via. Se il codice di funzione o la stored procedure gestita sono in esecuzione nel processo di SQL Server, è perché qualcuno si è collegato a quel server e ha eseguito un'istruzione SQL per richiamarli. È possibile la stored procedure o funzione venga eseguita nel contesto di tale connessione, con la transazione **impostare** opzioni e così via. In questo caso si parla di connessione di contesto.  
  
 La connessione di contesto consente di eseguire istruzioni Transact-SQL nello stesso contesto nel quale è stato richiamato il codice. Per ottenere la connessione di contesto, è necessario utilizzare la parola chiave relativa alla stringa di connessione "context connection", come nell'esempio seguente:  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>In questa sezione  
 [Connessione normale e Connessioni di contesto](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Vengono descritte le differenze tra le connessioni normali e di contesto.  
  
 [Restrizioni relative alle connessioni normali e di contesto](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Vengono descritte le restrizioni relative alle connessioni normali e di contesto.  
  
  
