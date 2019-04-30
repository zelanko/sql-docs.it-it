---
title: Comando pulsanti di Address Book | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e3b29fd5f4fab7e487be5be18752ac7de892537
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222008"
---
# <a name="address-book-command-buttons"></a>Pulsanti di comando di Address Book
L'applicazione Address Book include i pulsanti di comando seguenti:  
  
-   Oggetto **trovare** pulsante per inviare una query al database.  
  
-   Oggetto **cancellare** pulsante per deselezionare le caselle di testo prima di avviare una nuova ricerca.  
  
-   Un' **aggiornare il profilo** consente di salvare le modifiche apportate a un record dipendente.  
  
-   Oggetto **Cancel Changes** pulsante per annullare le modifiche.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Pulsante Trova  
 Facendo clic sui **trovare** pulsante Attiva Find_OnClick routine Sub di VBScript, che crea e invia la query SQL. Facendo clic su questo pulsante consente di popolare la griglia dei dati.  
  
## <a name="building-the-sql-query"></a>La creazione della Query SQL  
 La prima parte della routine Sub Find_OnClick compila la query SQL, una frase alla volta, aggiungendo le stringhe di testo a un'istruzione SQL SELECT globale. Inizia impostando la variabile `myQuery` a un'istruzione SQL SELECT che richiede tutte le righe di dati dalla tabella di origine dati. Successivamente, la routine Sub analizza ognuno dei quattro caselle di input nella pagina.  
  
 Poiché il programma Usa la parola `like` nella creazione di istruzioni SQL, le query sono ricerche delle sottostringhe anziché corrispondenze esatte.  
  
 Ad esempio, se il **Last Name** casella conteneva la voce "Berge" e il **titolo** casella conteneva la voce "Program Manager", l'istruzione SQL (valore di `myQuery`) leggerebbe:  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Se la query ha esito positivo, tutte le persone con un cognome che contiene il testo "Berge" (ad esempio Berge e Berger) e con un titolo che includono le parole "Program Manager" (ad esempio, Program Manager, le tecnologie avanzate) vengono visualizzate nella griglia dei dati HTML.  
  
## <a name="preparing-and-sending-the-query"></a>La preparazione e l'invio di Query  
 L'ultima parte della routine Sub Find_OnClick è costituito da due istruzioni. L'istruzione prima assegna il [SQL](../../../ado/reference/rds-api/sql-property.md) proprietà del [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto uguale alla query SQL compilata in modo dinamico. La seconda istruzione fa sì che il **Servizi Desktop remoto. DataControl** oggetto (`DC1`) per eseguire query sul database e quindi visualizzare i nuovi risultati della query nella griglia.  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Pulsante Aggiorna profilo  
 Facendo clic sui **aggiornare il profilo** pulsante Attiva la routine Sub Update_OnClick VBScript, che esegue il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) e [Aggiorna](../../../ado/reference/rds-api/refresh-method-rds.md) metodi.  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Quando si `DC1.SubmitChanges` viene eseguito, il servizio dati remoto tutte le informazioni sull'aggiornamento di pacchetti e lo invia al server tramite HTTP. L'aggiornamento è esclusiva; Se una parte dell'aggiornamento ha esito negativo, nessuna modifica viene eseguita e viene restituito un messaggio di stato. `DC1.Refresh` non è necessario dopo avere apportato **SubmitChanges** con il servizio dati remoto, ma garantisce dati aggiornati.  
  
## <a name="cancel-changes-button"></a>Pulsante Annulla modifiche  
 Facendo clic **Cancel Changes** di VBScript routine Sub Cancel_OnClick, che viene eseguito il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) dell'oggetto (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) (metodo).  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Quando si `DC1.CancelUpdate` viene eseguito, vengono rimossi eventuali modifiche che un utente ha apportato a un record dipendente nella griglia dei dati dall'ultima query o aggiornamento. Ripristina i valori originali.  
  
## <a name="see-also"></a>Vedere anche  
 [Navigazione pulsanti di Address Book](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


