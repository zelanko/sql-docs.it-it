---
title: Interfaccia SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 58fb89e88169a5ebabd63a39b9d2427fa63d5a9d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909407"
---
# <a name="sqlxml-interface"></a>Interfaccia SQLXML

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Con il driver JDBC viene fornito supporto per l'API di JDBC 4.0, in cui viene presentata l'interfaccia java.sql.SQLXML. Tale interfaccia definisce i metodi per interagire e modificare i dati XML. Il tipo di dati **SQLXML** viene mappato sul tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml**.  
  
L'interfaccia SQLXML offre metodi per accedere al valore XML come **Stringa**, **Lettore** o **Scrittore** oppure come **Flusso**. È inoltre possibile accedere al valore XML tramite **Origine** oppure impostarlo come **Risultato**, utilizzati con le API dei parser XML, tra cui Document Object Model (DOM), Simple API for XML (SAX) e Streaming API for XML (StAX), nonché con trasformazioni XSLT e XPath.  
  
## <a name="remarks"></a>Osservazioni  

Nella tabella seguente sono descritti i metodi definiti nell'interfaccia SQLXML:  
  
|Sintassi del metodo|Descrizione del metodo|  
|-------------------|------------------------|  
|[void free()](https://go.microsoft.com/fwlink/?LinkId=131685)|Consente di liberare l'oggetto SQLXML e di rilasciare le risorse da questo bloccate.|  
|[InputStream getBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131754)|Restituisce un flusso di input per la lettura di dati da SQLXML.|  
|[Reader getCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131755)|Restituisce i dati **XML** come oggetto java.io.Reader o come flusso di caratteri.|  
|[T extends Source T getSource(Class\<T> sourceClass)](https://go.microsoft.com/fwlink/?LinkId=131756)|Restituisce un **Source** per la lettura del valore **XML** specificato da questo oggetto **SQLXML**.<br /><br /> **Nota:** Il metodo getSource supporta le seguenti origini: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource e java.io.InputStream.|  
|[String getString()](https://go.microsoft.com/fwlink/?LinkId=131757)|Restituisce una rappresentazione di stringa del valore **XML** indicato dall'oggetto SQLXML.|  
|[OutputStream setBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131758)|Recupera un flusso che può essere utilizzato per scrivere il valore **XML** rappresentato dall'oggetto SQLXML.|  
|[Writer setCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131759)|Restituisce un flusso da utilizzare per scrivere il valore **XML** rappresentato dall'oggetto SQLXML.|  
|[T extends Result T setResult(Class\<T> resultClass)](https://go.microsoft.com/fwlink/?LinkId=131760)|Restituisce un **Result** per l'impostazione del valore **XML** specificato da questo oggetto **SQLXML**.<br /><br /> **Nota:** Il metodo setResult supporta le seguenti origini: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult e java.io.OutputStream.|  
|[void setString(String value)](https://go.microsoft.com/fwlink/?LinkId=131762)|Imposta il valore XML indicato dall'oggetto SQLXML sulla rappresentazione **Stringa** specificata.|  
  
Le applicazioni possono leggere e scrivere valori XML da e in un oggetto SQLXML una sola volta.  
  
Quando viene chiamato il metodo free(), un oggetto SQLXML diventa non valido e non è accessibile in lettura o scrittura. Se l'applicazione tenta di richiamare su tale oggetto SQLXML un metodo diverso da free(), verrà generata un'eccezione.  
  
L'oggetto SQLXML diventa inaccessibile in lettura o scrittura quando l'applicazione chiama uno dei seguenti metodi getter: getSource, getCharacterStream, getBinaryStream e getString.  
  
L'oggetto SQLXML diventa inaccessibile in lettura o scrittura quando l'applicazione chiama uno dei seguenti metodi setter: setResult, setCharacterStream, setBinaryStream e setString.  
  
## <a name="see-also"></a>Vedere anche  

[Supporto dei dati XML](../../connect/jdbc/supporting-xml-data.md)  
