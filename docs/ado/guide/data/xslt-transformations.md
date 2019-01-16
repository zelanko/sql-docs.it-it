---
title: Trasformazioni XSLT | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c522a8d278080d9249761309d29f465befe217d8
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255056"
---
# <a name="xslt-transformations"></a>Trasformazioni XSLT
XSLT possono essere applicati al codice XML generato per trasformarlo in un altro formato. Comprendere il formato XML in ADO consente di sviluppare modelli XSLT che possano trasformarlo in un modulo più semplici da usare.  
  
 Ad esempio, si sa che ogni riga del set di record viene salvato come elemento z: riga all'interno dell'elemento dati: rs. Analogamente, ogni campo del set di record viene salvato come una coppia attributo-valore per questo elemento.  
  
## <a name="remarks"></a>Note  
 Il seguente script XSLT può essere applicato al codice XML illustrato nella sezione precedente per trasformarlo in una tabella HTML da visualizzare nel browser:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 Il file XSLT consente di convertire il flusso XML generato dal metodo ADO Salva in una tabella HTML che visualizza ogni campo del set di record con un'intestazione di tabella. Le righe e intestazioni della tabella vengono inoltre assegnate diversi tipi di carattere e colori.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
