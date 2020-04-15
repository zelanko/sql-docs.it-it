---
title: Risoluzione dei problemi (driver ODBC di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303032"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Risoluzione dei problemi (driver ODBC Visual FoxPro)
Nelle sezioni seguenti viene illustrato come migliorare le prestazioni e risolvere i problemi che potrebbero verificarsi durante l'utilizzo del driver ODBC di Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Accesso alle viste con parametriAccessing Parameterized Views  
 Non è possibile accedere alle viste con parametri in un database di Visual FoxPro utilizzando il driver. Una vista con parametri crea una clausola WHERE nell'istruzione SQL **SELECT** della vista che limita i record scaricati ai record che soddisfano le condizioni della clausola WHERE creata utilizzando il valore fornito per il parametro. Poiché il driver non supporta il passaggio di parametri alla visualizzazione, i tentativi di accedere a una visualizzazione con parametri utilizzando il driver avranno esito negativo.  
  
 Il valore del parametro può essere fornito in fase di esecuzione o passato a livello di codice alla visualizzazione.  
  
## <a name="accessing-remote-views"></a>Accesso alle viste remote  
 Non è possibile accedere alle viste remote in un database Di Visual FoxPro utilizzando il driver. Le visualizzazioni remote sono visualizzazioni che accedono a dati non FoxPro o a una combinazione di dati FoxPro e non FoxPro. Per accedere alle viste remote, utilizzare Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminazione di record  
 È possibile contrassegnare i record per l'eliminazione utilizzando il driver, ma non è possibile rimuovere definitivamente i record dal database. Per rimuovere definitivamente i record da una tabella, utilizzare Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Aumento delle prestazioni mediante il recupero in background  
 È possibile migliorare le prestazioni nei recuperi di grandi dimensioni utilizzando la funzionalità di recupero in background del driver. Il recupero in background utilizza un thread separato per recuperare i dati richiesti da un'origine dati specifica.  
  
 È possibile utilizzare il recupero in background per un'origine dati in uno dei modi seguenti:You can employ background fetching for a data source in one of the following ways:  
  
-   Selezionare la casella di controllo **Recupera dati in background** nella finestra di [dialogo Installazione ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Usare la parola chiave dell'attributo BackgroundFetch nella stringa di connessione.  
  
 Per informazioni sulle parole chiave degli attributi delle stringhe di connessione, vedere [Utilizzo delle stringhe](../../odbc/microsoft/using-connection-strings.md)di connessione .  
  
## <a name="updating-multitiered-views"></a>Aggiornamento delle viste a più livelli  
 Una vista a più livelli è una vista basata su una o più viste anziché su una tabella di base. Quando si aggiornano i dati in una vista a più livelli, gli aggiornamenti vengono visualizzati verso il basso di un solo livello, alla visualizzazione su cui si basa la visualizzazione di primo livello; le tabelle di base non vengono aggiornate.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Utilizzo del linguaggio DDL (Data Definition Language) nelle stored procedureUsing Data Definition Language (DDL) in Stored Procedures  
 Non è possibile utilizzare DDL, ad esempio CREATE TABLE o ALTER TABLE, nelle stored procedure di Visual FoxPro.  
  
 Per informazioni sul linguaggio che è possibile utilizzare nelle stored procedure, vedere [Supporto per regole, trigger, valori predefiniti e stored procedure](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Utilizzo degli aggiornamenti posizionati  
 Il driver non supporta gli aggiornamenti posizionati. Utilizzare la clausola SQL WHERE per identificare le righe che si desidera aggiornare.  
  
## <a name="using-the-set-ansi-command"></a>Utilizzo del comando SET ANSI  
 Se sei uno sviluppatore Visual FoxPro, dovresti tenere presente che l'impostazione predefinita per SET ANSI è ON per il driver, a differenza di un'impostazione predefinita OFF per Visual FoxPro. L'impostazione predefinita ON per SET ANSI consente alle origini dati di Visual FoxPro di comportarsi in modo coerente con altre origini dati ODBC che in genere eseguono confronti esatti. È possibile modificare l'impostazione predefinita. Per ulteriori informazioni, vedere [SET ANSI](../../odbc/microsoft/set-ansi-command.md).
