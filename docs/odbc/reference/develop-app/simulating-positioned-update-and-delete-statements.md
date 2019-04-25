---
title: Simulazione di posizionato istruzioni Update e Delete | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445893"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulazione di istruzioni di eliminazione e aggiornamento posizionato
Se l'origine dati non supporta aggiornamento posizionato, quindi eliminare le istruzioni, il driver consente di simulare questi. Ad esempio, la libreria di cursori ODBC Simula aggiornamento posizionato ed eliminare le istruzioni. La strategia generale per la simulazione di istruzioni di eliminazione e aggiornamento posizionato consiste nel convertire le istruzioni posizionate quelle ricercata. Questa operazione viene eseguita sostituendo il **WHERE CURRENT OF** clausola con un ricercata **in cui** clausola che identifica la riga corrente.  
  
 Ad esempio, perché la colonna CustID identifica in modo univoco ogni riga nella tabella Customers, riga posizionata delete-istruzione  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 potrebbero essere convertiti in  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 Il driver è possibile utilizzare uno dei seguenti *identificatori di riga* nel **in cui** clausola:  
  
-   Colonne i cui valori vengono utilizzati per identificare in modo univoco ogni riga della tabella. Ad esempio, chiamando **SQLSpecialColumns** con SQL_BEST_ROWID restituisce la colonna ottima o set di colonne che hanno questo scopo.  
  
-   Pseudocolonne, forniti da alcune origini dati, allo scopo di identificazione univoca per ogni riga. Questi possono anche essere recuperati chiamando **SQLSpecialColumns**.  
  
-   Un indice univoco, se disponibile.  
  
-   Tutte le colonne nel set di risultati.  
  
 Esattamente le colonne che debba usare un driver nel **in cui** clausola costruisce dipende dal driver. In alcuni dati di origini, che determina un identificatore di riga possono essere costose. Tuttavia, è più veloce per l'esecuzione e garantisce che un'istruzione simulata aggiorna o Elimina al massimo una riga. A seconda delle funzionalità del sistema DBMS sottostante, utilizzando un identificatore di riga può essere costoso da configurare. Tuttavia, è più veloce per l'esecuzione e garantisce che un'istruzione simulata aggiornerà o eliminerà solo una riga. La possibilità di usare tutte le colonne nel set di risultati è in genere molto più semplice da configurare. Tuttavia, risulta più lento per l'esecuzione e, se le colonne non identificare in modo univoco una riga, è possibile che nelle righe da aggiornare o eliminare accidentalmente, soprattutto se l'elenco di selezione per il risultato impostato non contiene tutte le colonne esistenti nella tabella sottostante.  
  
 A seconda che delle strategie elencate il driver supporta, un'applicazione può scegliere la strategia vuole che il driver da usare con l'attributo di istruzione SQL_ATTR_SIMULATE_CURSOR. Anche se potrebbe sembrare strano che un'applicazione a rischiare inavvertitamente l'aggiornamento o eliminazione di una riga, l'applicazione è possibile rimuovere questo rischio, garantendo che le colonne nel set di risultati identificano in modo univoco ogni riga nel set di risultati. In questo modo il driver lo sforzo di dover eseguire questa operazione.  
  
 Se il driver viene scelto di utilizzare un identificatore di riga, intercetta il **SELECT FOR UPDATE** istruzione che crea il set di risultati. Se le colonne nell'elenco di selezione non consentono di identificare in modo efficace una riga, il driver aggiunge le colonne necessarie alla fine dell'elenco di selezione. Alcune origini dati dispongono di una singola colonna che identifica sempre in modo univoco una riga, ad esempio la colonna ROWID in Oracle; Se tale colonna è disponibile, il driver lo utilizza. In caso contrario, il driver chiama **SQLSpecialColumns** per ogni tabella di **FROM** clausola per recuperare un elenco delle colonne che identificano in modo univoco ogni riga. Una restrizione comune che deriva da questa tecnica è che la simulazione cursore ha esito negativo se è presente più di una tabella nel **FROM** clausola.  
  
 Indipendentemente dal modo in cui il driver identifica le righe, in genere WPAD il **FOR UPDATE OF** clausola disattivare il **SELECT FOR UPDATE** istruzione prima dell'invio all'origine dati. Il **FOR UPDATE OF** clausola viene utilizzata solo con aggiornamento posizionato ed eliminare le istruzioni. Origini dati che non supportano posizionato aggiornamento e istruzioni di eliminazione a livello generale non la supportano.  
  
 Quando l'applicazione invia un'istruzione delete per l'esecuzione o aggiornamento posizionato, il driver sostituisce i **WHERE CURRENT OF** clausola con un **in cui** clausola che contiene l'identificatore di riga. I valori di queste colonne vengono recuperati da una cache gestita dal driver per ogni colonna viene utilizzata la **in cui** clausola. Dopo che il driver ha sostituito il **in cui** clausola, invia l'istruzione all'origine dati per l'esecuzione.  
  
 Ad esempio, si supponga che l'applicazione invia l'istruzione seguente per creare un set di risultati:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se l'applicazione ha impostato SQL_ATTR_SIMULATE_CURSOR per richiedere una garanzia di univocità e se l'origine dati non fornisce una pseudo colonna che identifica sempre in modo univoco una riga, il driver chiama **SQLSpecialColumns** per il Tabella Customers, individua che CustID è essenziale per la tabella Customers e lo aggiunge all'elenco di selezione e rimuove il **FOR UPDATE OF** clausola:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver rimuove solo il **FOR UPDATE OF** clausola:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Si supponga che l'applicazione scorre il set di risultati e invia l'istruzione seguente per gli aggiornamenti posizionati per l'esecuzione, in cui Cust è il nome del cursore all'interno del set di risultati:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce i **in cui** clausola e associa il parametro CustID alla variabile nella propria cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce i **in cui** clausola e associa i parametri nome, indirizzo e telefono in questa clausola per le variabili nella relativa cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
