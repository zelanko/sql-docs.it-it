---
title: Simulazione di istruzioni Update e Delete posizionate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85d7642620d510ebba050a3fbc4348898e070070
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107528"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulazione di istruzioni di eliminazione e aggiornamento posizionato
Se l'origine dati non supporta le istruzioni Update e Delete posizionate, il driver può simulare tali istruzioni. La libreria di cursori ODBC, ad esempio, simula le istruzioni Update e Delete posizionate. La strategia generale per simulare le istruzioni Update e Delete posizionate consiste nel convertire le istruzioni posizionate in una ricerca. Questa operazione viene eseguita sostituendo la clausola **where current of** con una clausola **where** cercata che identifica la riga corrente.  
  
 Ad esempio, poiché la colonna CustID identifica in modo univoco ogni riga nella tabella Customers, l'istruzione DELETE posizionata  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 potrebbe essere convertito in  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 Il driver può utilizzare uno dei seguenti *identificatori di riga* nella clausola **where** :  
  
-   Colonne i cui valori servono per identificare in modo univoco ogni riga della tabella. Ad esempio, la chiamata di **SQLSpecialColumns** con SQL_BEST_ROWID restituisce la colonna o il set di colonne ottimale che soddisfano questo scopo.  
  
-   Pseudo-colonne, fornite da alcune origini dati, allo scopo di identificare in modo univoco ogni riga. Questi possono anche essere recuperabili chiamando **SQLSpecialColumns**.  
  
-   Indice univoco, se disponibile.  
  
-   Tutte le colonne del set di risultati.  
  
 Esattamente le colonne che un driver deve utilizzare nella clausola **where** che costruisce dipende dal driver. In alcune origini dati, la determinazione di un identificatore di riga può essere costosa. Tuttavia, è più veloce da eseguire e garantisce che un'istruzione simulata aggiorni o elimini al massimo una riga. A seconda delle funzionalità del sistema DBMS sottostante, l'utilizzo di un identificatore di riga può essere costoso da configurare. Tuttavia, l'esecuzione è più veloce e garantisce che un'istruzione simulata aggiornerà o eliminerà una sola riga. L'opzione di utilizzo di tutte le colonne nel set di risultati è in genere molto più semplice da configurare. Tuttavia, è più lento eseguire e, se le colonne non identificano in modo univoco una riga, può comportare l'aggiornamento o l'eliminazione accidentale di righe, in particolare quando l'elenco di selezione per il set di risultati non contiene tutte le colonne presenti nella tabella sottostante.  
  
 A seconda delle strategie precedenti supportate dal driver, un'applicazione può scegliere la strategia da usare con l'attributo dell'istruzione SQL_ATTR_SIMULATE_CURSOR. Sebbene possa sembrare strano che un'applicazione rischi di aggiornare o eliminare accidentalmente una riga, l'applicazione può rimuovere questo rischio garantendo che le colonne del set di risultati identifichino in modo univoco ogni riga nel set di risultati. Questo consente di risparmiare sul driver il lavoro necessario per eseguire questa operazione.  
  
 Se il driver sceglie di utilizzare un identificatore di riga, intercetta l'istruzione **Select for Update** che crea il set di risultati. Se le colonne nell'elenco di selezione non identificano in modo efficace una riga, il driver aggiunge le colonne necessarie alla fine dell'elenco di selezione. Alcune origini dati dispongono di una singola colonna che identifica sempre in modo univoco una riga, ad esempio la colonna ROWID in Oracle. Se tale colonna è disponibile, il driver lo utilizzerà. In caso contrario, il driver chiama **SQLSpecialColumns** per ogni tabella nella clausola **from** per recuperare un elenco delle colonne che identificano in modo univoco ogni riga. Una restrizione comune che deriva da questa tecnica è che la simulazione del cursore ha esito negativo se nella clausola **from** sono presenti più tabelle.  
  
 Indipendentemente dal modo in cui il driver identifica le righe, viene in genere eliminata la clausola **for Update of** dall'istruzione **Select for Update** prima dell'invio all'origine dati. La clausola **for Update of** viene utilizzata solo con le istruzioni Update e Delete posizionate. Le origini dati che non supportano le istruzioni Update e Delete posizionate in genere non lo supportano.  
  
 Quando l'applicazione invia un'istruzione Update o DELETE posizionata per l'esecuzione, il driver sostituisce la clausola **where current of** con una clausola **where** contenente l'identificatore di riga. I valori di queste colonne vengono recuperati da una cache gestita dal driver per ogni colonna utilizzata nella clausola **where** . Dopo aver sostituito la clausola **where** , il driver invia l'istruzione all'origine dati per l'esecuzione.  
  
 Si supponga, ad esempio, che l'applicazione invii l'istruzione seguente per creare un set di risultati:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se l'applicazione ha impostato SQL_ATTR_SIMULATE_CURSOR per richiedere una garanzia di univocità e se l'origine dati non fornisce una pseudo-colonna che identifica sempre in modo univoco una riga, il driver chiama **SQLSpecialColumns** per la tabella Customers, individua che CustID è la chiave per la tabella Customers e la aggiunge all'elenco SELECT e rimuove la clausola **for Update of** :  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver rimuove solo la clausola **for Update of** :  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Si supponga che l'applicazione scorra il set di risultati e invii la seguente istruzione di aggiornamento posizionata per l'esecuzione, dove Cust è il nome del cursore sul set di risultati:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce la clausola **where** e associa il parametro CustID alla variabile nella cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce la clausola **where** e associa il nome, l'indirizzo e i parametri del telefono in questa clausola alle variabili nella relativa cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
