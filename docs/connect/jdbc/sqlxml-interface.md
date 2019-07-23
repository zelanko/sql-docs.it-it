---
title: Interfaccia SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f235525e7a633bc0c49d39f8bec6bf4a79c0885d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006027"
---
# <a name="sqlxml-interface"></a>Interfaccia SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Con il driver JDBC viene fornito supporto per l'API di JDBC 4.0, in cui viene presentata l'interfaccia java.sql.SQLXML. Tale interfaccia definisce i metodi per interagire e modificare i dati XML. Il tipo di dati **SQLXML** viene mappato al tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dati **XML** .  
  
L'interfaccia SQLXML fornisce metodi per accedere al valore XML come **stringa**, **lettore** o **writer**o come **flusso**. È inoltre possibile accedere al valore XML tramite **Origine** oppure impostarlo come **Risultato**, utilizzati con le API dei parser XML, tra cui Document Object Model (DOM), Simple API for XML (SAX) e Streaming API for XML (StAX), nonché con trasformazioni XSLT e XPath.  
  
## <a name="remarks"></a>Remarks  

Nella tabella seguente sono descritti i metodi definiti nell'interfaccia SQLXML:  
  
|Sintassi del metodo|Descrizione del metodo|  
|-------------------|------------------------|  
|[void free()](https://go.microsoft.com/fwlink/?LinkId=131685)|Consente di liberare l'oggetto SQLXML e di rilasciare le risorse da questo bloccate.|  
|[InputStream getBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131754)|Restituisce un flusso di input per la lettura di dati da SQLXML.|  
|[Reader getCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131755)|Restituisce i dati **XML** come oggetto java.io.Reader o come flusso di caratteri.|  
|[T estende source t GetSource (classe\<t > SourceClass)](https://go.microsoft.com/fwlink/?LinkId=131756)|Restituisce un' **origine** per la lettura del valore **XML** specificato da questo oggetto **SQLXML** .<br /><br /> **Nota:** Il metodo getSource supporta le seguenti origini: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource e java.io.InputStream.|  
|[String getString()](https://go.microsoft.com/fwlink/?LinkId=131757)|Restituisce una rappresentazione di stringa del valore **XML** indicato dall'oggetto SQLXML.|  
|[OutputStream setBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131758)|Recupera un flusso che può essere utilizzato per scrivere il valore **XML** rappresentato dall'oggetto SQLXML.|  
|[Writer setCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131759)|Restituisce un flusso da utilizzare per scrivere il valore **XML** rappresentato dall'oggetto SQLXML.|  
|[T estende il risultato t (classe\<t > resultClass)](https://go.microsoft.com/fwlink/?LinkId=131760)|Restituisce un **risultato** per l'impostazione del valore **XML** specificato da questo oggetto **SQLXML** .<br /><br /> **Nota:** Il metodo setResult supporta le seguenti origini: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult e java.io.OutputStream.|  
|[void setString(String value)](https://go.microsoft.com/fwlink/?LinkId=131762)|Imposta il valore XML indicato dall'oggetto SQLXML sulla rappresentazione **Stringa** specificata.|  
  
Le applicazioni possono leggere e scrivere valori XML da e in un oggetto SQLXML una sola volta.  
  
Quando viene chiamato il metodo free(), un oggetto SQLXML diventa non valido e non è accessibile in lettura o scrittura. Se l'applicazione tenta di richiamare su tale oggetto SQLXML un metodo diverso da free(), verrà generata un'eccezione.  
  
L'oggetto SQLXML non diventa né leggibile né scrivibile quando l'applicazione chiama uno dei metodi get seguenti: getSource, getCharacterStream, getBinaryStream e GetString.  
  
L'oggetto SQLXML non diventa né scrivibile né leggibile quando l'applicazione chiama uno dei metodi setter seguenti: seresult, setCharacterStream, setBinaryStream e substring.  
  
## <a name="see-also"></a>Vedere anche  

[Supporto di dati XML](../../connect/jdbc/supporting-xml-data.md)  
