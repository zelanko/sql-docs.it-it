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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919720"
---
# <a name="commandtext-property-ado"></a>Proprietà CommandText (ADO)
Indica il testo di un comando per essere eseguita su un provider.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Ottiene o imposta una **stringa** valore che contiene un comando del provider, ad esempio un'istruzione SQL, un nome di tabella, un URL relativo o una chiamata alla stored procedure. Il valore predefinito è una stringa vuota ("").  
  
## <a name="remarks"></a>Note  
 Usare la **CommandText** proprietà per impostare o restituire il testo di un comando rappresentato da un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto. Ciò in genere sarà un'istruzione SQL, ma può anche essere di qualsiasi altro tipo di istruzione del comando riconosciuto dal provider, ad esempio una chiamata alla stored procedure. Un'istruzione SQL deve avere il sottolinguaggio specifico o una versione supportata dal processore di query del provider.  
  
 Se il [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) proprietà delle **comando** è impostata su **True** e il **comando** oggetto è associato a una connessione aperta quando si imposta il **CommandText** proprietà ADO prepara la query (vale a dire, un modulo compilato di query archiviato dal provider) quando si chiama il [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) o [aprire](../../../ado/reference/ado-api/open-method-ado-connection.md)metodi.  
  
 In base il [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) possono essere modificati, impostazione della proprietà ADO le **CommandText** proprietà. È possibile leggere il **CommandText** proprietà in qualsiasi momento per visualizzare il testo del comando effettivo ADO che verrà utilizzato durante l'esecuzione.  
  
 Usare la **CommandText** proprietà per impostare o restituire un URL relativo che specifica una risorsa, ad esempio un file o directory. La risorsa è relativo alla posizione specificata in modo esplicito da un URL assoluto, o in modo implicito da un'apertura [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni ed esempio di proprietà direzione (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery (metodo)](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, dimensioni e direzione (esempio di proprietà (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
