---
title: Provider di OLE DB per la pubblicazione Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80a373196f98a964bc3e522cc9329907a3392b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923908"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>Provider OLE DB per Internet Publishing
Il [record](../../../ado/reference/ado-api/record-object-ado.md) ADO e gli oggetti [flusso](../../../ado/reference/ado-api/stream-object-ado.md) possono essere utilizzati con il provider Microsoft OLE DB per Internet Publishing (Internet Publishing Provider) per accedere e modificare le risorse, ad esempio le cartelle Web o i file serviti da Microsoft FrontPage. Con ADO è possibile specificare l'origine di un **record**, di un **flusso**o di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) come URL. È quindi possibile caricare, scaricare, spostare, copiare ed eliminare risorse oppure modificare direttamente le proprietà delle risorse.  
  
 Per un esempio di codice in cui vengono utilizzati **record** e **flussi** con il provider di pubblicazione Internet, vedere lo [scenario di pubblicazione Internet](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 Il provider di pubblicazione Internet viene installato con Microsoft Windows 2000. Le versioni precedenti del provider di pubblicazione Internet sono disponibili anche con Microsoft Office 2000 e Microsoft Internet Explorer 5,0.  
  
 Esistono tre modi per connettere ADO al provider di pubblicazione Internet:  
  
-   Specificare "URL =" nella stringa di connessione. Ad esempio:  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   Specificare MSDAIPP. DSO per la parola chiave *provider* della stringa di connessione. Ad esempio:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   Specificare MSDAIPP. DSO per la proprietà [provider](../../../ado/reference/ado-api/provider-property-ado.md) dell'oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) . Ad esempio:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Se Msdaipp. DSO viene specificato in modo esplicito come valore del provider, con la parola chiave della stringa di connessione del *provider* o con la proprietà del **provider** , non è possibile utilizzare "URL =" nella stringa di connessione. In tal caso, si verificherà un errore. In alternativa, è sufficiente specificare l'URL, come illustrato in precedenza.  
  
 Per informazioni più specifiche su Internet Publishing Provider, vedere [Microsoft OLE DB provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)oppure la documentazione del provider fornita con l'applicazione di origine con cui è stato installato il provider OLE DB per Internet Publishing: Windows 2000, Office 2000 o Internet Explorer 5,0.
