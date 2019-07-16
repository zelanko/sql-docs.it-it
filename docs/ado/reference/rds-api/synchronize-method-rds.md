---
title: Synchronize (metodo) (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280e5f8c9eda472c6448b199ffa94ac18c13751
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963268"
---
# <a name="synchronize-method-rds"></a>Metodo Synchronize (Servizi Desktop remoto)
Sincronizzare i set di record specificato con il database specificato dalla stringa di connessione per l'utilizzo in ADO 2.5 e versioni successiva.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ConnectionString*  
 Stringa utilizzata per la connessione al provider OLE DB in cui verrà inviata la richiesta. Se viene utilizzato un gestore, il gestore può modificare o sostituire la stringa di connessione.  
  
 *HandlerString*  
 La stringa identifica il gestore da utilizzare con questa esecuzione. La stringa contiene due parti. La prima parte contiene il nome (ProgID) del gestore da utilizzare. La seconda parte della stringa contiene argomenti da passare al gestore. Come viene interpretata la stringa di argomenti è gestore specifico. Le due parti sono separate dall'istanza prima della virgola nella stringa di (anche se la stringa di argomenti potrebbe contenere virgole aggiuntive). Gli argomenti sono facoltativi.  
  
 *lSynchronizeOptions*  
 Maschera di bit delle opzioni di sincronizzazione.  
  
 1 =*UpdateTransact* aggiornamenti al database vengono eseguito il wrapping in una transazione. La transazione viene interrotta se uno o più aggiornamenti ha esito negativo.  
  
 2 =*RefreshWithUpdate* cause di righe da restituire quando nessuno dei due stati *aggiornare* né *RefreshConflicts* è impostata.  
  
 4 =*Aggiorna* il set di record viene aggiornato con i dati correnti dal database. Gli aggiornamenti in sospeso non vengono inseriti nel database. Se questo bit non è impostato, il set di record non viene aggiornato e vengono effettuato il push di eventuali aggiornamenti in sospeso al database.  
  
 8 =*RefreshConflicts* tutte le righe con modifiche in sospeso non è possibile aggiornare. Le righe che non è riuscita per l'aggiornamento vengono aggiornate con i dati correnti dal database.  
  
 *ppRecordset*  
 Puntatore al set di record da sincronizzare.  
  
 *pStatusArray*  
 Una variante usata per restituire una matrice protetta di stati di riga per le righe interessate da sincronizzare. Non impostare se nessuna delle opzioni di sincronizzazione seguenti sono impostata: *RefreshWithUpdate*, *Refresh* e *RefreshConflicts*.  
  
 *lcid*  
 L'identificatore LCID utilizzato per compilare gli eventuali errori che vengono restituiti in *pInformation*.  
  
 *pInformation*  
 Un puntatore al messaggio di errore informativo restituito da **Execute**. Se NULL, viene restituita alcuna informazione di errore.  
  
## <a name="remarks"></a>Note  
 Il *HandlerString* parametro può essere null. Cosa accade in questo caso dipende dal modo in cui il server di servizi desktop remoto è configurato. Nome di un gestore di "MSDFMAP. Handler" indica che il gestore di Microsoft fornito (Msdfmap.dll) deve essere utilizzato. Nome di un gestore di "MASDFMAP.handler,sample.ini" indica che il gestore Msdfmap.dll deve essere utilizzato e che l'argomento "il file" deve essere passato al gestore. MSDFMAP.dll interpreterà quindi l'argomento come una direzione da utilizzare il file per controllare le stringhe di connessione e la query.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


