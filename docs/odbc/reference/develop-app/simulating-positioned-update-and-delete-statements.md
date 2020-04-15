---
title: Simulazione di istruzioni di aggiornamento ed eliminazione posizionate Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301992"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulazione di istruzioni di eliminazione e aggiornamento posizionato
Se l'origine dati non supporta le istruzioni di aggiornamento ed eliminazione posizionate, il driver può simularle. Ad esempio, la libreria di cursori ODBC simula le istruzioni di aggiornamento ed eliminazione posizionate. La strategia generale per simulare le istruzioni di aggiornamento ed eliminazione posizionate consiste nel convertire le istruzioni posizionate in istruzioni ricercate. Questa operazione viene eseguita sostituendo la clausola **WHERE CURRENT OF** con una clausola **WHERE** ricercata che identifica la riga corrente.  
  
 Ad esempio, poiché la colonna CustID identifica in modo univoco ogni riga della tabella Customers, l'istruzione delete posizionata  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 potrebbe essere convertito in  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 Il driver può utilizzare uno dei seguenti *identificatori* di riga nella clausola **WHERE:**  
  
-   Colonne i cui valori servono a identificare in modo univoco ogni riga della tabella. Ad esempio, la chiamata **di SQLSpecialColumns** con SQL_BEST_ROWID restituisce la colonna o il set ottimale di colonne che servono a questo scopo.  
  
-   Pseudocolonne, fornite da alcune origini dati, allo scopo di identificare in modo univoco ogni riga. Questi possono anche essere recuperabili chiamando **SQLSpecialColumns**.  
  
-   Un indice univoco, se disponibile.  
  
-   Tutte le colonne nel set di risultati.  
  
 Esattamente quali colonne un driver deve utilizzare nella clausola **WHERE** che costruisce dipende dal driver. In alcune origini dati, determinare un identificatore di riga può essere costoso. Tuttavia, è più veloce da eseguire e garantisce che un'istruzione simulata aggiorni o elimini al massimo una riga. A seconda delle funzionalità del DBMS sottostante, l'utilizzo di un identificatore di riga può essere costoso da configurare. Tuttavia, è più veloce da eseguire e garantisce che un'istruzione simulata aggiornerà o eliminerà solo una riga. La possibilità di utilizzare tutte le colonne nel set di risultati è in genere molto più semplice da configurare. Tuttavia, l'esecuzione è più lenta e, se le colonne non identificano in modo univoco una riga, è possibile che le righe vengano aggiornate o eliminate inavvertitamente, soprattutto quando l'elenco di selezione per il set di risultati non contiene tutte le colonne presenti nella tabella sottostante.  
  
 A seconda di quale delle strategie precedenti il driver supporta, un'applicazione può scegliere quale strategia si desidera che il driver da utilizzare con l'attributo di istruzione SQL_ATTR_SIMULATE_CURSOR. Anche se potrebbe sembrare strano che un'applicazione rischi involontariamente di aggiornare o eliminare una riga, l'applicazione può rimuovere questo rischio assicurando che le colonne nel set di risultati identifichino in modo univoco ogni riga nel set di risultati. Ciò consente di risparmiare al driver lo sforzo di dover eseguire questa operazione.  
  
 Se il driver sceglie di utilizzare un identificatore di riga, intercetta l'istruzione **SELECT FOR UPDATE** che crea il set di risultati. Se le colonne nell'elenco di selezione non identificano in modo efficace una riga, il driver aggiunge le colonne necessarie alla fine dell'elenco di selezione. Alcune origini dati hanno una singola colonna che identifica sempre in modo univoco una riga, ad esempio la colonna ROWID in Oracle; se tale colonna è disponibile, il driver utilizza questo. In caso contrario, il driver chiama **SQLSpecialColumns** per ogni tabella nel **FROM** clausola per recuperare un elenco delle colonne che identificano in modo univoco ogni riga. Una restrizione comune risultante da questa tecnica è che la simulazione del cursore ha esito negativo se è presente più di una tabella nella clausola **FROM.**  
  
 Indipendentemente dal modo in cui il driver identifica le righe, in genere rimuove la clausola **FOR UPDATE OF** dall'istruzione SELECT FOR **UPDATE** prima di inviarla all'origine dati. La clausola **FOR UPDATE OF** viene utilizzata solo con istruzioni di aggiornamento ed eliminazione posizionate. Le origini dati che non supportano le istruzioni di aggiornamento ed eliminazione posizionate in genere non lo supportano.  
  
 Quando l'applicazione invia un'istruzione di aggiornamento o eliminazione posizionata per l'esecuzione, il driver sostituisce la clausola **WHERE CURRENT OF** con una clausola **WHERE** contenente l'identificatore di riga. I valori di queste colonne vengono recuperati da una cache gestita dal driver per ogni colonna utilizzata nella clausola **WHERE.** Dopo che il driver ha sostituito la clausola **WHERE,** invia l'istruzione all'origine dati per l'esecuzione.  
  
 Si supponga, ad esempio, che l'applicazione invii la seguente istruzione per creare un set di risultati:For example, suppose that the application submits the following statement to create a result set:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se l'applicazione ha impostato SQL_ATTR_SIMULATE_CURSOR per richiedere una garanzia di univocità e se l'origine dati non fornisce una pseudo-colonna che identifica sempre in modo univoco una riga, il driver chiama **SQLSpecialColumns** per la tabella Customers, rileva che CustID è la chiave per la tabella Customers e lo aggiunge all'elenco di selezione e rimuove la clausola **FOR UPDATE OF:**  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se l'applicazione non ha richiesto una garanzia di unicità, il driver rimuove solo la clausola **FOR UPDATE OF:**  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Si supponga che l'applicazione scora il set di risultati e invii la seguente istruzione di aggiornamento posizionata per l'esecuzione, dove Cust è il nome del cursore sul set di risultati:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce la clausola **WHERE** e associa il parametro CustID alla variabile nella relativa cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se l'applicazione non ha richiesto una garanzia di univocità, il driver sostituisce la clausola **WHERE** e associa i parametri Name, Address e Phone in questa clausola alle variabili nella cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
