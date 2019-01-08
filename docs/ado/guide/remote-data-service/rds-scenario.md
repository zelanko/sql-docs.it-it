---
title: Scenario RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e0f3be43ce8e2780268b7dfde83253b71da946
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539702"
---
# <a name="rds-scenario"></a>Scenario RDS
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 L'applicazione Address Book è uno scenario che illustra come usare Remote Data Service (RDS) per compilare un'applicazione Web semplice e basata sui dati - una rubrica online aziendali. Questo scenario è utile per Microsoft Visual Basic, Scripting Edition (VBScript) e ai programmatori di COM che desiderano imparare a usare i controlli ActiveX in grado di riconoscere i dati con Servizi Desktop remoto per il software più esperto gli sviluppatori che desiderano creare applicazioni Web incentrate sui dati.  
  
 Questo scenario presuppone che si sappia usare layout tag HTML, le tecniche di associazione di dati di utilizzo DHTML e programma di base con i controlli ActiveX.  
  
 Se è stato installato il SDK, il codice sorgente completo per l'applicazione di esempio Address Book è reperibile nella directory SDK in samples\dataaccess\rds\AddressBook\AddressBook.asp. Per visualizzare lo scenario di Address Book, in Internet Explorer 4.0 o versione successiva, digitare **https://*webserver*/RDS/AddressBook/AddressBook.asp** in cui *webserver* corrisponde al nome assegnato al computer server Windows NT 4.0 o Windows 2000 Web che esegue Internet Information Services (IIS) e ASP.  
  
## <a name="introduction-to-address-book"></a>Introduzione alla Rubrica  
 L'applicazione di esempio Address Book offre una rubrica online semplice che è possibile usare per pubblicare una directory disponibili per la ricerca su una rete intranet. Nella Rubrica è progettata in modo che un utente può immettere una stringa di ricerca in uno o più campi per richiedere informazioni sui dipendenti. Per illustrare le funzionalità di base del servizio dati remoto, l'applicazione di esempio è intenzionalmente mantenerle di dimensioni ridotte, con un numero minimo di oggetti e i campi di ricerca.  
  
 L'interfaccia dell'applicazione è costituita dalle parti seguenti:  
  
-   Non visivo **Servizi Desktop remoto. DataControl** oggetto di associazione dati utilizzato dal client per connettersi al database.  
  
-   Caselle di testo HTML che agiscono come campi di input per i criteri di ricerca di attributo dipendente.  
  
-   Pulsanti di comando HTML per compilare query, deselezionare i campi di ricerca, aggiornare il database con informazioni sui dipendenti, annullare le modifiche in sospeso e passare le righe di dati visualizzati nella griglia.  
  
-   Associazione di dati DHTML per visualizzare i dati restituiti dalle query su un database back-end (tramite il **Servizi Desktop remoto. DataControl** oggetto con associazione a dati) in una tabella.  
  
-   Routine di VBScript che si connettono ognuno degli elementi citate in precedenza e consentono loro di interagire. Il codice VBScript viene inoltre utilizzato per inizializzare il **Servizi Desktop remoto. DataControl** dell'oggetto e creare in modo dinamico le intestazioni di colonna della tabella HTML dai nomi del **Servizi Desktop remoto. DataControl** dei campi del recordset.  
  
 Seguire i collegamenti dal passaggio per passaggio per configurare ed eseguire lo scenario e per altre informazioni sul funzionamento dello scenario.  
  
 Questo scenario contiene gli argomenti seguenti.  
  
-   [Requisiti di sistema per l'applicazione Address Book](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Esecuzione dello script SQL per Address Book](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Esecuzione dell'applicazione di esempio Address Book](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Oggetto di data binding di Address Book](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Pulsanti di comando di Address Book](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Pulsanti di spostamento di Address Book](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti di sistema per l'applicazione Address Book](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)


