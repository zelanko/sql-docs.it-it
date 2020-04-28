---
title: Microsoft OLE DB provider per Internet Publishing | Microsoft Docs
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
ms.openlocfilehash: 19d719ddb4e5a2f7851a1d12dc4abe69069a354f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926756"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Panoramica di Microsoft OLE DB provider per Internet Publishing
Il provider Microsoft OLE DB per Internet Publishing consente a ADO di accedere alle risorse gestite da Microsoft FrontPage o Microsoft Internet Information Server. Le risorse includono file di origine Web, ad esempio file HTML o cartelle Web di Windows 2000.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a questo provider, impostare l'argomento del *provider* della proprietà [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) su:

```vb
MSDAIPP.DSO
```

 Questo valore può essere impostato o letto anche usando la proprietà del [provider](../../../ado/reference/ado-api/provider-property-ado.md) .

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è la seguente:

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -oppure-

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 La stringa è costituita dalle parole chiave seguenti:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il provider di OLE DB per la pubblicazione Internet.|
|**Origine dati** -o- **URL**|Specifica l'URL di un file o di una directory pubblicata in una cartella Web.|
|**ID utente**|Specifica il nome utente.|
|**Password**|Specifica la password dell'utente.|

> [!NOTE]
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare **Trusted_Connection = Yes** o **Integrated Security = SSPI** anziché le informazioni relative a ID utente e password nella stringa di connessione.

 Se si imposta il valore *ResourceURL* da "URL =" nella stringa di connessione su un valore non valido, per impostazione predefinita il provider di pubblicazione Internet genera una finestra di dialogo in cui viene richiesto un valore valido. Si tratta di un comportamento indesiderato per un componente nel livello intermedio di un'applicazione, perché sospende l'esecuzione del programma fino a quando la finestra di dialogo non viene cancellata e il client sembra bloccarsi perché non ha ricevuto una risposta dal componente.

> [!NOTE]
>  Se MSDAIPP. DSO viene specificato in modo esplicito come valore del provider, con la parola chiave della stringa di connessione del *provider* o con la proprietà del **provider** , non è possibile usare "URL =" nella stringa di connessione. In tal caso, si verificherà un errore. In alternativa, è sufficiente specificare l'URL come illustrato nell'argomento [utilizzo di ADO con il provider di OLE DB per la pubblicazione Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Vedere anche
 [Scenario di pubblicazione Internet](../../../ado/guide/data/internet-publishing-scenario.md) [provider di OLE DB per Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
