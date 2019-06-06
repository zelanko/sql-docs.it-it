---
title: Provider Microsoft OLE DB per Internet Publishing | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 48c6e95a644c643721a7cb1c6f15c5eaf1e5a995
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701400"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Provider Microsoft OLE DB per Internet Publishing Panoramica
Il Provider Microsoft OLE DB per Internet Publishing consente ADO per accedere alle risorse gestite da Microsoft FrontPage o Microsoft Internet Information Server. Le risorse includono i file di origine web quali file HTML o le cartelle web di Windows 2000.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare il *Provider* argomento delle [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà:

```vb
MSDAIPP.DSO
```

 Questo valore può anche essere impostato o letto usando il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 oppure

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il Provider OLE DB per Internet Publishing.|
|**Zdroj dat** - oppure - **URL**|Specifica l'URL di un file o directory pubblicata in una cartella Web.|
|**ID utente**|Specifica il nome utente.|
|**Password**|Specifica la password dell'utente.|

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = yes** oppure **Integrated Security = SSPI** anziché un ID utente e password informazioni nella stringa di connessione.

 Se si imposta il *l'URL risorsa* dal valore di "URL =" nella stringa di connessione a un valore non valido, per impostazione predefinita il Provider di pubblicazione Internet genera una finestra di dialogo per la richiesta di un valore valido. Infatti, un comportamento indesiderato per un componente nel livello intermedio di un'applicazione, sospende l'esecuzione del programma fino a quando la finestra di dialogo è stata cancellata e il client sembra bloccarsi poiché non ha ricevuto una risposta dal componente.

> [!NOTE]
>  Se MSDAIPP. DSO è specificato in modo esplicito come valore del provider, con la *Provider* parola chiave di stringa di connessione o il **Provider** proprietà, non è possibile usare "URL =" nella stringa di connessione. In caso contrario si verificherà un errore. In alternativa, specificare semplicemente l'URL come illustrato nell'argomento [utilizzo di ADO con il Provider OLE DB per Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Vedere anche
 [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md) [Provider OLE DB per Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
