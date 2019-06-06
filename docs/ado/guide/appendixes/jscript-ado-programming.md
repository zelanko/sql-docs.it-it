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
manager: jroth
ms.openlocfilehash: 5e53f1d6e30497282cce8e895f458d81660240d9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701298"
---
# <a name="jscript-ado-programming"></a>Programmazione ADO JScript
## <a name="creating-an-ado-project"></a>Creazione di un progetto di ADO  
 Microsoft JScript non supporta le librerie dei tipi, quindi non è necessario fare riferimento ad ADO nel progetto. Di conseguenza, è supportata alcuna funzionalità associata come il completamento della riga di comando. Inoltre, per impostazione predefinita, le costanti enumerate ADO non sono definite in JScript.  
  
 ADO fornisce, tuttavia, che è con due simboli di includere i file che contiene le definizioni seguenti da usare con JScript:  
  
-   Per la creazione di script sul lato server utilizzare Adojavas. Inc, che viene installato nella cartella libreria ADO.  
  
-   Per la creazione di script sul lato client utilizzare Adcjavas. Inc, che viene installato nella cartella libreria ADO.  
  
 È possibile copiare e incollare le definizioni di costanti da questi file nelle pagine ASP oppure, se si sta eseguendo lo scripting lato server, copiare Adojavas. Inc file in una cartella sul sito Web e farvi riferimento dalla pagina ASP simile al seguente:  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Creazione di oggetti ADO JScript  
 È invece necessario usare il **CreateObject** chiamata di funzione:  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Esempio di JScript  
 Il codice seguente è un esempio generico di programmazione sul lato server JScript in un file di pagina ASP (Active Server) che consente di aprire una **Recordset** oggetto:  
  
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
