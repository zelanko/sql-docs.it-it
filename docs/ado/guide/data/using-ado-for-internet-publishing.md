---
title: Uso di ADO per Internet Publishing | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d779204046b9bca2591fbdc9459d7c6b53061ff4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184961"
---
# <a name="using-ado-for-internet-publishing"></a>Uso di ADO per Internet Publishing
[Il Provider OLE DB per Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) Mostra un esempio specifico dell'accesso ai dati eterogenei con ADO. Anche se gli esempi in questa sezione saranno specifici per l'uso di Provider di pubblicazione, i principi illustrati dovrebbero essere simili quando si utilizza ADO con altri provider di dati eterogenei, ad esempio un provider in un archivio di posta elettronica.  
  
## <a name="urls"></a>URL  
 Uniform Resource Locator (URL) è utilizzabile come alternativa per le stringhe di connessione e il testo del comando per specificare le origini dati e il percorso del file e directory. È possibile usare gli URL con l'oggetto esistente [Connection](../../../ado/reference/ado-api/connection-object-ado.md) e **Recordset** oggetti e con il **Record** e **Stream** oggetti.  
  
 Per altre informazioni su come usare gli URL, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="record-fields"></a>Campi di record  
 La differenza tra dati eterogenei e dati omogenei essenziale è che nel primo caso, ogni riga di dati, oppure **Record**, può avere un set diverso di colonne, o **campi**. Per i dati omogenei, ogni riga ha lo stesso set di colonne. Per altre informazioni sui campi specifici del Provider di pubblicazione Internet, vedere [record e campi specificati dal provider](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
### <a name="appending-new-fields"></a>Aggiunta di nuovi campi  
 Numerosi oggetti ADO sono stati migliorati per l'uso in combinazione con **Record** e **Stream** oggetti.  
  
-   Il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) collection [Append](../../../ado/reference/ado-api/append-method-ado.md) metodo, che crea e aggiunge un [campo](../../../ado/reference/ado-api/field-object.md) alla raccolta di oggetti, possono anche specificare il valore del **campo**.  
  
-   Il [Update](../../../ado/reference/ado-api/update-method.md) metodo consente di finalizzare l'aggiunta o eliminazione di campi nella raccolta.  
  
-   Come una scelta rapida e alternativi per il **Append** metodo, è possibile creare campi assegnando un valore a un campo non definito o eliminato in precedenza.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Provider OLE DB per Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [URL relativi e assoluti](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [Record e campi specificati dal provider](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Record Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Cronologia di ADO](../../../ado/guide/ado-history.md)
