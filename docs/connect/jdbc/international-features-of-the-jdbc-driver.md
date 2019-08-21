---
title: Funzionalità internazionali del driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64c046ade18bfdf8789ce9fec221f3d33517fcbb
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028016"
---
# <a name="international-features-of-the-jdbc-driver"></a>Caratteristiche internazionali del driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Le funzionalità di internazionalizzazione di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] includono quanto segue:  
  
-   Supporto per un'interfaccia completamente localizzata nelle stesse lingue di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Supporto per le conversioni di linguaggio Java di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipendenti dalle impostazioni locali  
  
-   Supporto per lingue internazionali, indipendentemente dal sistema operativo  
  
-   Supporto per nomi IDN (a partire da Microsoft JDBC Driver 6.0 per SQL Server)  
  
## <a name="handling-of-character-data"></a>Gestione dei dati di tipo carattere  
 I dati di tipo carattere in Java vengono gestiti come Unicode per impostazione predefinita. L'oggetto **String** Java rappresenta dati di tipo carattere Unicode. Nel driver JDBC l'unica eccezione a questa regola è costituita dai metodi per il richiamo e l'impostazione dei flussi ASCII, che rappresentano casi speciali poiché utilizzano flussi di byte con il presupposto implicito di singole tabelle codici conosciute (ASCII).  
  
 Il driver JDBC fornisce inoltre la proprietà della stringa di connessione **sendStringParametersAsUnicode** . che può essere utilizzata per specificare che i parametri preparati per i dati di tipo carattere verranno inviati in formato ASCII or MBCS (Multi-byte Character Set) anziché Unicode. Per ulteriori informazioni sulla proprietà della stringa di connessione **sendStringParametersAsUnicode** , vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
### <a name="driver-incoming-conversions"></a>Conversioni in ingresso nel driver  
 I dati di tipo text Unicode provenienti dal server non devono essere convertiti. Vengono passati direttamente in formato Unicode. I dati non Unicode provenienti dal server vengono convertiti dalla tabella codici, a livello di database o di colonna, a Unicode. Per eseguire queste conversioni vengono utilizzate le routine di conversione JVM (Java Virtual Machine). Le conversioni vengono eseguite su tutti metodi per il richiamo di flussi String e Character tipizzati.  
  
 Se in JVM non è disponibile il supporto di tabella codici appropriato per i dati del database, verrà generata un'eccezione "La tabella codici XXX non è supportata dall'ambiente Java". Per risolvere il problema, è necessario installare il supporto completo per caratteri internazionali richiesto per tale JVM. Per un esempio, vedere la documentazione relative alle codifiche supportate nel sito Web Sun Microsystems.  
  
### <a name="driver-outgoing-conversions"></a>Conversioni in uscita dal driver  
 I dati di tipo carattere che passano dal driver al server possono essere ASCII o Unicode. Ad esempio, i nuovi metodi per caratteri nazionali di JDBC 4.0, come i metodi setNString, setNCharacterStream e setNClob delle classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), inviano sempre i valori i parametri al server in formato Unicode.  
  
 D'altro canto, i metodi dell'API per caratteri non nazionali, ad esempio i metodi setString, setCharacterStream e setClob delle classi [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) inviano i valori al server in formato Unicode solo quando la proprietà **sendStringParametersAsUnicode** è impostata su "true", che corrisponde al valore predefinito.  
  
## <a name="non-unicode-parameters"></a>Parametri non Unicode  
 Per ottenere prestazioni ottimali con tipi **char**, **varchar** o **LONGVARCHAR** di parametri non Unicode, impostare la proprietà della stringa di connessione **sendStringParametersAsUnicode** su "false" e utilizzare i metodi per caratteri non nazionali.  
  
## <a name="formatting-issues"></a>Problemi di formattazione  
 Per la data, l'ora e le valute, tutte le operazioni di formattazione con i dati localizzati vengono eseguite a livello di linguaggio Java usando l'oggetto Impostazioni locali e i diversi metodi di formattazione per i tipi di dati **Data**, **Calendario** e **Numero**. Nei rari casi in cui il driver JDBC deve passare dati dipendenti dalle impostazioni locali in un formato localizzato, viene utilizzato il formattatore appropriato con le impostazioni locali JVM predefinite.  
  
## <a name="collation-support"></a>Supporto delle regole di confronto  
 JDBC Driver 3.0 supporta tutte le regole di confronto supportate in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], nonché le nuove regole di confronto o le nuove versioni dei nomi di regole di confronto Windows introdotte in [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
 Per altre informazioni sulle regole di confronto, vedere [Regole di confronto e supporto Unicode](https://go.microsoft.com/fwlink/?LinkId=131366) e [Nome delle regole di confronto di Windows (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=131367) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-international-domain-names-idn"></a>Uso di International Domain Names (IDN)  
 JDBC Driver 6.0 per SQL Server supporta l'uso di IDN (Internationalized Domain Name) e può convertire un serverName Unicode in codifica compatibile con ASCII (Punycode) quando richiesto durante una connessione.  Se i nomi IDN vengono archiviati in Domain Name System (DNS) come stringhe ASCII in formato Punycode (specificato dal RFC 3490), abilitare la conversione del nome del server Unicode impostando la proprietà serverNameAsACE su true.  In caso contrario, se il servizio DNS è configurato per consentire l'utilizzo di caratteri Unicode, impostare la proprietà serverNameAsACE su false (impostazione predefinita).  Per le versioni precedenti del driver JDBC, è anche possibile convertire serverName in Punycode usando i metodi [IDN.toASCII di Java](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) prima di impostare tale proprietà per una connessione.  
  
> [!NOTE]  
>  La maggior parte dei software resolver scritti per piattaforme non Windows si basano sugli standard Internet DSN ed è pertanto più facile utilizzare il formato Punycode per nomi IDN, mentre un Server DNS basato su Windows in una rete privata può essere configurato per consentire l'utilizzo di caratteri UTF-8 in base a ciascun server.  Per informazioni dettagliate, vedere [Unicode character support](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx) (Supporto relativo ai caratteri Unicode).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
