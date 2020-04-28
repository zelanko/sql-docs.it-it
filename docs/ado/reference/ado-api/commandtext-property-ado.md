---
title: Proprietà CommandText (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0288dde74d2a172c9b0f8bdb865f4467fb0f637
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919720"
---
# <a name="commandtext-property-ado"></a>Proprietà CommandText (ADO)
Indica il testo di un comando da emettere a fronte di un provider.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Ottiene o imposta un valore **stringa** che contiene un comando del provider, ad esempio un'istruzione SQL, un nome di tabella, un URL relativo o una chiamata stored procedure. Il valore predefinito è la stringa vuota ("").  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **CommandText** per impostare o restituire il testo di un comando rappresentato da un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) . Si tratta in genere di un'istruzione SQL, ma può anche essere qualsiasi altro tipo di istruzione di comando riconosciuta dal provider, ad esempio una chiamata stored procedure. Un'istruzione SQL deve essere del dialetto o della versione particolare supportata da query processor del provider.  
  
 Se la proprietà [preparata](../../../ado/reference/ado-api/prepared-property-ado.md) dell'oggetto **Command** è impostata su **true** e l'oggetto **Command** è associato a una connessione aperta quando si imposta la proprietà **CommandText** , ADO prepara la query, ovvero un form compilato della query archiviata dal provider, quando si chiamano i metodi [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) o [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) .  
  
 A seconda dell'impostazione della proprietà [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) , ADO potrebbe modificare la proprietà **CommandText** . È possibile leggere la proprietà **CommandText** in qualsiasi momento per visualizzare il testo effettivo del comando che ADO utilizzerà durante l'esecuzione.  
  
 Utilizzare la proprietà **CommandText** per impostare o restituire un URL relativo che specifichi una risorsa, ad esempio un file o una directory. La risorsa è relativa a una posizione specificata in modo esplicito da un URL assoluto o in modo implicito da un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) aperta.  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Metodo Requery](../../../ado/reference/ado-api/requery-method.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
