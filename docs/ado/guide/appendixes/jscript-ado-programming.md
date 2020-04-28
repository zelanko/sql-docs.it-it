---
title: Programmazione ADO JScript | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d07759405dc337667cc8971ce7795af428a0cfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926806"
---
# <a name="jscript-ado-programming"></a>Programmazione ADO JScript
## <a name="creating-an-ado-project"></a>Creazione di un progetto ADO  
 Microsoft JScript non supporta le librerie dei tipi, pertanto non è necessario fare riferimento a ADO nel progetto. Di conseguenza, non sono supportate funzionalità associate come il completamento della riga di comando. Inoltre, per impostazione predefinita, le costanti enumerate ADO non sono definite in JScript.  
  
 ADO fornisce tuttavia due file di inclusione contenenti le seguenti definizioni da utilizzare con JScript:  
  
-   Per gli script sul lato server, usare Adojavas. Inc, installato nelle cartelle della libreria ADO.  
  
-   Per gli script sul lato client, usare Adcjavas. Inc, che viene installato nelle cartelle della libreria ADO.  
  
 È possibile copiare e incollare le definizioni di costanti da questi file nelle pagine ASP o, se si sta eseguendo lo script sul lato server, copiare il file Adojavas. Inc in una cartella nel sito Web e fare riferimento alla pagina ASP come indicato di seguito:  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Creazione di oggetti ADO in JScript  
 È invece necessario utilizzare la chiamata di funzione **CreateObject** :  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Esempio di JScript  
 Il codice seguente è un esempio generico di programmazione sul lato server di JScript in un file di Active Server pagina (ASP) che apre un oggetto **Recordset** :  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
