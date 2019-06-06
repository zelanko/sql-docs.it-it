---
title: Il Provider OLE DB per Internet Publishing | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 62fce79d6ee223ee5b039fe914685fdf3bd33c98
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704803"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>Provider OLE DB per Internet Publishing
L'oggetto ADO [Record](../../../ado/reference/ado-api/record-object-ado.md) e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetti sono utilizzabile con il Provider Microsoft OLE DB per Internet Publishing (Provider di pubblicazione Internet) per accedere e modificare risorse, ad esempio file o cartelle Web gestito da Microsoft FrontPage. Con ADO, è possibile specificare l'origine di un **Record**, **Stream**, o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sia un URL. È possibile caricare, scaricare, spostare, copiare ed eliminare le risorse o modificare direttamente le proprietà delle risorse.  
  
 Ad esempio codice che usa **record** e **flussi** con il Provider di pubblicazione Internet, vedere il [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 Il Provider di pubblicazione Internet viene installato con Microsoft Windows 2000. Le versioni precedenti di Internet Publishing Provider sono anche disponibili con Microsoft Office 2000 e Microsoft Internet Explorer 5.0.  
  
 Esistono tre modi per la connessione di ADO per Internet Publishing Provider:  
  
-   Specificare "URL =" nella stringa di connessione. Ad esempio:  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   Specificare Msdaipp. DSO per il *Provider* parola chiave della stringa di connessione. Ad esempio:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   Specificare Msdaipp. DSO per il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà delle [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. Ad esempio:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Se Msdaipp. DSO in modo esplicito viene specificato come valore del provider, con la *Provider* parola chiave di stringa di connessione o il **Provider** proprietà, non è possibile usare "URL =" nella stringa di connessione. In caso contrario si verificherà un errore. In alternativa, è sufficiente specificare l'URL come illustrato in precedenza.  
  
 Per informazioni più specifiche sul Provider di pubblicazione di Internet, vedere [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), o la documentazione del provider fornito con l'applicazione di origine con cui il Provider OLE DB per La pubblicazione su Internet è stato installato: Windows 2000, Office 2000 o Internet Explorer 5.0.
