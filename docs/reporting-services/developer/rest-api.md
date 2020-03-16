---
title: Sviluppare usando le API REST
description: L'API REST consente l'accesso programmatico agli oggetti contenuti nel catalogo di un server di report di SQL Server 2017 Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: developer
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/12/2018
ms.openlocfilehash: 90ccb4084f9dc2a2a2cd1da4f51281df147524c6
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937672"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Sviluppare con le API REST per Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services supporta le API REST (Representational State Transfer, trasferimento di stato rappresentativo). Le API REST sono endpoint di servizio che supportano un set di operazioni HTTP (metodi) che offrono l'accesso con diritti di creazione, recupero, aggiornamento o eliminazione per le risorse contenute in un server di report.

L'API REST consente l'accesso programmatico agli oggetti contenuti nel catalogo di un server di report di SQL Server 2017 Reporting Services. Esempi di oggetti sono cartelle, report, indicatori KPI, origini dati, set di dati, piani di aggiornamento, sottoscrizioni e così via. Tramite l'API REST è ad esempio possibile esplorare la gerarchia di cartelle, individuare il contenuto di una cartella o scaricare la definizione di un report. È anche possibile creare, aggiornare ed eliminare oggetti. Esempi di attività che è possibile eseguire sugli oggetti includono il caricamento di un report, l'esecuzione di un piano di aggiornamento, l'eliminazione di una cartella e così via.

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>Componenti della richiesta-risposta di un'API REST

La coppia richiesta-risposta di un'API REST può essere suddivisa in cinque componenti:

* L'**URI della richiesta**, costituito da: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Anche se l'URI della richiesta è incluso nell'intestazione del messaggio di richiesta, viene qui considerato come elemento distinto perché la maggior parte dei linguaggi o dei framework richiede di passarlo separatamente dal messaggio di richiesta.

    * Schema dell'URI: indica il protocollo usato per trasmettere la richiesta. Ad esempio, `http` o `https`.
    * Host dell'URI: specifica il nome di dominio o l'indirizzo IP del server in cui l'endpoint del servizio REST è ospitato, ad esempio `myserver.contoso.com`.
    * Percorso della risorsa: specifica la risorsa o la raccolta di risorse che può includere più segmenti usati dal servizio per determinare la selezione di queste risorse. Ad esempio: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` può essere usato per ottenere le proprietà specificate per CatalogItem.
    * Stringa di query (facoltativo): specifica parametri semplici aggiuntivi, ad esempio la versione dell'API o i criteri di selezione delle risorse.

* Campi di intestazione del messaggio di richiesta HTTP:

    * Un [metodo HTTP](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) necessario (noto anche come operazione o verbo) che indica al servizio il tipo di operazione richiesto. Le API REST di Reporting Services supportano i metodi DELETE, GET, HEAD, PUT, POST e PATCH.
    * Campi di intestazione aggiuntivi facoltativi, come richiesto dall'URI e dal metodo HTTP specificati.

* Campi facoltativi del **corpo del messaggio di richiesta** HTTP per supportare l'operazione URI e HTTP. Le operazioni POST contengono ad esempio oggetti con codifica MIME che vengono passati come parametri complessi. Per le operazioni POST o PUT, il tipo di codifica MIME per il corpo deve essere specificato anche nell'intestazione della richiesta `Content-type`. Alcuni servizi richiedono l'uso di un tipo MIME specifico, ad esempio `application/json`.

* Campi di **intestazione del messaggio di risposta** HTTP:

    * Un [codice di stato HTTP](http://www.w3.org/Protocols/HTTP/HTRESP.html), compreso tra codici di riuscita 2xx e codici di errore 4xx o 5xx. In alternativa, può essere restituito un codice di stato definito dal servizio, come indicato nella documentazione dell'API.
    * Campi di intestazione aggiuntivi facoltativi eventualmente necessari per supportare la risposta della richiesta, ad esempio un'intestazione della risposta `Content-type`.

* Campi facoltativi del **corpo del messaggio di risposta** HTTP:

    * Gli oggetti della risposta con codifica MIME vengono restituiti nel corpo della risposta HTTP, ad esempio una risposta da un metodo GET che restituisce dati. In genere, questi oggetti vengono restituiti in un formato strutturato, ad esempio JSON o XML, come indicato dall'intestazione della risposta `Content-type`.

## <a name="api-documentation"></a>Documentazione dell'API

Un'API REST moderna richiede una documentazione moderna. L'API REST si basa sulla specifica OpenAPI (detta anche specifica Swagger) e la documentazione è disponibile in [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Oltre a documentare l'API, SwaggerHub consente anche di generare una libreria client nel linguaggio preferito, ovvero JavaScript, TypeScript, C#, Java, Python, Ruby e altri.

## <a name="testing-api-calls"></a>Test delle chiamate API

Uno strumento per testare i messaggi di richiesta-risposta HTTP è [Fiddler](https://www.telerik.com/fiddler). Fiddler è un proxy di debug Web gratuito in grado di intercettare le richieste REST, semplificando la diagnosi dei messaggi di richiesta-risposta HTTP.

## <a name="next-steps"></a>Passaggi successivi

Vedere le API disponibili in [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

Esempi sono disponibili in [GitHub](https://github.com/Microsoft/Reporting-Services). L'esempio include un'app HTML5 basata su TypeScript, React e webpack insieme a un esempio di PowerShell.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
