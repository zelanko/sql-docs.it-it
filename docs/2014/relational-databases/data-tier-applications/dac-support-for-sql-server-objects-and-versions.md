---
title: Supporto dell'applicazione livello dati per oggetti e versioni di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b528a7a9efb91bb99cb7c2b0a32c71dc0de7785b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811275"
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>Supporto dell'applicazione livello dati per oggetti e versioni di SQL Server
  Un'applicazione livello dati (DAC) supporta gli oggetti del [!INCLUDE[ssDE](../../includes/ssde-md.md)] più comunemente utilizzati.  
  
 **Contenuto dell'argomento**  
  
-   [Oggetti di SQL Server supportati](#SupportedObjects)  
  
-   [Supporto dell'applicazione livello dati con le versioni di SQL Server](#SupportByVersion)  
  
-   [Limitazioni sulla distribuzione dei dati](#DeploymentLimitations)  
  
-   [Considerazioni aggiuntive per le azioni di distribuzione](#Considerations)  
  
##  <a name="SupportedObjects"></a> Oggetti di SQL Server supportati  
 Durante la creazione o la modifica di un'applicazione livello dati, è possibile specificare solo oggetti supportati. Non è possibile estrarre, registrare o importare un'applicazione livello dati da un database esistente che contiene oggetti non supportati in un'applicazione livello dati. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] i seguenti oggetti sono supportati in un'applicazione livello dati.  
  
|||  
|-|-|  
|RUOLO DEL DATABASE|FUNZIONE: inline con valori di tabella|  
|FUNZIONE: con valori di tabella con istruzioni multiple|FUNZIONE: Scalare|  
|INDICE: Cluster|INDICE: Non cluster|  
|INDICE: spaziale|INDICE: Univoco|  
|Account di accesso|Permissions|  
|Appartenenze a ruoli|SCHEMA|  
|Statistiche|STORED PROCEDURE: Transact-SQL|  
|Sinonimi|TABELLA: Vincolo CHECK|  
|TABELLA: Regole di confronto|TABELLA: colonna, incluse le colonne calcolate|  
|TABELLA: vincolo, valore predefinito|TABELLA: vincolo, chiave esterna|  
|TABELLA: vincolo, indice|TABELLA: vincolo, chiave primaria|  
|TABELLA: vincolo, valore univoco|TRIGGER: DML|  
|TIPO: HIERARCHYID, GEOMETRY, GEOGRAPHY|TIPO: tipo di dati definito dall'utente|  
|TIPO: tipo di tabella definito dall'utente|Utente|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> Supporto dell'applicazione livello dati con le versioni di SQL Server  
 Le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano operazioni di applicazione livello dati a livelli diversi. Tutte le operazioni dell'applicazione livello dati supportate da una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportate da tutte le edizioni di tale versione.  
  
 Le istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] supportano le seguenti operazioni dell'applicazione livello dati:  
  
-   Le operazioni di esportazione ed estrazione sono supportate in tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Tutte le operazioni sono supportate nel [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e in tutte le versioni di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]e [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].  
  
-   Tutte le operazioni sono supportate in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) o versioni successive e [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 o versioni successive.  
  
 Framework applicazione livello dati comprende gli strumenti lato client per la compilazione e l'elaborazione di pacchetti di applicazione livello dati e file di esportazione. Nei seguenti prodotti è incluso Framework applicazione livello dati  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è incluso DAC Framework 3.0 che supporta tutte le operazioni dell'applicazione livello dati.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 e Visual Studio 2010 SP1 è incluso DAC Framework 1.1 che supporta tutte le operazioni dell'applicazione livello dati, eccetto l'esportazione e l'importazione.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e Visual Studio 2010 è incluso Framework 1.0, applicazione livello dati, che supporta tutte le operazioni dell'applicazione livello dati eccetto l'esportazione, l'importazione e l'aggiornamento sul posto.  
  
-   Gli strumenti client di versioni precedenti di SQL Server o Visual Studio non supportano operazioni dell'applicazione livello dati.  
  
 Un pacchetto di applicazione livello dati o un file di esportazione compilato con una versione di Framework applicazione livello dati non può essere elaborato da una versione precedente di Framework applicazione livello dati. Ad esempio, un pacchetto di applicazione livello dati estratto utilizzando gli strumenti client di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] non può essere distribuito utilizzando gli strumenti client di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
 Un pacchetto di applicazione livello dati o un file di esportazione compilato con una versione di Framework applicazione livello dati può essere elaborato da qualsiasi versione successiva di Framework applicazione livello dati. Ad esempio, un pacchetto di applicazione livello dati estratto utilizzando gli strumenti client di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] può essere distribuito utilizzando gli strumenti client di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 o versione successiva.  
  
##  <a name="DeploymentLimitations"></a> Limitazioni sulla distribuzione dei dati  
 Si notino le seguenti limitazioni di fedeltà nel motore di distribuzione dati di DAC Framework in SQL Server 2012 SP1. Le limitazioni si applicano alle azioni di DAC Framework seguenti: distribuzione o pubblicazione di un file con estensione dacpac e importazione di un file con estensione bacpac.  
  
1.  Perdita di metadati in determinate situazioni e per alcuni tipi di base nelle colonne sql_variant. Nei casi interessati verrà visualizzato un avviso con il messaggio seguente:  **Determinate proprietà in tipi di dati specifici utilizzati in una colonna sql_variant non vengono mantenute se distribuite mediante DAC Framework.**  
  
    -   Tipi di base MONEY, SMALLMONEY, NUMERIC, DECIMAL:  la precisione non viene mantenuta.  
  
        -   Tipi di base DECIMAL/NUMERIC con precisione 38: i metadati sql_variant "TotalBytes" sono sempre impostati su 21.  
  
    -   Tutti i tipi di base di testo:  le regole di confronto predefinite del database vengono applicate a tutto il testo.  
  
    -   Tipi di base BINARY:  la proprietà Max Length non viene mantenuta.  
  
    -   Tipi di base TIME, DATETIMEOFFSET:  la precisione è sempre impostata su 7.  
  
2.  Perdita di dati nelle colonne sql_variant. Nel caso interessato verrà visualizzato un avviso con il messaggio seguente:  **La distribuzione di un valore in una colonna sql_variant DATETIME2 con scala maggiore di 3 da parte di DAC Framework comporta la perdita di dati. Durante la distribuzione, il valore DATETIME2 è limitato a una scala uguale a 3.**  
  
    -   Tipo di base DATETIME2 con scala maggiore di 3: la scala è limitata a uguale a 3.  
  
3.  L'operazione di distribuzione non viene completata per le condizioni seguenti nelle colonne sql_variant. Nei casi interessati verrà visualizzata una finestra di dialogo con il messaggio seguente:  **Operazione non riuscita a causa di limitazioni dei dati in DAC Framework.**  
  
    -   Tipi di base DATETIME2, SMALLDATETIME e DATE:  se ad esempio il valore non è compreso nell'intervallo DATETIME, l'anno è inferiore al 1753.  
  
    -   Tipo di base DECIMAL, NUMERIC: quando la precisione del valore è maggiore di 28.  
  
##  <a name="Considerations"></a> Considerazioni aggiuntive per le azioni di distribuzione  
 Si tengano presenti le considerazioni seguenti per le azioni di distribuzione dati di DAC Framework:  
  
-   **Estrazione/Esportazione**: queste limitazioni non sono applicabili alle azioni che usano DAC Framework per creare un pacchetto da un database, ad esempio l'estrazione di un file con estensione dacpac e l'esportazione di un file con estensione bacpac. I dati del pacchetto sono una rappresentazione totalmente fedele dei dati nel database di origine. Se una di queste condizioni è presente nel pacchetto, nel registro di estrazione/esportazione sarà contenuto un riepilogo dei problemi tramite i messaggi indicati in precedenza. In questo modo, l'utente verrà avvisato di potenziali problemi di distribuzione dati con il pacchetto creato. L'utente visualizzerà anche il messaggio di riepilogo seguente nel log:  **Queste limitazioni non influiscono sulla fedeltà dei valori e tipi di dati archiviati nel pacchetto di applicazione livello dati (DAC) creato da DAC Framework. Le limitazioni sono applicabili unicamente ai valori e tipi di dati derivanti dalla distribuzione di un pacchetto di applicazione livello dati (DAC) in un database. Per ulteriori informazioni sui dati interessati e su come ovviare a questa limitazione, vedere** [questo argomento](https://go.microsoft.com/fwlink/?LinkId=267086).  
  
-   **Distribuzione/Pubblicazione/Importazione** : queste limitazioni si applicano alle azioni che usano DAC Framework per distribuire un pacchetto in un database, ad esempio la distribuzione o pubblicazione di un file con estensione dacpac e l'importazione di un file con estensione bacpac. I dati presenti nel database di destinazione potrebbero non rappresentare in modo totalmente fedele quelli del pacchetto. Nel registro di distribuzione/importazione sarà contenuto un messaggio, indicato in precedenza, per ogni situazione in cui si è verificato il problema. L'operazione verrà bloccata da errori (vedere la categoria 3 precedente), ma continuerà con gli altri avvisi.  
  
     Per altre informazioni sui dati interessati in questo scenario e su come risolvere questa limitazione per le azioni di distribuzione/pubblicazione/importazione, vedere [questo argomento](https://go.microsoft.com/fwlink/?LinkId=267087).  
  
-   **Soluzioni alternative**: le operazioni di estrazione ed esportazione comporteranno la scrittura di file di dati BCP totalmente fedeli nei file con estensione bacpac o dacpac. Per evitare limitazioni, utilizzare l'utilità della riga di comando BCP.exe di SQL Server per distribuire dati totalmente fedeli in un database di destinazione da un pacchetto di applicazione livello dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](data-tier-applications.md)  
  
  
