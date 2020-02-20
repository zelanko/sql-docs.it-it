---
title: Programmazione con SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22f225799e704b7a34449bbfc69ef351cc4d4ac1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027776"
---
# <a name="programming-with-sqlxml"></a>Programmazione con SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In questa sezione viene descritto come usare i metodi dell'API [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per archiviare e recuperare un documento XML in e da un database relazionale con oggetti **SQLXML**.  
  
 Sono inoltre contenute informazioni sui tipi di oggetti SQLXML e vengono elencate importanti linee guida e limitazioni da prendere in considerazione quando si utilizzano oggetti SQLXML.  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>Lettura e scrittura di dati XML con oggetti SQLXML  
 Nell'elenco seguente viene descritto come usare i metodi dell'API [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per leggere e scrivere dati XML con oggetti SQLXML:  
  
-   Per creare un oggetto SQLXML, usare il metodo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Si noti che questo metodo consente di creare un oggetto SQLXML senza dati. Per aggiungere dati **xml** all'oggetto SQLXML, chiamare uno dei metodi seguenti specificati nell'interfaccia SQLXML: setResult, setCharacterStream, setBinaryStream o setString.  
  
-   Per recuperare l'oggetto SQLXML stesso, usare i metodi getSQLXML della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
-   Per recuperare dati **xml** da un oggetto SQLXML, usare uno dei metodi seguenti specificati nell'interfaccia SQLXML: getSource, getCharacterStream, getBinaryStream o getString.  
  
-   Per aggiornare i dati **xml** in un oggetto SQLXML, usare il metodo [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   Per archiviare un oggetto SQLXML in una colonna della tabella del database di tipo **xml**, usare i metodi setSQLXML della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
 Nell'esempio di codice incluso in [Esempio di tipo di dati SQLXML](../../connect/jdbc/sqlxml-data-type-sample.md) viene spiegato come eseguire queste comuni attività dell'API.  
  
## <a name="readable-and-writable-sqlxml-objects"></a>Oggetti SQLXML accessibili in lettura e scrittura  
 Nella seguente tabella sono elencati i tipi di oggetti SQLXML supportati dai metodi di impostazione, richiamo e aggiornamento forniti dall'API di JDBC. Le colonne della tabella fanno riferimento ai seguenti elementi:  
  
-   Nella colonna **Nome metodo** sono elencati i metodi getter, setter e updater supportati nell'API JDBC.  
  
-   La colonna **Oggetto SQLXML getter** rappresenta un oggetto SQLXML, che viene creato tramite il metodo [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) o il metodo [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
-   La colonna **Oggetto SQLXML setter** rappresenta un oggetto SQLXML, che viene creato tramite il metodo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) della classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Si noti che i metodi setter seguenti accettano solo un oggetto SQLXML creato tramite il metodo [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md).  
  
|Nome metodo|Oggetto SQLXML metodo di richiamo<br /><br /> (accessibile in lettura)|Oggetto SQLXML metodo di impostazione<br /><br /> (accessibile in scrittura)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|Non supportato|Supportato|  
|CallableStatement.setObject()|Non supportato|Supportato|  
|PreparedStatement.setSQLXML()|Non supportato|Supportato|  
|PreparedStatement.setObject()|Non supportato|Supportato|  
|ResultSet.updateSQLXML()|Non supportato|Supportato|  
|ResultSet.updateObject()|Non supportato|Supportato|  
|ResultSet.getSQLXML()|Supportato|Non supportato|  
|CallableStatement.getSQLXML()|Supportato|Non supportato|  
  
 Come illustrato nella tabella precedente, i metodi SQLXML di impostazione non funzionano con gli oggetti SQLXML accessibili in lettura. Analogamente i metodi di richiamo non funzioneranno con gli oggetti SQLXML accessibili in scrittura.  
  
 Se l'applicazione richiama il metodo setObject specificando un parametro di scala o di lunghezza con un oggetto SQLXML, il parametro di scala o di lunghezza verrà ignorato.  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>Linee guida e limitazioni relative all'uso di oggetti SQLXML  
 Le applicazioni possono utilizzare gli oggetti SQLXML per leggere e scrivere i dati da e nel database. Nel seguente elenco vengono fornite informazioni su limitazioni e linee guida specifiche da adottare quando si utilizzano oggetti SQLXML:  
  
-   Un oggetto SQLXML può essere valido solo per la durata della transazione in cui è stato creato.  
  
-   Un oggetto SQLXML ricevuto da un metodo di richiamo può essere utilizzato solo per leggere dati.  
  
-   Un oggetto SQLXML creato dall'oggetto connessione può essere utilizzato solo per scrivere dati.  
  
-   Per leggere i dati, l'applicazione può richiamare un solo metodo di richiamo su un oggetto SQLXML accessibile in lettura. Dopo aver richiamato il metodo di richiamo, tutti gli altri metodi di richiamo o impostazione sullo stesso oggetto SQLXML non verranno eseguiti.  
  
-   Dopo un'operazione di lettura o di scrittura relativa all'oggetto SQLXML, l'applicazione può richiamare sull'oggetto solo il metodo free. È tuttavia possibile elaborare l'origine o il flusso restituito purché la colonna o il parametro sottostante sia attivo. Se la colonna o il parametro sottostante diventa inattivo, l'origine o il flusso associato all'oggetto SQLXML verrà chiuso. Se la colonna o il parametro sottostante non è più valido, i dati sottostanti non saranno più disponibili per i metodi di richiamo Stream, Simple API for XML (SAX) e Streaming API for XML (StAX).  
  
-   L'applicazione può richiamare un solo metodo di impostazione su un oggetto SQLXML accessibile in scrittura. Dopo aver richiamato il metodo di impostazione, tutti gli altri metodi di impostazione o richiamo sullo stesso oggetto SQLXML non verranno eseguiti.  
  
-   Per impostare i dati sull'oggetto SQLXML, l'applicazione deve utilizzare il metodo di impostazione appropriato e le funzioni dell'oggetto restituito.  
  
-   I metodi getSQLXML della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e della classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) restituiscono dati **null** se la colonna sottostante è **null**.  
  
-   Gli oggetti del metodo di impostazione sono validi per la durata della connessione in cui sono stati creati.  
  
-   Alle applicazioni non è consentito impostare un valore **null** usando i metodi setter forniti dall'interfaccia SQLXML. Le applicazioni possono impostare una stringa vuota ("") utilizzando i metodi di impostazione forniti nell'interfaccia SQLXML. Per impostare un valore **null**, le applicazioni devono chiamare uno dei metodi seguenti:  
  
    -   I metodi setNull della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   I metodi setObject della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
    -   I metodi setSQLXML della classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) e della classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) con un valore di parametro **null**.  
  
-   Per prestazioni ottimali durante la modifica di documenti XML è consigliabile utilizzare i parser Simple API for XML (SAX) e Streaming API for XML (StAX) anziché i parser Document Object Model (DOM).  
  
 I parser XML non gestiscono i valori vuoti. SQL Server consente tuttavia alle applicazioni di recuperare e archiviare valori vuoti da e nelle colonne del database del tipo di dati XML. Se pertanto durante l'analisi dei dati XML il valore sottostante è vuoto, il parser genererà un'eccezione. Per gli output DOM il driver JDBC rileverà l'eccezione e genererà un errore. Per gli output SAX e StAX l'errore deriverà direttamente dal parser.  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>Supporto del buffer adattivo con SQLXML  
 I flussi di caratteri e binari restituiti dall'oggetto SQLXML rispettano le modalità di buffer adattivo o completo. Se invece i parser XML non sono flussi, non rispetteranno le impostazioni del buffer adattivo o completo. Per altre informazioni sul buffer adattivo, vedere [Uso del buffer adattivo](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto dei dati XML](../../connect/jdbc/supporting-xml-data.md)  
  
  
